
## docker_manual

도커 버전 확인법
```
# docker -v
Docker version 20.10.8, build 3967b7d
```

컨테이너 생성
예) 우분투 20.04 컨테이너 생성.(로컬 도커엔진에 존재하지않다면 
```
# docker run -i -t ubuntu:20.04
root@3e261a7aca58:/#
```
여기서 
-i -t 옵션은 컨테이너와 상호(interactive) 입출력을 가능케함
root는 기본 사용자
3e261a7aca58는 호스트 이름(무작위 16진수 해시값)
