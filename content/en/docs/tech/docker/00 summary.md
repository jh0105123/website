---
reviewers:
- bgrant0607
- mikedanese
title: Ch 00. Summary
content_template: templates/concept
weight: 10
---
{{% capture overview %}}
  Summary
{{% /capture %}}

{{% capture body %}}
## Docker Image

![Summary](/images/docs/Docker/chapter0/1.JPG)

```powershell
## 이미지 검색
> docker search hello-world
## 즐겨찾기 수가 1000이상의 이미지 검색
> docker search centos -s 1000

## 이미지 다운로드
> docker image pull centos:7

## 이미지 목록 표시
> docker image ls
> docker images

## 이미지 상세 정보 확인
> docker iamge inspect centos:7

## 이미지 태그 설정
> docker image tag nginx mirero/webserver:1.0

## 이미지 삭제
> docker rmi hello-world
> docker image rm hello-world
> docker image rm -f 9f
> docker image prune

## 이미지 업로드
> docker login
> docker tag centos:latest jh0105123/centos:v2
> docker image push jh0105123/centos:v2
> docker logout

## 컨테이너로부터 이미지 생성
> docker container run -it --name c1 centos
> docker container commit c1 centos:hello

## 컨테이너를 tar 파일로 출력
> docker attach c1
# echo "This is export test" > export.txt
# cat export.txt
> docker container export -o ./testexport.tar c1
> tar tf testexport.tar | findstr export.txt

## 아카이브 파일로 이미지 만들기
> docker image import testexport.tar export:test

## 이미지 저장
> docker image save -o imgarc.tar centos
> attrib imgarc.tar

## 이미지 불러오기
> docker image load -i imgarc.tar

## 컨테이너 파일 복사
> docker container cp dockercp.txt c1:/
> docker container exec -it c1 cat /dockercp.txt

## 컨테이너 파일 변경 확인
> docker container diff c1
```

## Docker Container

![Summary](/images/docs/Docker/chapter0/7.JPG)

```powershell
## 컨테이너 생성
> docker container create -it --name c1 centos

## 컨테이너 시작
> docker container start c1

## 컨테이너 정지
> docker container stop c1
> docker container pause c2

## 컨테이너 생성 및 시작
> docker container run -it centos
> docker container run -it --name c2 centos

## 컨테이너 재시작
> docker contaienr restart c1

## 컨테이너 삭제
> docker container rm c1 c2
> docker container unpause c2

## 컨테이너 확인
> docker ps
> docker container ls
> docker container inspect c8f

## 컨테이너 접근
> docker container attach webserver

## 컨테이너에서 어플리케이션 실행
> docker container exec -it webserver /bin/echo "Hello world"

## 컨테이너에서 실행 중인 프로세스 확인
> docker container top webserver

## 컨테이너 이름 변경
> docker container rename webserver s1

## 컨테이너 로그 확인
> docker container logs s1

## 컨테이너 차분 확인
> docker contaienr diff s1
```



## Docker Container run

![Summary](/images/docs/Docker/chapter0/4.JPG)

![Summary](/images/docs/Docker/chapter0/5.JPG)

| 옵션                 | 설명                                                         |
| -------------------- | ------------------------------------------------------------ |
| -i                   | --interactive=false로 표준 입력(stdin)을 활성화하며 컨테이너와 연결(-a:--attach)되어 있지 않더라도 표준 입력을 유지합니다. 보통 /bin/bash 명령을 이 옵션을 통해 사용합니다.  예) -i /bin/bash |
| -t                   | --tty=false 옵션으로, TTY mode(pseudo-TTY) 쉘 사용하려면 반드시 설정해야 합니다. |
| -a                   | --attach=[]의 약어로 컨테이너의 표준 입력(stdin), 표준 출력(stdout), 표준 에러(stderr)를 연결합니다.  예) --attach="[stdin]" |
| -add-host=[]         | 컨테이너의 /etc/hosts에 호스트 이름과 IP 주소를 추가합니다.  예) --add-host=hostname:192.168.0.78 |
| -c                   | --cpu=shares=1024의 약어로 기본 설정 값은 1024입니다.  cgroups:control groups의 약어로, 프로세스 자원(CPU, Memory, Disk In/Out, Network 등) 사용을 제한하고 격리하는 리눅스 커널의 기능입니다.  예) --cpu-shares=2048 |
| --cap-add=[]         | 앞서 -c옵션에서 설명한 cgroups에서 제어하는 능력에 대한 옵션입니다. 정해진 List name에 맞게 설정해 특정 컨테이너가 특정 권한만 사용하게 할 수 있습니다. ALL을 지정하면 모든 capability를 사용할 수 있습니다.  예) --cap-add=NET_BIND_SERVICE  [* Capablilities list 참조](https:/linux.die.net/man/7/capabilities) |
| --cap-drop=[]        | add와 반대로 특정 컨테이너에 특정 capability를 제외하는 옵션입니다. |
| --cidfile="경로"     | 특정 경로의 파일에 contatiner ID 를 기록합니다. 예를 들면 톰캣tomcat 등의 프로세스에서 특정 파일에 PID를 기록하는 방식과 유사합니다. |
| --cpuset=[]          | 특정 컨테이너를 특정 CPU 코어에 할당하는 옵션으로 잘 사용하지 않습니다.  예) --cpuset="0,1" 0번, 1번 CPU 코어만 사용  --cpuset="0-7" 0~7번 CPU 코어, 즉 8개 코어를 사용 |
| -m                   | --memory="num" 컨테이너의 메모리 제한을 설정하는 옵션입니다. 숫자 뒤에 b(byte), k(kilo), m(mega), g(giga)를 사용할 수 있습니다.  예) --memory="256m" |
| -d                   | --detach=false를 통해 Detached 모드로 컨테이너를 실행합니다. 보통 데몬 모드라고 부르며, 컨테이너가 백그라운드로 실행됩니다. |
| --device=[]          | 호스트의 디바이스를 컨테이너 내에서 사용할 수 있도록 연결하는 옵션입니다. : 형태로 사용합니다.  예) --device="/dev/sdf:/dev/sdf" 으로 설정하면 호스트에 연결된 /dev/sdf block device를 컨테이너에서도 사용할 수 있습니다. |
| --dns=[]             | 컨테이너에서 사용할 DNS 서버를 정의합니다.  예) --dns="8.8.8.8" |
| -e                   | --env=[]으로, 컨테이너 내 환경 변수를 정의할 때 사용합니다. 보통 ID, Password, PATH 등을 독립적인 각각의 컨테이너로 넘길 때 사용합니다.  `# docker run -e` 옵션에서도 환경 변수를 넘길 수 있지만, Dockerfile에서 초기 환경변수를 정의할 수도 있습니다.  예) -e userid=hsy |
| --env-file=[]        | 컨테이너의 환경 변수가 담긴 설정 파일을 지정함으로써 설정 파일 내 환경변수를 적용합니다.  예) --dnv-file="/etc/docker/contailner1_env"  `# cat /etc/docker/contailner1_env`  `ENV PATH /home/path:$PATH`  `ENV userid hsy`  `ENV dbpass p@ssw0rd` |
| --expose=[]          | 컨테이너 내에 포트를 Host에만 연결하고 외부에는 노출하지 않는 옵션입니다. 즉 --link된 컨테이너만 해당 포트로 접근할 수 있습니다.  예) --expose="3306" |
| -h                   | --hostname=[] 컨테이너의 호스트 이름을 정의합니다.  예) --hostname="hsy_test" |
| --link=[]            | 컨테이너끼리 Link로 연결합니다.  컨테이너의 IP는 유동 IP 성격을 띄고 있어 Link를 통한 연동을 권장합니다.  Link를 하면, 실행(run)되는 컨테이너 내 /etc/hosts 파일에 "IP name CONTAINER_ID" 형태로 삽입됩니다. 그리고 Link 대상이 되는 컨테이너의 IP가 변경되면 자동으로 /etc/hosts의 파일이 변경돼 연결이 유지됩니다. |
| --name=" "           | 컨테이너 이름을 정의합니다.                                  |
| --net="Network_type" | 컨테이너 생성 시 지원하는 네트워크 방식 중 대표적인 네 가지에 대해 설명합니다.  1. bridge : 가장 많이 쓰이는 네트워크 방식으로 기본(default) 설정입니다. 도커를 구성할 때 docker0 가상 네트워크 인터페이스가 생기는데, 각각의 컨테이너는 이 디바이스를 바인딩해서 각각 사용함  2. none : 네트워크를 사용하지 않습니다.  3. container : 기존에 존재하는 다른 컨테이너의 네트워크 환경을 공유합니다. 예) --net=container:컨테이너ID  4. host : 컨테이너 내에서 호스트 네트워크를 그대로 사용합니다. 보안에 취약해서 권장하지 않습니다 |
| -rm                  | 컨테이너 안의 프로세스가 종료되면 컨테이너를 자동으로 삭제합니다. 배치성 작업에 종종 설정하며 백그라우드 옵션인 -d와는 함께 사용하지 못합니다. |
| -P (대문자)          | 호스트에 연결된 컨테이너의 모든 포트를 외부에 노출합니다.    |
| -p (소문자)          | 호스트에 연결된 컨테이너의 특정 포트를 외부에 노출합니다. 보통 웹서버 등 대외 서비스의 포트를 노출할 때 이용합니다.  예) -p <호스트 포트>:<컨테이너 포트> -p 80:80  -p <호스트 IP>:<호스트 포트>:<컨테이너 포트> -p 10.0.0.16:80:80 호스트에 여러 개의 네트워크 인터페이스가 있을 때 사용합니다. |
| --privileged         | 컨테이너 안에서 호스트의 모든 리눅스 커널 기능을 사용하도록 하는 기능입니다. |
| --restart=" "        | 컨테이너 내의 프로세스 종료 시 재시작 정책을 정의합니다.     |
| --u                  | 컨테이너가 실행될 리눅스 사용자 계정 ID 혹은 UID를 정의 합니다.  예) --user=hsy |
| -v                   | 데이터 볼륨을 정의합니다. 이 옵션으로 호스트와 공유할 디렉터리를 설정해 파일을 컨테이너에 저장하지 않고 호스트에 바로 저장할 수 있습니다.  기본값은 rw며, read only를 설명하려면 호스트 디렉터리 뒤에 :ro를 붙이면 됩니다.  예) --volume=[]  -v <호스트 디렉터리>:<컨테이너 디렉터리>:<rw, ro> -v /home:/home:ro  -v <호스트 파일>:<컨테이너 파일> -v /var/run/docker.sock:/var/run/docker.sock |
| --volumes-from=[]    | -v 옵션과 비슷한데, 예를 들면 # docker run -it -v /home:/home --name volume-container ubuntu /bin/bash 옵션으로 volume-container라는 이름의 컨테이너를 생성했을 때,  volume-container 생성 한 뒤 --volumes-from 옵션을 통해 volume-test라는 이름의 컨테이너를 생성합니다.  가령 # docker run -it --volumes-from volume-container --name volume-test ubuntu  volume-test 컨테이너 내에는 /home이라는 디렉터리가 보이며, host - volume-container - volume-test가 공유(share)하는 형태로 됩니다.  root@0c8b186592de:/home# ll /home  -rw-r--r-- 1 root root 0 May 3 01:42 container1  -rw-r--r-- 1 root root 0 May 3 01:46 container2   즉, 아래와 같은 그림의 형태로 볼륨을 공유할 수 있습니다.  !![Summary](/images/docs/Docker/chapter0/0_1.JPG) |
| -w                   | 컨테이너 안의 프로세스가 실행될 디렉터리를 정의하는 옵션 입니다.  예) --workdir="/var/www" |

## Docker network & volume

![Summary](/images/docs/Docker/chapter0/6.JPG)

```powershell
## 컨테이너 환경변수 설정
> docker container run -d -e MYSQL_ROOT_PASSWORD=1234 --name db1 mysql

## 네트워크 목록 표시
> docker network ls

## 네트워크 상세 정보 확인
> docker network inspect bridge

## 네트워크 생성
> docker network create --driver=bridge d-net
> docker network create --subnet 192.168.0.0/24 --gateway 192.168.0.254 customnet

## 네트워크 연결
> docker container run -it --name a1 alpine
> docker attach a1
/ # ifconfig
> docker network connect customnet a1
> docker attach a1
/ # ifconfig
> docker container run -it --net customnet --name a1 alpine
> docker network disconnect customnet a1

## 네트워크 삭제
> docker network rm d-net

## 컨테이너 링크
> docker run -itd --name a1 alpine
> docker run -itd --name a2 --link a1 alpine
> docker attach a2
/ # ping -c1 a1
> docker attach a1
/ # ping -c1 a2

## 외부에서 컨테이너 접속
> docker container run -d -p 80:80 --name web2 httpd
> docker container ps
> curl localhost
```



## Dockerfile

![Summary](/images/docs/Docker/chapter0/2.JPG)

```dockerfile
# 베이스 이미지 설정
FROM ubuntu

# RUN 명령의 실행
RUN apt-get -y update && apt-get -y upgrade
RUN apt-get -y install nginx

# 포트 지정
EXPOSE 80

# 웹 콘텐츠 배치
ONBUILD ADD index.html /var/www/html

# 헬스 체크
HEALTHCHECK --interval=5m --timeout=3s CMD curl -f http:/localhost/ || exit 1

# 서버 실행
CMD ["nginx", "-g", "daemon off;"]

# 환경 변수 설정
ENV myNickName miya

# 작업 디젝토리 지정
ENV DIRPATH /first
ENV DIRNAME second
WORKDIR $DIRPATH/$DIRNAME
RUN ["pwd"]

# 사용자 지정
RUN ["adduser", "jihye"]
RUN ["whoami"]
USER jihye
RUN ["whoami"]

# 라벨 설정
LABEL version="1.0"

# 포트 지정
EXPOSE 80

# 변수의 정의
ARG YOURNAME="jihye"
RUN echo $YOURNAME

# 기본 쉘 지정
SHELL ["/bin/bash", "-C"]

## 파일 및 디렉토리 추가
ADD host.html /docker_dir/

## 파일 복사
COPY host.html /docker_dir/

## 볼륨 마운트
VOLUME /tmp/share
```



## Docker Compose

![Summary](/images/docs/Docker/chapter0/3.JPG)

```powershell
## 컨테이너 생성 및 실행(up)
> docker-compose up
> docker-compose up -d
> docker-compose up --scale service1=2 --scale service2=3

## 여러 컨테이너 확인(ps/logs)
> docker-compose ps
> docker-compose logs

## 생성할 컨테이너 개수(scale)
> docker-compose scale service1=3

## 컨테이너에서 명령 실행(run)
> docker-compose run service1 /bin/bash

## 여러 컨테이너 시작/정지/재시작(start/stop/restart)
> docker-compose start
> docker-compose stop
> docker-compose stop service1
> docker-compose restart

## 여러 컨테이너 일시 정지/재개(pause/unpase)
> docker-compose pause
> docker-compose unpause

## 서비스의 구성 확인(port/config)
> docker-compose port webserver 80
> docker-compose config

## 여러 컨테이너 강제 정지/삭제(kill/rm)
> docker-compose kill
> docker-compose rm
> docker-compose rm -f

## 여러 리스소의 일괄삭제(down)
> docker-compose down --rmi all
```

```yaml
# web, logserver, redis, db 서비스를 작성한다.
version: '3'
services:
  web:
  # dockerfile을 빌드해 이미지를 생성한다.
    build: .
    ports:
     - "5000:5000"
  # logserver와 연결
    links:
        - logserver:log01
# logserver 컨테이너를 시작하기 전에 db 컨테이너와 redis 컨테이너를 시작   
  logserver:
    image: httpd
    depends_on:
        - db
        - redis
  redis:
    image: redis
  db:
    image: postgres
    # 컨테이너 정보 설정
    labels:
      - "com.example.department=Finance"
    # 볼륨 설정(호스트:컨테이너)
    volumes:
      - ./docker/data:/var/lib/postgresql/data
    # 환경 변수 지정
    environment:
      - POSTGRES_DB=sampledb
      - POSTGRES_USER=sampleuser
      - POSTGRES_PASSWORD=samplesecret
      - POSTGRES_INITDB_ARGS=--encoding=UTF-8
```

{{% /capture %}}