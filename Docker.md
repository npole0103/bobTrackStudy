# 도커 개념 정리

[도커 이론 개념 정리](https://velog.io/@cckn/Docker-%EC%9D%B4%EB%A1%A0-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC)
[도커 개념 및 핵심 설명](https://khj93.tistory.com/entry/Docker-Docker-%EA%B0%9C%EB%85%90)
[도커 개념 및 간단한 명령어 정리](https://jungwoon.github.io/docker/2019/01/11/Docker-1.html)
[도커 개념 정리 및 사용 방법](https://cultivo-hy.github.io/docker/image/usage/2019/03/14/Docker%EC%A0%95%EB%A6%AC/)

---

## Docker

**컨테이너 기반의 오픈소스 가상화 플랫폼**

Docker는 컨테이너를 기반으로 하는 오픈소스 가상화 플랫폼

다양한 프로그램, 실행환경을 컨테이너로 추상화하고 동일한 인터페이스를 제공하여 프로그램의 배포 및 관리를 단순하게 해줍니다. 백엔드 프로그램, 데이터베이스 서버, 메시지 큐등 어떤 프로그램도 컨테이너로 추상화할 수 있고 조립PC, AWS, Azure, Google cloud등 어디에서든 실행할 수 있습니다.

---

## 컨테이너

화물 컨테이너를 생각해보자

화물 컨테이너를 이용해서 물건을 실으면 물건의 크기와 무게 등과 상관없이(신경 쓰지 않고) 물건을 적재할 수 있다.

소프트웨어에서 말하는 컨테이너도 마찬가지다

여러 소프트웨어 등을 동일한 규격으로 묶어 실제 사용자가 최대한 신경을 덜 쓰고 사용할 수 있도록 만든 것이 컨테이너이다.

---

## 가상화를 사용하는 이유?

컨테이너는 가상화 기술 중 하나로 대표적으로 LXC(Linux Container)가 있습니다. 기존 OS를 가상화 시키던 것과 달리 컨테이너는 OS레벨의 가상화로 프로세스를 격리시켜 동작하는 방식으로 이루어집니다.

한 서버의 여러 OS를 가상화 하여 사용하는 것과 컨테이너 방식으로 프로세스를 격리시켜 동작하는 방법은 어떠한 차이점이 있을까요?

---

## VM / Docker 차이

![image](https://user-images.githubusercontent.com/37138188/127309655-3762f976-363d-4ab9-b153-2b902fbf0d33.png)

기존에 우리에게 익숙한 VM같은 경우엔 Host OS 위에 가상화를 시키기 위한 Hypervisor 엔진 그리고 그 위에 Guest OS를 올려 사용합니다.

이는 가상화된 하드웨어 위에 OS가 올라가는 형태로 거의 완벽하게 Host와 분리된다고 봐도 무방합니다.

반면에 컨테이너 기반 가상화는 Docker 엔진 위에 Application 실행에 필요한 바이너리만 올라가게 됩니다.

---

## 도커 이미지

Docker Image란 컨테이너를 실행할 수 있는 실행파일, 설정 값 들을 가지고 있는 것이라고 생각 하면 됩니다.

그림과 같이 Image를 컨테이너에 담고 실행을 시킨다면 해당 프로세스가 동작하게 되는 것이죠.

그럼 어떻게 이미지가 만드는지 알기 위해선 어떻게 이미지가 만들어지는지 먼저 알아보도록 하겠습니다.


---

## 도커 파일

Docker File은 이미지 생성 출발점으로 이미지를 구성하기 위한 명령어들을 작성하여 이미지를 구성할 수 있습니다.

그 뜻은 Docker File을 읽을 수만 있다면 해당 이미지가 어떻게 구성되어 있는지도 알 수 있다는 의미가 됩니다.

```
$ vim Dockerfile

FROM ubuntu:14.04

# app 디렉토리 생성
RUN mkdir -p /app

#Docker 이미지 내부에서 RUN, CMD, ENTRYPOINT의 명령이 실행될 디렉터리를 설정합니다.
WORKDIR /app  

# 현재 디렉터리에 있는 파일들을 이미지 내부 /app 디렉터리에 추가함
ADD     . /app

RUN apt-get update
RUN apt-get install apache2
RUN service apache2 start

VOLUME ["/data", "/var/log/httpd"]


# 하기 포트를 외부로 노출합니다.
EXPOSE 80

# 쉘을 사용하지 않고 컨테이너가 시작되었을 때 logbackup 스크립트를 실행
CMD ["/app/log.backup.sh"]

:wq!
```

---

## 이미지와 컨테이너 차이

이미지와 컨테이너는 무엇일까??

이미지는 소프트웨어 구동에 필요한 의존(Dependency)과 명세를 담고 있다.

컨테이너는 이미지를 통해 만들어진다.

개발을 해본 사람이라면 Class와 Instance의 차이를 알 것이다.

일반적인 경우에는 Class를 직접 사용하지 않는다.

해당 Class를 기반으로 한 Instance를 생성하여 사용한다.

컨테이너와 이미지도 같은 이치이다.

---

## Docker 명령어

`sudo usermod -aG docker $USER` : 현재 접속중인 사용자에게 권한주기

`docker -v` : 도커 버전 확인

`docker ps` : 도커 Process Status, Running 중인 것만 표시

`docker ps -a` : 도커 Process Status, 모든 컨테이너 표시

`docker pull [이미지이름]:[태그]` : 도커 공식 이미지 저장소에서 이미지를 내려받는다.

`docker images` : 도커 이미지 확인하기

`docker create [옵션] [이미지이름]:[태그]` : 이미지로 컨테이너 생성하기

ex) `docker create -i -t centos:7`
- -i : 상호 입출력
- -t : tty를 활성화하여 bash 쉘을 사용

`docker start [이미지이름]:[태그]` : 만들어진 컨테이너 실행하기

`docker stop [이미지이름]:[태그]` : 컨테이너 중단하기

`docker attach [이미지이름]:[태그]` : 도커의 내부쉘로 들어가는 명령어

`docker run [옵션] [이미지 이름]:[태그]` : 컨테이너 만들고 실행하기. 위의 생성 -> 실행 -> 들어가기 까지 한번에 해주는 명령어 입니다.
- -i : 상호 입출력
- -t : tty를 활성화하여 bash 쉘을 사용

`docker rename [기존 이름] [변경 하고자 하는 이름]` : 컨테이너 이름 변경

`docker rm [컨테이너 이름]` : 컨테이너 삭제

`docker rmi [이미지 이름]` : 도커 이미지 삭제

`docker rm 'docker ps -a -q'` : 컨테이너 전체 삭제

`docker run -i -t --name [MY_WEB_SERVER_IP] -p [호스트 포트]:[컨테이너의 포트] [이미지이름]:[태그]` : 컨테이너 외부에 노출

ex) `docker run -i -t -p 3306:3306 -name 192.168.0.100:7777:80 ubuntu:14.04`

---

