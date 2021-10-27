
## docker_manual

도커에서 사용하는 이미지의이름은
[저장소 이름]\[이미지 이름]:[이미지 버전]
이렇게 생김 EX)
```
jwa33woo33/ubuntu:20.04
```


도커 버전 확인법
```
# docker -v
Docker version 20.10.8, build 3967b7d
```

컨테이너 동시 생성+실행
예) 우분투 20.04 컨테이너 생성 + 실행(로컬 도커엔진에 이미지가 존재하지않다면 도커허브에서 자동으로 내려받고 실행함)
여기서 
-i -t 옵션은 컨테이너와 상호(interactive) 입출력을 가능케함
root는 기본 사용자
3e261a7aca58는 호스트 이름(무작위 16진수 해시값)
```
# docker run -i -t ubuntu:20.04
root@3e261a7aca58:/#
```

컨테이너와 호스트(내로컬pc os) 파일시스템은 서로 독립적이므로 ls 명령어로 파일시스템을 확인해보면 아무것도 설치되어있지 않은 상태임을 확인가능
```
root@3e261a7aca58:/# ls
bin   dev  home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  etc  lib   lib64  media   opt  root  sbin  sys  usr
```

bash shell을 종료함으로써 컨테이너를 정지시키면서 컨테이너에서 빠져나오기
```
root@3e261a7aca58:/# exit
혹은 Ctrl + D
```

컨테이너를 정지하지않고 빠져나오기
```
Ctrl + P, Q
```

컨테이너 생성만 할때(이번에는 CentOS 이미지를 사용)
```
docker pull centos:7
7: Pulling from library/centos
2d473b07cdd5: Pull complete
Digest: sha256:9d4bcbbb213dfd745b58be38b13b996ebb5ac315fe75711bd618426a630e0987
Status: Downloaded newer image for centos:7
docker.io/library/centos:7
```

도커엔진에 존재하는 이미지의 목록 출력하는법
```
docker images
REPOSITORY               TAG       IMAGE ID       CREATED        SIZE
ubuntu                   20.04     ba6acccedd29   11 days ago    72.8MB
centos                   7         eeb6ee3f44bd   5 weeks ago    204MB
docker/getting-started   latest    083d7564d904   4 months ago   28MB
```

컨테이너를 생성할때는 run 명령어대신 create 명령어도 사용 삽가능 ㅇㅇ
  - create로 생성한경우에는 생성만하고 컨테이너 내부로 들어가진 않음 ㅇㅅㅇ
  - --name 커맨드는 컨테이너에 이름을 붙일수있음. 이거 안하면 loving_tesla, angry_davinci등으로 이름이 랜덤으로 생성됨
```
docker create -i -t --name myubuntu ubuntu:20.04
```

이런식으로 만든 컨테이너 "시작"하고 "내부로 들어"가는 방법
```
docker start myubuntu
myubuntu

docker attach myubuntu
root@542828774ee4:/#
```

run 커맨드: docker pull(이미지가 없을때) -> docker create -> docker start -> docker attach(-i -t 옵션을 사용했을때)
create 커맨드: docker pull(이미지가 없을떄) -> docker create


컨테이너 목록확인(현재 start해서 켜져있는거만)
```
docker ps
CONTAINER ID   IMAGE          COMMAND   CREATED             STATUS         PORTS     NAMES
3e261a7aca58   ubuntu:20.04   "bash"    About an hour ago   Up 2 minutes             loving_tesla
```

컨테이너 목록확인(종료된 컨테이너 포함)
```
docker ps -a
CONTAINER ID   IMAGE          COMMAND   CREATED             STATUS                      PORTS     NAMES
542828774ee4   ubuntu:20.04   "bash"    9 minutes ago       Exited (0) 30 seconds ago             myubuntu
3e261a7aca58   ubuntu:20.04   "bash"    About an hour ago   Up 2 minutes                          loving_tesla
```

컨테이너 이름 변경방법
```
docker rename loving_tesla myfucking_ubuntu
```

컨테이너 삭제(도커 UI앱에서 휴지통 표시 눌러도됨)
  - 컨테이너가 꺼져있는 상태에서만 지울수잇음 ㅇㅇ 그래서 stop커맨드로 먼저 끄고하셈
```
docker stop myfucking_ubuntu
docker rm myfucking_ubuntu
```

다음명령어는 컨테이너의 실행 상태와 관계없이 모든 컨테이너를 정지하고 삭제함(잘못하면 ㅈ망하기때문에 필요한상황아니면 하지마셈)
```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```










