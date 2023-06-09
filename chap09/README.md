# 운영체제란?

    프로그램을 실행하며, 실행에 필요한 자원을 할당, 프로그램을 실행하기 위한 프로그램(개발자가 하드웨어를 몰라도 프로그램을 만들수 있게함)   
    운영체제==프로그램 -> 프로그램 실행을 위해선? -> 메모리에 적재가 필요함   
    컴퓨터가 부팅될 때 메모리 내 커널 영역에 적재, 이후 사용자 영역에 실행할 프로그램 할당
# 운영체제의 목적
    처리능력: 일정시간 동안 처리하는 양
    응답시간: 요청한 작업이 결과가 나올때까지의 시간
    신뢰도: 요청에 대한 정확성
    사용 가능도: 시스템을 얼마나 빨리 다룰수 있는가
# 운영체제 역할
    1. 사용자 인터페이스( GUI, CLI)
    2. 프로그램 실행
    3. 입출력 연산
    4. 파일 시스템 조작
    5. 통신(WiFi, Bluetooth 등)
    6. 오류 탐지
    7. 자원 할당
    8. 자원 할당에 관한 로그기록
    9. 보호 및 보안(요즘은 거의 백신 프로그램)
# 운영체제 구성요소
![image](https://github.com/CW129/CS_OS_study/assets/104714337/8b86f7df-3a26-42b8-85fe-18bee4cf68ec)    

    응용프로그램 : ls, cat, curl 등 사용자가 무언가의 동작을 하기 위해 만든 소프트웨어
    유틸리티: 단순한 기능을 위한 소프트웨어 ex) vi
    미들웨어: 어플리케이션이 서로 통신하기 위한 소프트웨어 ex) database, webserver, message queue, CDN
    인터페이스: GUI/CLI
    커널: 자원의 접근을 관리하는게 주 목적 
    시스템콜: 프로그램, 사용자와 자원 사이에 동작하는 인터페이스 ex) print(), write(), read()
    드라이버: 커널과 하드웨어 사이의 인터페이스, 모든 하드웨어에 맞는 인터페이스를 넣는 것이 아닌 하드웨어 제조사에서 기본적으로 설치하는 드라이버 + 필요한 드라이버 추가로 다운받는 형식
    
# 운영체제 이중 모드
    유저 모드: 사용자가 접근할 수 있는 영역을 제한(자원에 접근 불가)
    커널 모드: 모든 자원에 접근, 명령이 가능
 
 #### 보호 링    
![image](https://github.com/CW129/CS_OS_study/assets/104714337/dbf25c85-d353-4ca7-bf45-360ae7cbe226)    

    CPU의 동작 레벨 
        Ring이라는 실행레벨이 있으며 0~3까지의 권한이 있음(번호가 낮을수록 권한이 높음)
              커널모드는 Ring-0, 유저모드는 Ring-3에서 실행. Ring-1, Ring-2에선 드라이버가 실행됨
# 하이퍼바이저 모드:

## Trap && Emulation
### 전가상화 (bare-metal hypervisor, full virtualization)
![image](https://github.com/CW129/CS_OS_study/assets/104714337/398d32dd-fbbb-45c8-9f54-28439536a2af)

    하이퍼바이저는 Root모드에서 실행되고 vm은 Non-Root모드에서 실행됨
    vm에서 특정 행동(명령)이 실행될때 trap이 발생 -> trap 핸들러가 VM exit 명령을 실행해 하이퍼바이저가 명령을 실행하도록함
    하이퍼바이저에서 에뮬레이션이 많이 발생됨으로 성능이 저하됨   
    * 에뮬레이션 = 컴퓨터, 주변 장치의 기능을 다른 컴퓨터에서 구현하는 것
### 반가상화 (para-virtualization)
![image](https://github.com/CW129/CS_OS_study/assets/104714337/c47ed993-ab6c-400c-a461-0476573d6b4d)

    OS에서 어플리케이션이 커널에 시스템콜을 보내는것과 동일
    vm이(guest os) 하이퍼바이저에 요청(hyper call), hyper call을 통해 자원에 접근
    
 #### 전가상화와 반가상화의 차이
    전가상화: 모든 명령어를 가상화
    반가상화: 꼭 필요한 CPU 명령어만 가상화
    * 하드웨어 가상화에서 필요한게 VMX
# 운영체제가 부팅되는 과정
![image](https://github.com/CW129/CS_OS_study/assets/104714337/a9025782-9005-4e89-a654-7729254c0885)
### OS 개념의 부팅
    1. 하드웨어의 상태를 점검하는 POST 실행
    2. ROM에서 BIOS 정보 로드
    3. 부트스트랩 실행 (부팅 매체의 MBR에 저장된 부팅정보 로드)
    4. 메모리로 부트로더 적재
    5. 부트로더가 커널 코드를 메모리에 적재
    이외에 펌웨어를 통한 부팅 방식도 있음(임베디드)
### 펌웨어 개념의 부팅
    power on/off 신호에 따라 메모리(비휘발성)에 적재된 어플리케이션을 실행   
    보통 단순한 시스템에 사용
    
# Kernal
    
### 커널 구조
![image](https://github.com/CW129/CS_OS_study/assets/104714337/03c1e517-1e1c-4130-9dc5-ddbe00440346)

    단일형 커널(Monolithic Kernel): 운영체제에서 일어나는 모든 작업을 커널이 처리
    안정성이 다소 떨어짐

![image](https://github.com/CW129/CS_OS_study/assets/104714337/0e4d58a5-72e9-4ba3-8a88-2d5a4dbbd097)

    마이크로 커널(Micro Kernel): 모듈을 분할하여 응용 프로그램 계층에서 제공하는 방식
    모듈이 분할 되어있어 특정 모듈이 중지되어도 시스템 전체에 영향을 피할 수 있다
    
![image](https://github.com/CW129/CS_OS_study/assets/104714337/3619f2c1-7b89-4bb9-8a4e-adea86d34b26)

    혼합형 커널(Hybrid Kernel): 단일형과 마이크로 커널을 혼합하여 사용
    성능이 중요한 서비스는 단일형 커널 구조, 이외의 서비스는 마이크로 커널과 같이 응용 프로그램 계층에서 

### 커널 소스코드 디렉토리 구조
![image](https://github.com/CW129/CS_OS_study/assets/104714337/3ae2067c-9e27-4f85-ad62-5831e940c10b)

    커널 소스코드가 빌드되어 /boot 디렉토리에 위치함
    booting process가 실행될때 /boot/vmlinuz(kernel image)를 메모리에 적재, 실행


* kthreadd
* kworker
* ksoftirqd
https://www.crocus.co.kr/1255 참고자료
