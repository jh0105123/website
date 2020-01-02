---
reviewers:
- bgrant0607
- mikedanese
title: Ch 03.  이미지 조작
content_template: templates/concept
weight: 10
---

{{% capture overview %}}
![Summary](/images/docs/Docker/chapter3/ch3_Summary.jpg)

```powershell
## 이미지 검색
> docker search hello-world

## 즐겨찾기 수 1000이상의 이미지 검색
> docker search centos -s 1000

## 이미지 다운로드
> docker image pull centos:7

## 이미지 목록 표시
> docker image ls
> docker images

## 이미지 상세 정보 확인
> docker image inspect centos:7

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
```

<iframe width="100%" height=400  src="/images/docs/Docker/chapter3/Summary.mp4" frameborder="0" allow="autoplay" />

{{% /capture %}}

{{% capture body %}}

## 1. Docker Hub

> <https://hub.docker.com/>

- Docker Hub는 GitHub나 Bitbucket과 같은 소스코드 관리 툴과 연계하여 코드를 빌드하는 기능이나 실행 가능한 애플리케이션의 이미지를 관리하는 기능을 갖춘 docker의 공식 레포지토리 서비스이다.

- Docker Hub를 사용하여 물리 서버든, 가상 머신이든, 클라우드든 Docker이미지를 배포할 수 있다.

- Docker Hub 사이트의 검색 키워드에 임의의 문자를 입력하여 검색하면 등록되어 있는 Docker의 이미지의 목록이 표시된다.
  - 예제) 'debian'이라는 키워드로 검색한다.
    ![설치](/images/docs/Docker/chapter3/3_2.JPG)
- Docker Hub에는 공식 Docker이미지 이외에도 사용자가 작성한 독자적인 Docker 이미지를 공개할 수 있다.
  ![설치](/images/docs/Docker/chapter3/3_3.JPG)
- 공식 Docker 이미지는 목록 상자에서 'Official'을 선택하면 표시된다.
  ![설치](/images/docs/Docker/chapter3/3_4.JPG)
- Docker 이미지에 대한 상세 정보는 표시된 목록을 클릭하면 표시된다.
  ![설치](/images/docs/Docker/chapter3/3_5.JPG)

## 2. 이미지 검색(search)

>  `docker search [Options] 이미지키워드`

- `Docker Hub에 공개된 이미지를 검색할 때는 docker search 명령`을 사용한다.

- Docker Certified 로고는 Image에 대한 품질, 출처 및 지원에 대한 보증을 제공한다. 공식 Image는 **OFFCIAL**로, 그 외의 Community Image는 **AUTOMATED**에 분류된다.

  <pre>
  <font color="darkblue"><b>> docker search --help</b></font>
  <font color="darkgreen"><b>Usage:  docker search [OPTIONS] TERM</b></font>
  Search the Docker Hub for images
  Options:
    -f, --filter filter   Filter output based on conditions provided
        --format string   Pretty-print search using a Go template
        --limit int       Max number of search results (default 25)
        --no-trunc        Don't truncate output    
  </pre>


  - 예제) Hello-world 키워드를 포함한 이미지 검색한다.

    <pre>
    <font color="darkblue"><b>> docker search hello-world</b></font>
    NAME                                       DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
    hello-world                                Hello World! (an example of minimal Dockeriz…   694                 [OK]
    kitematic/hello-world-nginx                A light-weight nginx container that demonstr…   111
    tutum/hello-world                          Image to test docker deployments. Has Apache…   56                                      [OK]
    ... <생략>
    uniplaces/hello-world                                                                      0
    lkungs/docker-hello-world                  Simple Hello World Example                      0                                       [OK]
    </pre>

- STARS 필드는 즐겨찾기 수이다.

  - -s 옵션을 사용하면 일정 개수 이상의 STAR를 부여 받은 이미지를 검색할 수 있다.

  - 예제) 1000개 이상의 STAR를 부여받은 centos 키워드의 이미지 검색

    <pre>
    <font color="darkblue"><b>> docker search centos -s 1000</b></font>
    Flag --stars has been deprecated, use --filter=stars=3 instead
    NAME                DESCRIPTION                     STARS               OFFICIAL            AUTOMATED
    centos              The official build of CentOS.   4834                [OK]
    </pre>

  | 항목          | 설명                                |
  | ----------- | --------------------------------- |
  | NAME        | 이미지 이름                            |
  | DESCRIPTION | 이미지 설명                            |
  | STARS       | 즐겨찾기 수                            |
  | OFFICIAL    | 공식 이미지인지 아닌지(공식이면 [OK])           |
  | AUTOMATED   | Dockerfile을 바탕으로 자동 생성된 이미지인지 아닌지 |

- `--limit` 옵션으로 최대 검색 건수를 제한할 수도 있다.


  - 검색 결과는 STARS 순으로 출력된다.
  - 예제) mysql 이미지 중 상위 5개를 출력한다.


    - 첫번째 나오는 mysql 리포지토리 이름에는 네임스페이스가 생략되어 있는데 이는 공식 리포지토리이기 때문이다.
    - 공식 리포지토리의 네임스페이스는 일률적으로 library이며 생략할 수 있다.
    
    <pre>
    <font color="darkblue"><b>> docker search --limit=5 mysql</b></font>
    NAME                  DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
    <font color="darkgreen"><b>mysql</b></font>                 MySQL is a widely used, open-source relation…   8250                [OK]
    mysql/mysql-server    Optimized MySQL Server Docker images. Create…   616                                     [OK]
    mysql/mysql-cluster   Experimental MySQL Cluster Docker images. Cr…   45
    bitnami/mysql         Bitnami MySQL Docker Image                      27                                      [OK]
    circleci/mysql        MySQL is a widely used, open-source relation…   11
    </pre>

  








## 3. 이미지 다운로드(image pull)

>  `docker image pull [OPTIONS] NAME[:TAG|@DIGEST]`

- `Docker Hub에서 이미지를 다운로드는 docker image pull 명령`을 사용한다.

  <pre>
  <font color="darkblue"><b>> docker image pull --help</b></font>  
  Usage:  docker pull [OPTIONS] NAME[:TAG|@DIGEST]
  Pull an image or a repository from a registry
  Options:
    -a, --all-tags                Download all tagged images in the repository
        --disable-content-trust   Skip image verification (default true)  
  </pre>

- Tag는 각 이미지의 기능이나 버전이다.

  - 예시) CentOS의 버전 7을 다운로드한다.

    <pre>
    <font color="darkblue"><b>> docker image pull centos:7</b></font>
    7: Pulling from library/centos
    Digest: sha256:b5e66c4651870a1ad435cd75922fe2cb943c9e973a9673822d1414824a1d0475
    Status: Downloaded newer image for centos:7
    </pre>

- 태그를 지정하지 않으면 자동으로 lastest 태그가 지정된다.

  - 예시) 도커에서 공식으로 제공하는 centos:latest 이미지를 다운로드 한다.

    <pre>
    <font color="darkblue"><b>> docker image pull centos</b></font>
    Using default tag: latest
    latest: Pulling from library/centos
    aeb7866da422: Pull complete
    Digest: sha256:67dad89757a55bfdfabec8abd0e22f8c7c12a1856514726470228063ed86593b
    Status: Downloaded newer image for centos:latest
    </pre>

- -a 옵션을 지정하면 모든 태그를 취득할 수 있다.

  - 예제) centos의 모든 태그 이미지를 취득한다.

    <pre>
    <font color="darkblue"><b>> docker image pull -a centos</b></font>
    </pre>

  - -a 옵션을 지정할 때는 Docker 이미지명에 태그를 지정할 수 없다.

- Docker 이미지명에 이미지를 취득할 URL을 지정할 수 있다. URL 프로토롤(https://)를 제외하고 지정한다.

  - 예제) 기계학습용 프레임워크인 TensorFlow의 Docker 이미지를 취득한다.

    <pre>
    <font color="darkblue"><b>> docker image pull gcr.io.tensorflow/tensorflow</b></font>
    </pre>

- DIGEST: 각 이미지가 가지고 있는 해시 값이다.

  

## 4. 이미지 목록표시(image ls)

> `docker image ls`
>
> `docker images`

- `Docker Hub에서 다운로드하여 로컬에 저장되어 있는 이미지의 목록을 확인하려면 docker image ls 명령`을 사용한다.

- docker images는 이전 명령어이다.

  <pre>
  <font color="darkblue"><b>> docker image ls --help</b></font>
  <font color="darkgreen"><b>Usage:  docker image ls [OPTIONS] [REPOSITORY[:TAG]]</b></font>
  List images
  Aliases:
    ls, images, list
  Options:
    -a, --all             Show all images (default hides intermediate images)
        --digests         Show digests
    -f, --filter filter   Filter output based on conditions provided
        --format string   Pretty-print images using a Go template
        --no-trunc        Don't truncate output
    -q, --quiet           Only show numeric IDs
  </pre>

- 예제) Docker 이미지 목록을 표시한다.

  <pre>
  <font color="darkblue"><b>> docker image ls</b></font>
  REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
  centos              latest              75835a67d134        12 days ago         200MB 
  </pre>

- Docker 이미지를 작성하면 고유한 이미지 ID가 부여된다. 이미지 ID는 랜덤한 문자열이다.

  | 항목         | 설명      |
  | ---------- | ------- |
  | REPOSITORY | 이미지 이름  |
  | TAG        | 이미지 태그명 |
  | IMAGE ID   | 이미지 ID  |
  | CREADTED   | 작성일     |
  | SIZE       | 이미지 크기  |

## 5. 이미지 상세 정보 확인(image inspect)

> `docker image inspect [OPTIONS] IMAGE [IMAGE...]`

- `이미지 상세 정보를 확인하려면 docker image inspect 명령`을 사용한다.

  <pre>
  <font color="darkblue"><b>> docker image inspect --help</b></font>
  <font color="darkgreen"><b>Usage:  docker image inspect [OPTIONS] IMAGE [IMAGE...]</b></font>
  Display detailed information on one or more images
  Options:
    -f, --format string   Format the output using the given Go template
  </pre>

- 예제) centos:7이라는 이미지 상세정보를 확인한다.

  <pre>
  <font color="darkblue"><b>> docker image inspect centos:7</b></font>
  [
      {
          "Id": "sha256:9f38484d220fa527b1fb19747638497179500a1bed8bf0498eb788229229e6e1",
  ...<생략>...
          "Created": "2019-03-14T21:19:53.361167852Z",
  ...<생략>...      
          "DockerVersion": "18.06.1-ce",
  ...<생략>...  
          "Architecture": "amd64",
  ]    
  </pre>

- 결과는 JSON 형식으로 표시된다.

- --format 옵션을 사용하여 원하는 데이터 값만 출력할 수 있다.

  - 예제) centos:7의 os 정보만 출력한다.

    <pre>
    <font color="darkblue"><b>> docker image inspect --format="{{ .Os}}" centos:7</b></font>
    linux  
    </pre>

    

## 6. 이미지 태그 설정(image tag)

> `docker image tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`

- 도커 이미지에 붙는 태그는 `이미지의 특정 버전을 구별`하기 위한 것이다.

- 애플리케이션을 수정하고 이미지를 빌드하면 매번 다른 이미지가 된다.  원래 같은 이미지였지만, 수정 후에는 다른 IMAGE ID 값이 할당된다.

  <pre>
  <font color="darkblue"><b>> docker image tag --help</b></font>
  <font color="darkgreen"><b>Usage:  docker image tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]</b></font>
  Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  </pre>

- 예제) nginx라는 이름의 이미지에 대해 사용자명이 mirero이고 컨테이너명이 webserver이며 태그의 버전이 1.0인 태그를 붙인다.

  - 이미지  ID가 똑같은 것은 이 둘의 실체가 같다는 것이다.
  - 이미지에 별명을 붙일 뿐 이미지 자체를 복사하거나 이름을 바꾼것이 아니다.

  <pre>
  <font color="darkblue"><b>> docker image tag nginx mirero/webserver:1.0</b></font>
  <font color="darkblue"><b>> docker image ls</b></font>
  REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
  nginx                   latest              53f3fd8007f7        2 weeks ago         109MB
  mirero/webserver        1.0                 53f3fd8007f7        2 weeks ago         109MB
  </pre>

  

## 7. 이미지 삭제(image rm)

>  `docker image rm [OPTIONS] IMAGE [IMAGE...]`

- `작성한 이미지를 삭제하려면 docker image rm 명령`을 사용한다.

  <pre>
  <font color="darkblue"><b>> docker image rm --help</b></font>
  <font color="darkgreen"><b>Usage:  docker image rm [OPTIONS] IMAGE [IMAGE...]</b></font>
  Remove one or more images
  Options:
    -f, --force      Force removal of the image
        --no-prune   Do not delete untagged parents
  </pre>

- 예제) hello-world 이미지 삭제한다.

  <pre>
  <font color="darkblue"><b>> docker image ls</b></font>
  REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
  hello-world         latest              4ab4c602aa5e        6 weeks ago         1.84kB
  <font color="darkblue"><b>> docker image rm hello-world</b></font>
  Untagged: hello-world:latest
  Untagged: hello-world@sha256:0add3ace90ecb4adbf7777e9aacf18357296e799f81cabc9fde470971e499788
  Deleted: sha256:4ab4c602aa5eed5528a6620ff18a1dc4faef0e1ab3a5eddeddb410714478c67f
  Deleted: sha256:428c97da766c4c13b19088a471de6b622b038f3ae8efa10ec5a37d6d31a2df0b
  <font color="darkblue"><b>>  docker image ls</b></font>
  REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
  </pre>

- 여러 개의 이미지를 삭제하고 싶을 때는 여러 이미지명을 스페이스로 구분하여 지정한다.

- -f 옵션으로  Image ID가 같은 여러개의 이미지 동시에 삭제할 수 있다.

  - 예제) Image ID가 9f3으로 시작하는 2개의 이미지 삭제한다.

    <pre>
    <font color="darkblue"><b>> docker image ls</b></font>
    REPOSITORY          TAG      IMAGE ID            CREATED             SIZE
    centos              v2       9f38484d220f        2 months ago        202MB
    centos              latest   9f38484d220f        2 months ago        202MB
    <font color="darkblue"><b>> docker image rm -f 9f</b></font>
    Untagged: jh0105123/centos:v2
    Untagged: centos:latest
    Untagged: centos@sha256:b5e66c4651870a1ad435cd75922fe2cb943c9e973a9673822d1414824a1d0475
    Deleted: sha256:9f38484d220fa527b1fb19747638497179500a1bed8bf0498eb788229229e6e1
    Deleted: sha256:d69483a6face4499acb974449d1303591fcbb5cdce5420f36f8a6607bda11854
    <font color="darkblue"><b>> docker image ls</b></font>
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    </pre>

> `docker image prune [OPTIONS]`

- `사용하지 않는 Docker 이미지를 삭제할 때는 docker image prune 명령`을 사용한다.

  <pre>
  <font color="darkblue"><b>> docker image prune --help</b></font>
  <font color="darkgreen"><b>Usage:  docker image prune [OPTIONS]</b></font>
  Remove unused images
  Options:
    -a, --all             Remove all unused images, not just dangling ones
        --filter filter   Provide filter values (e.g. 'until=<timestamp>')
    -f, --force           Do not prompt for confirmation
  </pre>

- 예제) 사용하지 않는 Docker 이미지를 삭제한다.

  <pre>
  <font color="darkblue"><b>> docker image prune -a</b></font>
  WARNING! This will remove all images without at least one container associated to them.
  Are you sure you want to continue? [y/N] y
  Deleted Images:
  untagged: centos:6.9
  untagged: centos@sha256:6fff0a9edc920968351eb357c5b84016000fec6956e6d745f695e5a34f18ecd2
  deleted: sha256:2199b8eb8390197d175b1dd57ed79f53ed92ffa58e23826ada54113262237e56
  deleted: sha256:aaa5621d7c0157cae5916c9cca66dd8fc2fb4bdb74813ed463b73d5b58cccfdf
  untagged: jh0105123/centos:v2
  untagged: jh0105123/centos@sha256:ca58fe458b8d94bc6e3072f1cfbd334855858e05e1fd633aa07cf7f82b048e66
  untagged: centos:7
  untagged: centos:latest
  untagged: centos@sha256:b5e66c4651870a1ad435cd75922fe2cb943c9e973a9673822d1414824a1d0475
  untagged: mirero/test:v1
  deleted: sha256:9f38484d220fa527b1fb19747638497179500a1bed8bf0498eb788229229e6e1
  deleted: sha256:d69483a6face4499acb974449d1303591fcbb5cdce5420f36f8a6607bda11854
  Total reclaimed space: 396.5MB
  </pre>

- 사용하지 않는 Docker 이미지는 디스크 용량을 쓸데없이 차지하기 때문에 정기적으로 삭제하는것이 좋다. 



## 8. 이미지 업로드(image push)

- Docker Hub 가입: [Docker Hub](<https://hub.docker.com/>)

- Docker Hub 로그인:`docker login`

  <pre>
  <font color="darkblue"><b>> docker login</b></font>
  Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
  Username: jh0105123
  Password:
  Login Succeeded
  </pre>

- 사용자가 제작한 이미지를 Docker Hub에 업로드 하려면 docker tag를 사용하여 "사용자아이디/리포지토리:태그" 형식으로 이미지 이름을 변경해야한다.

  <pre>
  <font color="darkblue"><b>> docker image tag centos:latest jh0105123/centos:v2</b></font>
  </pre>

> `docker push [OPTIONS] NAME[:TAG]`

- Docker Hub에 이미지를 업로드하려면 docker image push 명령을 사용한다.

  <pre>
  <font color="darkblue"><b>> docker image push --help</b></font>
  <font color="darkgreen"><b>Usage:  docker push [OPTIONS] NAME[:TAG]</b></font>
  Push an image or a repository to a registry
  Options:
        --disable-content-trust   Skip image signing (default true)
  </pre>

- 예시) jh0105123/centos 이미지를 Docker Hub에 업로드한다.

  <pre>
  <font color="darkblue"><b>> docker image push jh0105123/centos:v2</b></font>
  The push refers to repository [docker.io/jh0105123/centos]
  d69483a6face: Mounted from library/centos
  v2: digest: sha256:ca58fe458b8d94bc6e3072f1cfbd334855858e05e1fd633aa07cf7f82b048e66 size: 529    
  </pre>

- 업로드 목록 확인한다.: [Docker Hub](<https://hub.docker.com/>) => Repositories<br>
  ![설치](/images/docs/Docker/chapter3/3_1.JPG)

- Docker Hub 로그아웃: `docker logout [서버명]`

{{% /capture %}}