# AWS 기초

[참고한 블로그1](https://easy-h.tistory.com/16)
[참고한 블로그2](https://dreamdeveloper403.tistory.com/31)

---

## 21.07.21

## 왜 우리가 AWS를 사용해봐야 하는 것인가?

**클라우드 인프라 자체의 보안은 AWS가 담당**
- 컴퓨팅
- 스토리지
- 데이터베이스
- 네트워킹
- 가용 영역
- 리전
- 엣지 로케이션

**클라우드 인프라 위의 보안은 고객이 담당**
- 고객 데이터 / 어플리케이션
- 플랫폼
- 어플리케이션
- 계정 및 접근 관리
- 운영체제, 네트워크 및 방화벽 설정 / 구성
- 암호화 키 관리
- 서버 및 클라이언트 암호화
- 네트워크 트래픽 방어

---

## 클라우드 컴퓨팅
컴퓨팅 파워, 데이터베이스 스토리지, 애플리케이션 및 기타 IT 리소스를 필요에 따라 인터넷을 통해 제공하고 사용한 만큼만 비용을 지불하는 개념임

## IaaS / PaaS / SaaS

![image](https://user-images.githubusercontent.com/37138188/126520418-3a54477b-739a-4b52-a63f-ebe595ff12b8.png)

서비로서의 인프라 IaaS : 클라우드 IT의 기본 빌딩 블록을 포함하고 일반적으로 네트워킹 가능, 컴퓨터 및 데이터 스토리지 공간을 제공함. 기존 IT 리소스와 가장 유사함.(VPC, EC2, S3, EBS, EFS)

서비스로서의 플랫폼 PaaP : 조직은 기본 인프라를 관리할 필요 없어 애플리케이션 개발과 관리에 집중 가능함.

서비스로서의 소프트웨어 SaaS : 완전한 제품을 제공하는 것을 뜻하며 최종 사용자 어플리케이션이라고 할 수 있다. 특정 소프트웨어를 어떻게 사용할 것인가에 대해서만 집중하면 되며 서비스가 어떻게 유지 관리되고 인프라는 어떤지에 대해서 생각할 필요가 없다.

## Region
복수 개의 데이터 센터의 독립적인 물리적 위치를 말하며 AWS 자원은 리전 단위로 제공되고 각 리전은 개별 가용구역(AZ)으로 구성되어 있다. (인터넷으로 연결되어 있는 지역)

---

## Availability Zones
하나의 Region 내에 공간적으로 분리된 전원을 말하며 물리적 보안, 백업 역할을 하는 안전 장치로 운영되는 데이터 센터를 의미한다. 개별적인 AZ 사이엔 낮은 속도를 가진 서버 클러스터로 연결되어 데이터 처리를 할 수 있는 특징을 가지고 있다.

---

## EC2(Elastic Compute Cloud)
가상 서버, 즉 독립된 하나의 컴퓨터를 임대해주는 것을 말한다.
다양한 OS를 사용 가능하며 cpu, 메모리, 네트워크에 따른 다양한 인스턴스 타입을 지원하며 다양한 과금 옵션도 제공한다.
- 유연한 가상 서버를 구축하고 보안 및 네트워크 구성과 스토리지 관리가 가능
- 실제로 사용한 용량만큼만 지불
- Lunux 또는 Windows 운영체제

---

## Instance
AWS에서 제공하는 하나의 컴퓨터 개념이다. 인스턴스 컴퓨터에 원격으로 접속하여 제어 가능하며 웹서버를 설치하거나 거대한 DB환경을 구성할 수도 있음.

---

## S3(Amazone Simple Storage Service)
- 어디서나 원하는 양의 데이터를 저장하고 검색할 수 있도록 구축된 객체 스토리지
- 데이터를 버킷에 저장함, 객체는 파일과 해당 파일을 설명하는 메타데이터로 구성됨
- 버킷에 저장 가능한 객체 수의 제한 X
- 비용이 비싸다. 멀티 클라우드를 고려하게 된다.

---

## EBS(Amazone Elastic Block Store)
대규모 처리량과 트랜잭션 집약적인 위크로드 모두를 지원하기 위해 Amazone EC2에서 사용하도록 설계된 사용하기 쉬운 블록 스토리지 서비스

---

## EFS(Amazone Elastic File System)
EC2 인스턴스를 위한 완전 관리형 파일 시스템이며 어디에서나 접근이 가능함.

## 데이터베이스 서비스

**RDS(관계형 데이베이스)**
- Amazone RDS
- Amazone Aurora : 클라우드에 최적화된 MySQL 및 PostgreSQL 호환성의 관계형 데이터베이스
- Aurora Global DataBase : 여러 AWS 리전에 걸쳐 있어, 지연 시간이 짧은 전역 읽기와 리전 전체 중단에 대한 재해 복구를 지원함
- Amazone Aurora 서버리스 : 온디엔드 Auto Scaling 구성, 클라이언트 중단 없이 컴퓨팅 및 메모릭 용량 확장
- Amazone RedShift
- Amazone RDS on VMware

**No SQL(Not Only SQL, 비관계형 데이터베이스)**
- Amazone ElasticCache
- Amazone DynamoDB : 빠르고 유연한 Key-Value NoSQL 데이터베이스 서비스
- Amazone Neptune
- Amazone Timestream
- Amazone DocumentDB
- Amazone Quantum Ledger Database(QLDB)

---

## VPC(Virtual Private Cloud)
[VPC 설명](https://pjh3749.tistory.com/283)

### 선수지식

#### IPv4

![image](https://user-images.githubusercontent.com/37138188/126523028-4b555b5b-e7dc-48ea-ae28-49c5671db9a4.png)

IPv4 : 32자리 8bit씩 4등분

각 자리를 옥텟이라고 부른다.

#### 클래스

![image](https://user-images.githubusercontent.com/37138188/126523094-8b27f94a-f19e-43d3-b379-8fb7a2a5458a.png)

CLASS A / CLASS B / CLASS C

각 클래스에 따라서 Network ID와 Host ID를 구분한다.

#### 클래스 구분 하는 법

![image](https://user-images.githubusercontent.com/37138188/126523676-517449ae-a1b3-481a-b8f6-f57a0faee68e.png)


#### CIDR(Classless Inter-Domain Routing)

CIDR은 급격히 부족해지는 IPv4 주소를 보다 효율적으로 사용하게 합니다. 표현형식은 xxx.xxx.xxx.xxx/yy 형태로 표시를 하게 됩니다.

맨 뒤의 yy는 서브넷 마스크를 2진수로 바꾸었을 때 1의 개수입니다.

위에서 언급했듯이 기본적으로 C 클래스는 24개의 1로 아이피를 가려버립니다. 가린 이후의 자릿수부터 사용할 수 있게 됩니다.

![image](https://user-images.githubusercontent.com/37138188/126524745-d651f25c-3926-4a0e-ada2-3eb2e9630407.png)


[VPC 완전 정리](https://seohyun0120.tistory.com/entry/AWS-VPC-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC)

---

## 21.07.22

---

## AWS Lambda

[참고](https://seoyeonhwng.medium.com/aws-lambda%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-44df535d5487)

### AWS Lambda
Lambda는 AWS에서 제공하는 서버리스 컴퓨팅 플랫폼이다.

### 서버리스란
서버가 없다는 뜻이 아니고 개발자가 서버의 존재를 신경쓸 필요가 없다는 뜻이다.  
서버가 잘 돌아가고 있는지, 개수와 사양한 적당한지 등등 신경쓸 필요없이 사용자는 오직 코드에만 집중할 수 있으니 무척 편하다.

이때 사용한 컴퓨팅 시간, 용량에 대해서만 AWS에게 비용을 지불하면 된다.

### 언제 쓰면 좋을까?
코드를 계속 실행시키기 보다는 특정한 시기에만 실행시키는 경우에 Lambda를 사용하면 유용하다.

예를 들면
- 서버 띄우지 않고 간단한 코드를 실행시키고 싶은 경우
- 특정 기간 또는 특정 주기로 코드를 실행시켜야 하는 경우
- 트리거가 실행될때만 코드를 실행시키고 싶은 경우

하지만 람다의 단점도 존재한다.
- 코드 용량이 최대 250MB 이다.
- 함수 실행 시간은 최대 15분이다.
- 처음 함수 호출시 Cold Start를 하게되고 초기 지연시간이 발생한다.
- 비싸다.
- 
등등이 있지만 그래도 서버 걱정 없이 오직 코드에만 집중 할 수 있다는 것은 굉장히 편하고 합리적인 것은 분명하다.

---

## ELB(Elastic Load Balacing)
[참고](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=theswice&logNo=221174336958)

ELB는 Load Balancing이라는 이름처럼 접근을 여러 대의 EC2 인스턴스로 분산하는 역할을 담당합니다.

일반적으로 접근 분산 기능을 사용하는 목적은 크게 두 가지입니다. 
- 대량의 접근을 여러 개의 인스턴스로 처리를 부하 분산하는 목적입니다.
- 1대의 인스턴스에 장애가 발생한 경우에도 다른 인스턴스로 서비스 제공을 지속할 수 있게 하기 위한 가용성 보장 성격의 목적입니다.

### ELB 서비스의 가용성
ELB는 접속 부하에 맞게 자동적으로 리소스의 확장/축소를 수행합니다. 따라서 ELB는 요청처리 능력을 항상 감시합니다.

대량의 요청이 발생해도 ELB로 인해 병목 현상이 발생하는 상황은 거의 일어나지 않습니다.

---

## ELB 종류 - CLB / ALB / NLB

![image](https://user-images.githubusercontent.com/37138188/126741886-a197e4b4-9f5d-40d4-a1de-c43d21ca7cf3.png)

---

## Web Application Hosting 이해하기

![image](https://user-images.githubusercontent.com/37138188/126741349-7121f459-b027-4434-8dcf-2c38cb8c8a89.png)

CLB 또는 ALB라고 이해하면 됨.

---