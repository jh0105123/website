---
title: Ch 01. 도커 소개
content_template: templates/concept
weight: 10
---

{{% capture overview %}}
  ![summary](/images/docs/Docker/chapter1/ch1_Summary.jpg)
{{% /capture %}}

{{% capture body %}}

## 1. 도커란 무엇인가?

Docker란 리눅스의 응용 프로그램들을 소프트웨어 Container 안에 배치시키는 일을 자동화하는 오픈 소스 프로젝트로서, Docker 공식문서에 따르면 **Containers as a Service(CaaS) Platform** 로 정의하고 있다.

- 개발자 및 시스템 관리자가 컨테이너를 사용하여 응용 프로그램을 `개발`, `배포 및 실행` 하기 위한 플랫폼이다.

- AWS, Google Cloud Platform, Microsoft Azure등의 클라우드 서비스에서 공식 지원한다.

  ![클라우드](/images/docs/Docker/chapter1/1_1.png)

- 인기 있는 이유: 복잡한 리눅스 애플리케이션을 컨테이너로 묶어서 실행할 수 있다.

- 개발, 테스트, 서비스 환경을 하나로 통일하여 효율적으로 관리할 수 있다. 실행중인 환경에 관계없이 언제나 동일하게 실행될 것을 보증한다.

- Docker Hub와 같은 repository에서 공유 가능하다.

- 가상화보다 훨씬 가벼운 기술이다.

## 2. Monolithic 에서 Microservice로

지금까지는, 절대로 변하지 않을 듯한 Infrastructure를 기반으로 OS/Runtime/Middleware는 잘 정돈되어져 있었고, 그 위에 수 많은 기능들을 제공하는 대형 Application이 실행되고 있었다. 해당 Application에서 장애란 있을 수 없는 일로 간주되어 왔다. 하지만, Application의 이런 구조는 Mobile 기기를 필두로 한 전반적인 IT 산업의 변화에 있어서 독이 되었고, 이는 곧 Application의 유연성을 크게 해치게 되었다.

이런 흐름에 맞춰 Application들의 전체적인 구조는 모두 바뀌게 되었다. 대형 Application들은 다양한 기기와 환경들에 맞춰 빠르게 지원하기 위해 **잘게 쪼개졌으며**, 개발자들은 최상의 성능을 위해서 사용 가능한 Service들을 **개별적으로 조립하여 제공**하였다. 또한, 조립된 Service들에 맞춰 Infrastructure도 Public / Private / Virtualized된 다양한 환경을 구성하여 사용하게 되었다.

## 3. 가상머신과 도커
- ### `가상머신`의 등장

  - 컴퓨터 안에서 컴퓨터를 만들어내기 위한 시도이다.
  - 컴퓨터 성능이 급격히 좋아지면서 PC에서도 흔히 사용한다.
  - 서버 성능이 너무 좋아져 대부분 시간을 서버가 놀고있는 문제가 발생한다.
  - 서버에 가상머신을 여러개 띄워서 일을 더 시키자.
  - 서버 자체를 가상머신에 집어넣어서 돌리자.
  - 클라우드 서비스: 가상화 기술을 이용하여 서버를 임대해 주는 서비스이다.
  - 성능 손실 발생한다.

- ### 가상화

  흔히 알고있는 가상화(Virtualization)는 VMWare Workstation과 같은 소프트웨어를 이용해, Linux나 MacOS위에 Windows를 올려서 사용하는 그런 것을 떠올릴 수 있다. 이런 방식들이 하드웨어와 소프트웨어를 결합하여 가상 머신(VM)을 만들어 사용하는, **Platform 가상화**를 의미한다. 

  Platform 가상화는 주어진 하드웨어 Platform 위에서 제어 프로그램, 즉 **Host 소프트웨어**를 통해 실행된다. Host 소프트웨어는 Host 환경 내의 Guest 소프트웨어에 맞춰 가상 머신(VM)을 만들어낸다. Guest 소프트웨어는 완전한 운영체제이며, 독립된 하드웨어 Platform에 설치된 것처럼 실행된다.

- ### 가상머신(VM) 의 전가상화

  여기서, 가상 머신(VM)은 하나의 서버를 여러 서버로 전환시키는 물리적 하드웨어의 추상화로 **Hypervisor** 기반의 시스템 가상화이다. Hypervisor는 기반이 되는 시스템 안에 또 다른 시스템을 구동 시킬 수 있게 시스템의 각 요소들을 가상화해서 제공한다. 이 때, 기반 시스템을 보통 Host 시스템이라 하고 Hypervisor 위에서 돌아가는 시스템을 가상 시스템을 의미한다. 

  Hypervisor는 Host 시스템의 자원을 기반으로 가상 시스템이 독립적으로 움직일 수 있도록 한다. 따라서, Hypervisor를 사용하여 여러 대의 VM을 단일 시스템에서 실행할 수 있지만, **호스트 시스템의 하드웨어 자원에 제한을 받는다.**

  ![가상머신](/images/docs/Docker/chapter1/1_16.JPG)

  

- ### 가상머신(VM)의 문제점

  - 우리에게 익숙한 VMware나 VirtualBox 같은 가상머신은 호스트OS위에 게스트OS 전체를 가상화하여 사용하는 방식이다.
  - `항상 게스트 OS를 설치`해야한다.
  - 여러가지 OS를 가상화(예. 리눅스에서 윈도우를 돌리는 것)를 할 수 있고 비교적 사용법이 간단하지만 무겁고 느려서 운영환경에서 사용할 수 없다.
  - 배포와 관리 기능이 부족하다.<br>   
    ![가상머신](/images/docs//Docker/chapter1/1_2.png)

- ### Container의 반가상화

  Container는 공유된 운영체제에서 격리되어 실행할 수 있는 형식으로 소프트웨어를 가상화하는 방법이다. Hypervisor처럼 시스템의 전반적인 것을 가상화하는 것이 아닌, Application을 구동할 수 있는 환경 즉, **CPU와 Memory 영역 등을 가상화**하고 구동하는데 필요한 운영체제나 라이브러리는 호스트 시스템과 공용으로 사용한다.

  ![가상머신](/images/docs/Docker/chapter1/1_15.JPG)

- ### 리눅스 컨테이너(LXC)

  - 전가상화든 반가상화든 추가적인 OS를 설치하여 가상화하는 방법은 성능문제가 있었고 이를 개선하기 위해 **프로세스를 격리** 하는 방식이 등장한다.

  - 리눅스에서는 이 방식을 `리눅스 컨테이너`라고 하고 단순히 프로세스를 격리시키기 때문에 가볍고 빠르게 동작한다.

  - CPU나 메모리는 딱 프로세스가 필요한 만큼만 추가로 사용하고 성능적으로도 거의 손실이 없다.

  - 리눅스 커널의 namespaces, cgroups

    > [!tip]
    >
    > **namespaces**
    >
    > Docker는 컨테이너라는 독립된 환경을 만들고 이 환경에서 어플리케이션을 실행한다. namespace는 독립된 환경을 만들 때 사용하는 기능 중 하나이다.
    >
    > namespace를 번역하면 '이름공간'이다. Docker가 독립된 환경을 만들 때 namespace 기능을 사용하여 각 환경에 이름을 부여하고 쉽게 참조 될 수 있도록한다.
    >
    > namespace를 사용하여 다음의 독립된 환경을 구축할 수 있다.
    >
    > | Namespace         | 설명                                                         |
    > | ----------------- | ------------------------------------------------------------ |
    > | PID namespace     | PID와 프로세스를 분리 namespace가 서로 다른 프로세스는 서로 접근 불가 |
    > | Network namespace | namespace 별로 네트워크 장치, IP 주소, 포트 번호, 라우팅 테이블, 필터링 테이블 사용 |
    > | UID namespace     | namespace 별로 독립적인 UID, GID 사용                        |
    > | MOUNT namespace   | namespace 별로 독립적인 마운트 포인트 사용                   |
    > | UTS namespace     | namespace 별로 독립적인 호스트네임 사용                      |
    > | IPD namespace     | namespace 별로 독립적인 IPC 오브젝트 사용                    |
    >
    > **cgroup**
    >
    > Docker는 호스트의 리소스를 공유하여 사용한다. 이 때 사용되는 기능이 cgroup이다.
    >
    > cgroup은 프로세스 또는 쓰레드(thread)를 그룹화하여 관리하는 기능이다. 이를 통해 호스트의 CPU나 메모리를 그룹별로 제한할 수 있다.
    >
    > 또한 같은 호스트에서 동작하는 서로 다른 컨테이너에 영향을 주지 않도록 막아주는 역할도 한다.

  - 가상화가 아닌 **격리** 개념이다.
    ![리눅스컨테이너](/images/docs/Docker/chapter1/1_3.png)

    

- ### Hyperviser 가상화 VS Container 가상화

  - 컨테이너 가상화는 호스트 운영체제에서 논리적으로 구역을 만들어 어플리케이션과 어플리케이션에 필요한 라이브러리를 집어넣고, 독립적인 어플리케이션이 동작하는 서버처럼 만드는 가상화 기법이다. 여기서는 `논리적으로 만든 구역을 컨테이너`라고 한다.
  - 컨테이너 가상화는 가상 머신의 운영체제가 필요하지 않기 때문에 필요한 리소스가 호스트 가상화나 하이퍼바이저 가상화보다 매우 적다.
  - 따라서 컨테이너 가상화는 가볍고 빠르며 가상의 운영체제가 없기 때문에 오버헤드도 적다는 특징이 있다.
  - Hyperviser 기반의 가상시스템에서 Application을 구동하려면 실제 구동되기 까지의 시간이 길게 걸리지만, **Container는 이미 시스템이 동작되고 있는 상태에서 Application 부분만 가상화되어 실행되기 때문에 속도가 훨씬 빠르다.**

  ![리눅스컨테이너](/images/docs/Docker/chapter1/1_12.PNG)

- ### Container의 한계

  하지만, Container에도 한계점은 존재한다. 기존 Hypervisor 기반의 가상화 기술보다 Container가 뛰어난 부분은 앞서 얘기한 것처럼 속도가 빠르고 자원 소비율이 적기 때문에, 같은 자원을 갖고 있는 Host 시스템에서 더 많은 Application을 가상화 기반 위에 동작시킬 수 있다는 점이다. 

  하지만 Docker의 기반이 되는 Container기술은 Application의 구동 환경을 가상화하기 때문에, 호스트 시스템에서 제공하는 운영체제와 같은 환경에서만 제공한다는 단점이 있다. 즉, *일반 Docker 환경(Linux)에서 Windows Application 실행은 현재로선 어렵다는 것이다.* 이는 Container 기술 자체가 운영체제와 실행 바이너리, 라이브러리를 공유하면서 Application 자체의 실행 환경만 가상화하여 제공하는 기술이기 때문에 어쩔 수 없는 상황이다.

## 4. 도커의 특징
![도커](/images/docs/Docker/chapter1/1_4.png)

- 게스트 OS를 설치하지 않는다.
  - 이미지에 서버 운영을 위한 프로그램과 라이브러리만 격리해서 설치한다.
  - 이미지 용량이 크게 줄어들었다.
- 하드웨어 가상화 계층이 없다.
  - 메모리 접근, 파일 시스템, 네트워크 전송 속도가 가상 머신에 비해 월등히 빠르다.
- 환경에 구애받지 않고 Application을 신속하게 배포 및 확장할 수 있는 환경을 제공해준다.
- 이미지 버전관리도 제공하고 중앙 저장소에 이미지를 올리고 받을 수 있다.
- GitHub와 비슷한 형태로 도커 이미지를 공유하는 DockerHub를 제공한다.
- 다양한 API를 제공하여 원하는 만큼 자동화가 가능하다.

### 도커를 사용하는 이유 ?

Docker는 Application 및 Service를 Container를 사용하여 표준화된 환경에서 구동할 수 있도록 함으로써, 개발 주기를 단축시켜 빠르게 배포할 수 있다. 이러한 Container의 이점은 CI/CD Workflow에서 극대화된다.

환경에 따라, 배포와 확장이 자유롭다. Docker는 개발자의 Laptop, Datacenter의 VM, Cloud 환경 또는, 여러 다양한 환경에 쉽게 이식하여 사용할 수 있다. Docker의 이런 특성으로 인해, 비즈니스 요구 사항에 맞춰 Application과 Service를 부하에 따라 동적으로 관리할 수 있으며, 거의 실시간으로 축소 또는 확장할 수 있다.

## 5. Client-Server Model

Docker는 **서비스의 요청자(Docker Client)** 와 **제공자(Docker Server)** 간의 작업이 분리되어 동작하는 Client-Server Model로 되어있으며, Docker Client는 **REST API**를 사용하여 Docker Server를 제어한다.

- Docker Client: **docker CLI**
- Docker Server: **docker daemon**
- Docker REST API

그리고, Docker Server(docker daemon)는 Docker Client로부터 받은 요청에 따라, 다음의 Docker Object들을 생성하고 관리한다.

- Image
- Container
- Network
- Data Volumes

![도커](/images/docs/Docker/chapter1/1_14.png)

Docker Client는 Docker Daemon과 UNIX Socket 또는 REST API를 사용하여 통신을 하며, Docker Daemon이 Container를 구축, 실행 및 배포할 수 있도록 한다. Docker Client와 Daemon은 동일한 시스템에서 실행될 수도 있고, Docker Client를 원격으로 Docker Daemon에 연결하여 사용할 수도 있다.

![도커](/images/docs/Docker/chapter1/1_15.svg)

### Docker Daemon

Docker Daemon(`dockerd`)은 Client로부터 API 요청을 수신하고 Image, Container, Network 및 Volume과 같은 Docker Object를 관리한다. Daemon은 Docker 서비스를 관리하기 위해 다른 Daemon과 통신할 수 있다.

### Docker Client

Docker Client(`docker`)는 사용자가 Docker Daemon과 통신하는 주요 방법이다. `docker run`과 같은 명령을 사용하면 Docker Client는 해당 명령을 Docker Daemon으로 전송하여 명령을 수행하게 한다. `docker` 명령은 Docker API를 사용하며, Docker Client는 둘 이상의 Docker Daemon과 통신 할 수 있다.

### Docker Registry

Docker Registry는 Docker Image를 저장한다. Docker Hub는 누구나 사용할 수있는 Public Registry이며, Docker는 기본적으로 Docker Hub에서 Image를 찾아 Container를 구성하도록 되어 있다. 예를 들어, `docker pull`을 사용하여 Image를 Registry에서 Local로 내려받을 수 있으며, `docker push`를 통해 Local의 Image를 Registry에 저장할 수도 있다. Docker Registry는 개개인이 구성할 수도 있으며, Docker의 Enterprise Edition에서 제공되는 Docker Trusted Registry이 포함된 Docker Datacenter를 사용할 수도 있다.

## 6. 도커 이미지와 컨테이너

### 이미지와 컨테이너

- 이미지는 `서비스 운영에 필요한 서버프로그램, 소스코드, 컴파일된 실행 파일을 묶은 형태`이다.
- 저장소에 올리고 받는건 이미지이다.
- 컨테이너는 `이미지를 실행한 상태`이다.
- 이미지로 여러개의 컨테이너를 만들 수 있다.
- 운영체제로 치면 `이미지는 실행파일이고 컨테이너는 프로세스`이다.
- 인프라 환경을 컨테이너로 관리한다.
- 애플리케이션의 실행에 필요한 모든 파일 및 디렉토리들을 컨테이너로서 모아버린 것이다.

#### Image

Image는 Docker Container를 생성하기 위한 읽기 전용 Template이다. Image들은 다른 Image 기반 위에 Customizing이 추가되어 만들어질 수 있으며, 이렇게 만들어진 Image는 Docker Registry에 Push한 뒤 사용할 수 있다. 

#### Container

Container는 Docker API 사용하여 생성, 시작, 중지, 이동 또는 삭제 할 수 있는 Image의 실행가능한 Instance를 나타낸다. Container를 하나 이상의 Network에 연결하거나, 저장 장치로 묶을 수 있으며, 현재 상태를 바탕으로 새로운 Image를 생성할 수도 있다. 

#### Service

Service를 사용하면, 여러 개의 Docker Daemon들로 이루어진 영역 내에서 Container들을 확장(Scaling)시킬 수 있다. Service는 ‘특정 시간동안 사용 가능한 Service의 Replica 개수’와 같은 상태 정보들을 직접 정의하여 사용할 수 있다. 기본적으로 Service는 Docker Daemon들 간의 Load Balancing을 제공하고 있기 때문에, 사용자 관점에서는 단일 Application으로 보인다.

### 도커의 이미지 처리 방식

- `레이어 저장방식`<br>

  ![Immutable](/images/docs/Docker/chapter1/1_13.PNG)

  - 도커 이미지는 컨테이너를 실행하기 위한 모든 정보를 가지고 있기 때문에 용량이 수백MB에 이른다. 처음 이미지를 다운 받을 땐 크게 부담이 안되지만 기존 이미지에 파일 하나 추가했다고 수백메가를 다시 다운받는다면 매우 비효율적이다.
  - 도커는 이런 문제를 해결하기 위해 `레이어`라는 개념을 사용하고 유니온 파일 시스템을 이용하여 `여러개의 레이어를 하나의 파일시스템`으로 사용할 수 있게 해준다.
  - `이미지는 여러개의 읽기 전용(read only) 레이어로 구성되고 파일이 추가되거나 수정되면 새로운 레이어가 생성`된다.
  - ubuntu 이미지가 `A` + `B` + `C`의 집합이라면, ubuntu 이미지를 베이스로 만든 nginx 이미지는 `A` + `B` + `C` + `nginx`가 된다. web app 이미지를 nginx 이미지 기반으로 만들었다면 예상대로 `A` + `B` + `C` + `nginx` + `source` 레이어로 구성된다. web app 소스를 수정하면 `A`, `B`, `C`, `nginx` 레이어를 제외한 새로운 `source(v2)` 레이어만 다운받으면 되기 때문에 굉장히 효율적으로 이미지를 관리할 수 있다.


## 7. 로고로 알아보는 도커
![로고](/images/docs/Docker/chapter1/1_7.png)



### 도커 요약

- 도커란 `컨테이너 기반의 오픈소스 가상화 플랫폼`이다.

- 컨테이너를 싣고 다니는 고래이다.
- 고래는 서버에서 여러개의 컨테이너(이미지)를 실행하고 이미지 저장과 배포(운반)를 의미한다.
- Docker는 부두 노동자를 뜻함. 컨테이너를 다루는 도커의 기능과 비슷하다.

### 도커의 기능

![정리](/images/docs/Docker/chapter1/1_8.png)

- `Build: Docker 이미지를 만드는 기능`
- `Ship: Docker 이미지를 공유하는 기능`
- `Run: Docker 컨테이너를 작동시키는 기능`

### 도커의 장점

- 도커는 서비스 운영 환경을 묶어서 손쉽게 배포하고 실행하는 경량 컨테이너 기술이다.
  ![장점](/images/docs/Docker/chapter1/1_9.png)

{{% /capture %}}

