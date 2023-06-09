# 6장 메모리와 캐시 메모리

메모리는 보통 RAM 이라는 장치입니다.

RAM 종류에는 DRAM, SRAM, SDRAM, DDR SDRAM이 있습니다.

## 특징

RAM에는 우리가 실행할 프로그램의 명령어와 데이터가 저장됩니다.

또한 RAM은 전원을 끄면 저장된 명령어와 데이터가 모두 사라지는 휘발성 저장 장치입니다.

이와 달리 전원이 꺼져도 내용이 유지되지 저장 장치를 비휘발성 저장 장치라고 합니다.

ex ) 하드 디스크, SSD, CD-ROM, USB 같은 보조기억장치들

CPU는 보조기억장치에 직접 접근 X 따라서 실행하려고 하는 프로그램을 보조기억장치에서 불러와 이를 RAM으로 복사하여 저장한 뒤 실행합니다.

- 일반적으로 보조기억장치는 ‘보관할 대상’을 저장
- RAM에는 ‘실행할 대상’을 저장

<img width="474" alt="스크린샷 2023-05-02 오후 9 19 21" src="https://user-images.githubusercontent.com/61916401/235866613-c0f1cb5d-9a02-480f-b604-05d5f3b425e9.png">


<aside>
💡 메모리가 초과되는 경우 하드 디스크 가상메모리 페이징을 하여 하드 디스크에 일부를 메모리 처럼 사용 가능

</aside>

## 용량과 성능

RAM 용량이 크면 많은 프로그램을 동시에 빠르게 실행하는데 유리합니다.

용량이 크면 보조기억장치에서 많은 데이터를 가져와 미리 RAM에 저장할 수 있지만 용량이 작다면 보조기억장치에서 여러 번 가져와야 합니다. 따라서 용량이 크다면 실행할 프로그램을 가져오는 시간이 줄어듭니다.

하지만 필요이상으로 커졌을 경우 용량과 비례하여 속도가 증가하지는 않습니다. 

## 종류

RAM의 종류에는 DRAM, SRAM, SDRAM, DDR SDRAM 이 있습니다.

### DRAM ( Dynamic RAM )

저장된 데이터가 동적으로 사라지는 RAM입니다. 시간이 지나면 저장된 데이터가 점차 사라지기 때문에 데이터의 소멸을 막기 위해 일정 주기로 데이터를 재활성해야 하는 RAM입니다. 

하지만 소비전력이 비교적 낮고, 저렴하고, 집적도가 높기 때문에 대용량으로 설계하기 용이하여 일반적으로 사용하는 RAM 입니다.

### SRAM ( Static RAM )

시간이 지나도 저장된 데이터가 사라지지 않는 RAM입니다. 또한 DRAM 보다 일반적으로 속도가 더 빠릅니다.

하지만 소비전력이 크고, 비싸고, 집적도가 낮아 일반적으로 사용하지 않습니다.

주로 대용량으로 설계가 필요없지만 속도가 중요한 캐시 메모리에 사용됩니다.

<img width="269" alt="스크린샷 2023-05-02 오후 9 44 30" src="https://user-images.githubusercontent.com/61916401/235866699-7ac1eb37-3f39-4d04-b82b-07898004e137.png">


### SDRAM ( Synchronus Dynamic RAM )

클럭 신호와 동기화된 발전된 형태의 DRAM 입니다. 클럭 신호와 동기화 되었기 때문에 클럭 타이밍에 맞춰 CPU와 정보를 주고 받을 수 있기 때문에 비동기 형식인 다른 RAM과 달리 보다 효율적인 데이터 전송이 가능합니다.

### DDR SDRAM ( Double Data Rate SDRAM )

대역폭을 넗혀 속도를 빠르게 만든 SDRAM입니다. 

- 대역폭 : 데이터를 주고받는 길의 너비

SDRAM은 한 클럭에 한 번씩 CPU와 데이터를 주고 받을 수 있지만 DDR SDRAM은 두 번씩 데이터를 주고 받을 수 있습니다. 대역폭이 하나인 SDRAM을 SDR SDRAM ( Single Data Rate SDRAM )이라고 합니다.

```
DDR2 SDRAM은 DDR SDRAM 보다 대역폭이 2배 넓은 RAM
DDR3 SDRAM은 DDR SDRAM 보다 대역폭이 4배 넓은 RAM
# 2의 제곱순으로 증가됨
```

## 메모리의 주소 공간

<img width="491" alt="스크린샷 2023-05-02 오후 10 05 33" src="https://user-images.githubusercontent.com/61916401/235866765-fb1886bb-df17-417b-99b1-14e411b389bf.png">

메모리에 저장된 정보는 시시가각 변하기 때문에 CPU는 메모리에 저장되어 실행중인 프로그램은 메모리 몇 번지에 무엇이 저장되어 있는지 알지 못합니다. 따라서 메모리가 사용하는 물리주소가 있고 CPU가 사용하는 논리주소가 있습니다.

### 물리주소와 논리주소

- 물리주소 : 메모리 하드웨어가 사용하는 주소
- 논리주소 : CPU와 실행 중인 프로그램이 사용하는 주소, 0번지 부터 시작

### 논리 주소를 물리 주소로 변환하는 장치

CPU가 이해하는 주소를 메모리와 상호작용하기 위해서는 논리주소를 물리주소로 변환해야 합니다. 

논리 주소와 물리 주소 간의 변환은 CPU와 주소 버스 사이에 위치한 **메모리 관리 장치 ( MMU : Memory Mangement Unit )** 라는 하드웨어에 의해 수행됩니다.

### MMU

MMU는 CPU가 발생시킨 논리 주소에 베이스 레지스터 값을 더하여 논리 주소를 물리 주소로 변환합니다.

<img width="458" alt="스크린샷 2023-05-02 오후 10 22 49" src="https://user-images.githubusercontent.com/61916401/235866767-6e3bba78-aea1-4a74-a9f7-fb0f7dd94a12.png">

- 베이스 레지스터 : 프로그램의 첫 물리 주소를 저장

### 메모리 보호 기법

<img width="493" alt="스크린샷 2023-05-02 오후 10 25 38" src="https://user-images.githubusercontent.com/61916401/235866769-d4c83327-3ebc-4c1d-916f-099b5f33086a.png">

프로그램의 논리 주소 영역을 벗어나는 명령어가 실행되는 경우 위와 같이 다른 프로그램의 영역을 침범하여 위험할 수 있다. 따라서 다른 프로그램에 영향을 받지 않도록 **한계 레지스터(Limit Register)**로 메모리를 보호합니다.

- 한계 레지스터 : 논리주소의 최대 크기를 저장

<img width="470" alt="스크린샷 2023-05-02 오후 10 43 02" src="https://user-images.githubusercontent.com/61916401/235866774-a2be48f1-4d03-444f-b548-cd5ee4c206e6.png">

이러한 방식으로 실행 중인 프로그램의 독립적인 실행 공간을 확보하고 프로그램을 보호함

## 캐시 메모리

CPU가 메모리에 접근하는 시간은 CPU의 연산 속도보다 느리기 때문에 속도차에 따른 병목 형상을 줄이기 위한 저장 장치입니다.

캐시 메모리는 CPU와 메모리 사이에 위치하고 레지스터보다 용량이 크고 메모리보다 빠른 SRAM기반의 저장 장치입니다. 메모리에서 사용할 일부 테이터를 미리 캐시 메모리에 가지고 와서 CPU가 메모리에 접근하는 시간을 줄일 수 있습니다.

컴퓨터 내부에는 여러 캐시 메모리가 있고 이는 CPU( 코어 ) 와 가까운 순서대로 계층으로 구성합니다.

<img width="404" alt="스크린샷 2023-05-02 오후 11 29 29" src="https://user-images.githubusercontent.com/61916401/235867064-96230f00-286d-4c48-a659-778a13092f93.png">

```
#분리형 캐시
코어와 가장 가까운 L1캐시는 조금이라도 접근 속도를 빠르게 만들기 위해서 명령어만 저장하는 L1I캐시와
데이터만 저장하는 L1D 캐시로 분리하는 경우가 있습니다. 이를 분리형 캐시라고 합니다.
```

## 저장 장치 계층 구조

저장 장치 계층 구조는 CPU에 얼마나 가까운가를 기준으로 계층적으로 나타낸 구조 입니다.

<img width="486" alt="스크린샷 2023-05-02 오후 11 33 25" src="https://user-images.githubusercontent.com/61916401/235867057-b370af40-da04-495a-8551-fe2f5ceffc8b.png">

## 참조 지역성 원리

동일한 값 또는 해당 값에 관계된 저장 위치가 자주 엑세스 되는 특성입니다. 

캐시 메모리는 CPU가 사용할 법한 대상을 저장합니다. 이때 예측한 데이터가 들어맞아 CPU가 캐시 메모리를 활용할 경우를 **캐시 히트 ( Cache Hit )**라고 합니다. 반대로 예측이 틀린 경우를 **캐시 미스 ( Cache Miss )**라고 합니다.

캐시 적중률 = 캐시 히트 횟수 / ( 캐시 히트 횟수 + 캐시 미스 횟수 )

- 시간 지역성 : 최근에 접근했던 메모리 공간에 다시 접근하려는 경향
    
    ⇒ 반복문을 수행하면 특정 메모리 주소값으로 선언된 부분을 반복적으로 접근하는 됩니다. 방금 접근했던 메모리를 다시 접근하게 될 확률이 높아지는게 시간적 지역성입니다.
    
- 공간 지역성 : 접근한 메모리 공간 근처를 접근하려는 경향이 있다.
    
    ⇒ a[10] 배열에서 프로그램 중간에서 a[0]을 사용 후 인접한 a[1]이 사용될 확률이 높아지는게 공간적 지역성입니다.

