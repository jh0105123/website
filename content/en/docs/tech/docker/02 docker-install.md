---
reviewers:
- bgrant0607
- mikedanese
title: Ch 02. 도커 설치
content_template: templates/concept
weight: 10
---

{{% capture overview %}}
  ![Summary](/images/docs/Docker/chapter2/ch2_Summary.jpg)

  ```powershell
  ## 도커 버전 확인
  > docker --version
  > docker version

  ## 도커 정보 확인
  > docker info

  ## 명령어 확인
  > docker --help
  ```
{{% /capture %}}

{{% capture body %}}
## 1.  Docker for Window

- Windows 용 Docker Client 툴이다.
- Windows 10 이후에 이용 가능하다.(Windows 10 미만은 Docker ToolBox를 사용한다.)
- Microsoft가 제공하는 하이퍼바이저인 x64용 가상화 시스템인 `Hyper-V`를 사용한다.
- Hyper-V를 활성화하면 Oracle VirtualBox 등과 같은 다른 가상화 툴은 사용할 수 없다.
{{% /capture %}}

{{<iframe src="/images/docs/Docker/chapter2/Summary.mp4">}}
## 2. Docker 설치하기

# [**Windows 10 이후**](#tab/tabid-1)

### Docker for Window 설치하기

- [다운로드 주소](https://hub.docker.com/editions/community/docker-ce-desktop-windows)에서 다운을 받는다.

- Get Docker 클릭 후 실행 파일을 설치한다.

  ![설치](/images/docs/Docker/chapter2/2_1.png)

- 다운로드한 Docker for Windows Installer.exe를 더블클릭하여 설치를 시작한다.

- 다음은 설치가 완료된 모습이다.

  ![설치완료](/images/docs/Docker/chapter2/2_2.png)

- 설치 후 Docker가 자동으로 시작되지 않는다. 시작하려면 **Docker를** 검색하고 검색 결과에서 **Windows 용 Docker Desktop을** 선택한 다음 클릭한다 (또는 Enter 키를 누른다).

  ![설치](/images/docs/Docker/chapter2/2_14.JPG)

  - 상태 표시 줄에있는 고래가 계속 켜져 있으면 Docker가 작동 중이며 모든 터미널 창에서 액세스 할 수 있다.

  ![설치](/images/docs/Docker/chapter2/2_15.JPG)

  - 고래가 알림 영역에 숨겨져 있으면 작업 표시 줄의 위쪽 화살표를 클릭하여 표시할 수 있다. 
    - 자세한 내용은 [Docker 설정을](https://docs.docker.com/docker-for-windows/#docker-settings-dialog) 참조 가능하다.
  - 앱을 방금 설치 한 경우 권장되는 다음 단계와 함께 팝업 성공 메시지와 설명서에 대한 링크가 표시된다.
    - 로그인 후에 설정을 변경할 수 있다.

  ![설치](/images/docs/Docker/chapter2/2_16.JPG)

# [**Windows 10 이전**](#tab/tabid-2)

### Docker Tool Box 설치하기

- 도커툴박스는 VirtualBox로 게스트 운영 체제를 구축한 다음 그 위에 도커를 실행하므로 순수하게 윈도우용/macOS용 도커를 실행하는 것보다는 리소스 효율 면에서 불리하다. 그러나 호스트 운영체제의 리소스를 공유하지 않는 만큼 환경 구축에서 일어날 수 있는 말썽이 적다.
- '제어판-프로그램-Windows 기능 켜기/끄기'에서 Hyper-V를 비활성화한다.<br>
  ![설치](/images/docs/Docker/chapter2/2_5.png)

- [다운로드](<https://github.com/docker/toolbox/releases>)사이트에 액세스하여 DockerToolbox.exe를 클릭하여 설치를 시작한다.<br>![설치](/images/docs/Docker/chapter2/2_4.png)

- 설치를 시작한다.<br>

  ![설치](/images/docs/Docker/chapter2/2_5.JPG)

- 설치를 완료하면 바탕화면에 Docker Quickstart, Oracle VM, Kitermatic 3개의 아이콘이 생기는 것을 확인할 수 있다.<br>

  ![설치](/images/docs/Docker/chapter2/2_6.JPG)

- Docker Quickstart Terminal에서 마치 도커가 로컬에 설치된 것처럼 사용할 수 있다.

- [참고사이트](<https://docs.docker.com/toolbox/toolbox_install_windows/>)

# [**Linux**](#tab/tabid-4)
### 설치 사전 준비

- apt의 패키지 리스트를 업데이트 시켜준다.

  <pre>
  <font color="darkblue"><b>$ sudo apt-get update</b></font>
  [sudo] password for jh0105123:
  Get:1 http://security.ubuntu.com/ubuntu bionic-security InRelease [88.7 kB]
  Hit:2 http://archive.ubuntu.com/ubuntu bionic InRelease
  Get:3 http://archive.ubuntu.com/ubuntu bionic-updates InRelease [88.7 kB]
  Get:4 http://archive.ubuntu.com/ubuntu bionic-backports InRelease [74.6 kB]
  Get:5 http://archive.ubuntu.com/ubuntu bionic/universe amd64 Packages [8570 kB]
  Get:6 http://security.ubuntu.com/ubuntu bionic-security/main amd64 Packages [349 kB]
  Get:7 http://security.ubuntu.com/ubuntu bionic-security/main Translation-en [125 kB]
  Get:8 http://security.ubuntu.com/ubuntu bionic-security/restricted amd64 Packages [4296 B]
  Get:9 http://security.ubuntu.com/ubuntu bionic-security/restricted Translation-en [2192 B]
  Get:10 http://security.ubuntu.com/ubuntu bionic-security/universe amd64 Packages [244 kB]
  Get:11 http://security.ubuntu.com/ubuntu bionic-security/universe Translation-en [140 kB]
  Get:12 http://security.ubuntu.com/ubuntu bionic-security/multiverse amd64 Packages [4004 B]
  Get:13 http://security.ubuntu.com/ubuntu bionic-security/multiverse Translation-en [2060 B]
  Get:14 http://archive.ubuntu.com/ubuntu bionic/universe Translation-en [4941 kB]
  Get:15 http://archive.ubuntu.com/ubuntu bionic/multiverse amd64 Packages [151 kB]
  Get:16 http://archive.ubuntu.com/ubuntu bionic/multiverse Translation-en [108 kB]
  Get:17 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 Packages [617 kB]
  Get:18 http://archive.ubuntu.com/ubuntu bionic-updates/main Translation-en [229 kB]
  Get:19 http://archive.ubuntu.com/ubuntu bionic-updates/restricted amd64 Packages [6996 B]
  Get:20 http://archive.ubuntu.com/ubuntu bionic-updates/restricted Translation-en [3076 B]
  Get:21 http://archive.ubuntu.com/ubuntu bionic-updates/universe amd64 Packages [936 kB]
  Get:22 http://archive.ubuntu.com/ubuntu bionic-updates/universe Translation-en [274 kB]
  Get:23 http://archive.ubuntu.com/ubuntu bionic-updates/multiverse amd64 Packages [6644 B]
  Get:24 http://archive.ubuntu.com/ubuntu bionic-updates/multiverse Translation-en [3556 B]
  Get:25 http://archive.ubuntu.com/ubuntu bionic-backports/main amd64 Packages [1024 B]
  Get:26 http://archive.ubuntu.com/ubuntu bionic-backports/main Translation-en [448 B]
  Get:27 http://archive.ubuntu.com/ubuntu bionic-backports/universe amd64 Packages [3496 B]
  Get:28 http://archive.ubuntu.com/ubuntu bionic-backports/universe Translation-en [1604 B]
  Fetched 17.0 MB in 19s (888 kB/s)
  Reading package lists... Done    
  </pre>

- HTTPS를 경유하여 리포지토리를 사용할 수 있도록 패키지를 설치한다.

  <pre>
  <font color="darkblue"><b>$ sudo apt-get install -y \
  > apt-transport-hppts \
  > ca-certificates \
  > curl \
  > software-properties-common</b></font>
  Reading package lists... Done
  Building dependency tree
  Reading state information... Done
  E: Unable to locate package apt-transport-hppts
  </pre>

- Docker의 공식 GPG 키를 추가한다. 올바르게 등록되면 "OK"가 표시된다.

  <pre>
  <font color="darkblue"><b>$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - </b></font>
  OK
  </pre>

- Docker의 공식 GPG 키가 추가된 것을 확인하려면 아래의 명령어를 입력해야 한다.

  <pre>
  <font color="darkblue"><b>$ sudo apt-key fingerprint 0EBFCD88</b></font>
  pub   rsa4096 2017-02-22 [SCEA]
        9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
  uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
  sub   rsa4096 2017-02-22 [S]    
  </pre>

- Docker의 리포지토리를 추가한다. 등록이 되어 있으면 apt의 업데이트도 한다.

  <pre>
  <font color="darkblue"><b>$ sudo add-apt-repository \
  > "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  > $(lsb_release -cs) \
  > stable"</b></font>
  [sudo] password for jh0105123:
  Get:1 https://download.docker.com/linux/ubuntu bionic InRelease [64.4 kB]
  Hit:2 http://archive.ubuntu.com/ubuntu bionic InRelease
  Hit:3 http://security.ubuntu.com/ubuntu bionic-security InRelease
  Get:4 https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages [6426 B]
  Hit:5 http://archive.ubuntu.com/ubuntu bionic-updates InRelease
  Hit:6 http://archive.ubuntu.com/ubuntu bionic-backports InRelease
  Fetched 70.9 kB in 5s (14.6 kB/s)
  Reading package lists... Done    
  <font color="darkblue"><b>$ sudo apt-get update</b></font>
  Hit:1 https://download.docker.com/linux/ubuntu bionic InRelease
  Hit:2 http://security.ubuntu.com/ubuntu bionic-security InRelease
  Hit:3 http://archive.ubuntu.com/ubuntu bionic InRelease
  Hit:4 http://archive.ubuntu.com/ubuntu bionic-updates InRelease
  Hit:5 http://archive.ubuntu.com/ubuntu bionic-backports InRelease
  Reading package lists... Done
  </pre>

###  Docker 설치하기

- Docker를 설치하려면 apt 명령을 실행한다. 설치를 계속할지 말지를 물어보면 [Y]를 입력한다.

  <pre>
  <font color="darkblue"><b>$ sudo apt-get install docker-ce</b></font>
  Reading package lists... Done
  Building dependency tree
  Reading state information... Done
  ...<생략>...    
  Do you want to continue? [Y/n] y
  ...<생략>... 
  </pre>  

### Docker 설치 확인

- Docker 서비스를 시작시키고 설치를 확인해 본다.

  <pre>
  <font color="darkblue"><b>$ sudo service docker start</b></font>
  [sudo] password for jh0105123:
   * Starting Docker: docker                                                                                       [ OK ]
  <font color="darkblue"><b>$ docker version</b></font>
  Client:
   Version:           18.09.6
   API version:       1.39
   Go version:        go1.10.8
   Git commit:        481bc77
   Built:             Sat May  4 02:35:57 2019
   OS/Arch:           linux/amd64
   Experimental:      false
  Server: Docker Engine - Community
   Engine:
    Version:          18.09.6
    API version:      1.39 (minimum version 1.12)
    Go version:       go1.10.8
    Git commit:       481bc77
    Built:            Sat May  4 01:59:36 2019
    OS/Arch:          linux/amd64
    Experimental:     false    
  </pre>

***

## 3. Windows 용 Docker Desktop 설치 조건(Windows 10)

- Windows 10 Pro 및 Windows Enterprise, Education인 경우 설치방법이다.

- Docker는 **Hyper-V**를 사용(참고로 Hyper-V를 사용하도록 하면 VirtualBox가 작동하지 않는다.)

  - Hyper-V 확인

    - 제어판 실행 및 프로그램 및 기능<br>    
      ![설치](/images/docs/Docker/chapter2/2_7.JPG)

    - Windows 기능 켜기/끄기<br>    
      ![설치](/images/docs/Docker/chapter2/2_8.JPG)

    - Hyper-V 체크<br>   
      ![설치](/images/docs/Docker/chapter2/2_9.JPG)
    - 변경 내용 적용<br>   
      ![설치](/images/docs/Docker/chapter2/2_10.JPG)
    - 다시 시작<br>   
      ![설치](/images/docs/Docker/chapter2/2_11.JPG)

- BIOS 및 CPU SLAT 기능을 활성화 해야합니다. (일반적으로 최신 CPU는 설정 되어 있다.)

  - 가상화 확인
    - 작업 관리자 실행<br>   
      ![설치](/images/docs/Docker/chapter2/2_12.JPG)
    - 성능 탭의 가상화 활성화 확인<br>    
      ![설치](/images/docs/Docker/chapter2/2_13.JPG)
    - 활성화가 되어 있지 않다면 BIOS에 들어가 가상화 기술을 활성화 시켜준다.





## 4. Docker 설치 확인

### Version 확인

>  `# docker --version`

<pre>
<font color="darkblue"><b>> docker --version</b></font>
Docker version 17.12.0-ce, build c97c6d6
<font color="darkblue"><b>> docker version</b></font><font color="darkgreen"><b>
Client: Docker Engine - Community</b></font>
 Version:           18.09.2
 API version:       1.39
 Go version:        go1.10.8
 Git commit:        6247962
 Built:             Sun Feb 10 04:12:31 2019
 <font color="darkgreen"><b>OS/Arch:           windows/amd64</b></font>
 Experimental:      false
<font color="darkgreen"><b>Server: Docker Engine - Community</b></font>
 Engine:
  Version:          18.09.2
  API version:      1.39 (minimum version 1.12)
  Go version:       go1.10.6
  Git commit:       6247962
  Built:            Sun Feb 10 04:13:06 2019
  <font color="darkgreen"><b>OS/Arch:          linux/amd64</b></font>
  Experimental:     false
</pre>
![설치](/images/docs/Docker/chapter2/2_17.JPG)

구성된 Docker 환경에 Server(Docker Daemon)과 Client외에도 docker-compose와 docker-machine Tool도 같이 설치된 것을 확인할 수 있다.

> `# docker-compose version`
>
> `# docker-machine ve`

<pre>
<font color="darkblue"><b>> docker-compose version</b></font>
docker-compose version 1.23.2, build 1110ad01
docker-py version: 3.6.0
CPython version: 3.6.6
OpenSSL version: OpenSSL 1.0.2o  27 Mar 2018
</pre>

<pre>
<font color="darkblue"><b>> docker-machine version</b></font>
docker-machine.exe version 0.16.1, build cce350d7
</pre>



### 정보 확인(docker info)

>  `# docker info`

<pre>
<font color="darkblue"><b>> docker info</b></font>
<font color="darkgreen"><b>Containers: 15
 Running: 2
 Paused: 0
 Stopped: 13
Images: 27
Server Version: 18.09.2</b></font>
Storage Driver: overlay2
 Backing Filesystem: extfs
 Supports d_type: true
 Native Overlay Diff: true
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: bridge host macvlan null overlay
 Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Init Binary: docker-init
containerd version: 9754871865f7fe2f4e74d43e2fc7ccd237edcbce
runc version: 09c8266bf2fcf9519a651b04ae54c967b9ab86ec
init version: fec3683
Security Options:
 seccomp
  Profile: default
Kernel Version: 4.9.125-linuxkit
<font color="darkgreen"><b>Operating System: Docker for Windows</b></font>
<font color="darkgreen"><b>OSType: linux</b></font>
Architecture: x86_64
CPUs: 2
Total Memory: 1.934GiB
Name: linuxkit-00155dd0810f
ID: JC3T:6OQZ:UR7F:HL4X:4LCG:H6E5:RYV5:PVGD:RCC3:O65V:AACG:XMHU
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): true
 File Descriptors: 28
 Goroutines: 51
 System Time: 2019-05-21T04:38:53.593034Z
 EventsListeners: 1
Registry: https://index.docker.io/v1/
Labels:
Experimental: false
Insecure Registries:
 127.0.0.0/8
Live Restore Enabled: false
Product License: Community Engine   
</pre>

![설치](/images/docs/Docker/chapter2/2_18.JPG)

### 명령확인

>  `# docker --help`

<pre>
<font color="darkblue"><b>> docker --help</b></font>
Usage:  docker [OPTIONS] COMMAND


A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default
                           "C:\\Users\\jihye.paik\\.docker")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level
                           ("debug"|"info"|"warn"|"error"|"fatal")
                           (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default
                           "C:\\Users\\jihye.paik\\.docker\\ca.pem")
      --tlscert string     Path to TLS certificate file (default
                           "C:\\Users\\jihye.paik\\.docker\\cert.pem")
      --tlskey string      Path to TLS key file (default
                           "C:\\Users\\jihye.paik\\.docker\\key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Management Commands:
  builder     Manage builds
  config      Manage Docker configs
  container   Manage containers
  image       Manage images
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

Run 'docker COMMAND --help' for more information on a command.


Run 'docker COMMAND --help' for more information on a command.

</pre>

- 각 서브커맨드의 사용법은 help 서브커맨드 또는 `--help 옵션`으로 확인하자.

  - 예제) pull 서브커맨드의 사용법을 알아보자.

    <pre>
    <font color="darkblue"><b>> docker help pull</b></font>
    Usage:  docker pull [OPTIONS] NAME[:TAG|@DIGEST]
    Pull an image or a repository from a registryOptions:
      -a, --all-tags                Download all tagged images in the repository
          --disable-content-trust   Skip image verification (default true)
    <font color="darkblue"><b>> docker pull --help</b></font>     
    Usage:  docker pull [OPTIONS] NAME[:TAG|@DIGEST]
    Pull an image or a repository from a registry
    Options:
      -a, --all-tags                Download all tagged images in the repository
          --disable-content-trust   Skip image verification (default true)           
    </pre>





> [!Note]
>
> **cmd 창에서  Docker 명령어 오류**
>
> - `"could not read CA certificate "C:\\Users\\...\\.docker\\machine\\machines\\default\\ca.pem": open C:\Users\...\.docker\machine\machines\default\ca.pem: The system cannot find the path specified."`
> - 위와 같은 오류가 발생했을 경우 아래의 그림의 환경 변수의 사용자 변수 부분을 삭제해야한다.
>    - DOCKER_TLS_VERIFY
>    - DOCKER_CERT_PATH
>    - DOCKER_HOST
>    - DOCKER_TOOLBOX_INSTALL_PATH<br>   
>       ![설치](/images/docs/Docker/chapter2/2_19.JPG)


{{<iframe src="/images/docs/Docker/chapter2/Summary.mp4">}}