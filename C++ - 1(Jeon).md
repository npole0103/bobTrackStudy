## C++ 프로그래밍 기초

---

![image](https://user-images.githubusercontent.com/37138188/126182347-c0ba7c27-0539-4368-bf88-3fd808b060ad.png)

---

포인터, 문자열 처리, 해결하기 힘든 컴파일 링커 오류, 배우기도 까다롭고 너무나 많은 API

---

![image](https://user-images.githubusercontent.com/37138188/126182414-2c31731a-76fa-434c-b4a6-1e5a275b0c13.png)

---

실행파일 빌드 과정의 이해

컴파일 – 링크 – exe 

CPU가 해석하기 위해선 기계어가 필요하다.

![image](https://user-images.githubusercontent.com/37138188/126182426-4f50c902-9cf4-419d-94e3-adb5db019089.png)

프로그램은 전부 함수로 되어 있다.

**소스코드 -> 오브젝트 파일 -> 기계어 -> 실행 파일**

---

다양한 프로젝트 형식

정적 라이브러리, 동적 라이브러리, 실행 파일

![image](https://user-images.githubusercontent.com/37138188/126182433-766dd2f9-0382-4d05-8347-64f8332ea9c2.png)

**라이브러리**
- 정적 라이브러리는 파일 형태이다.
- 동적 라이브러리랑 실행파일은 플러그인이다.

---

정적 라이브러리란? :헤더 파일과 라이브러리 파일

컴파일 시점이 불완전할 가능성이 있다.

컴파일 때야 함수가 있는지 없는지 확인할 수 있다.
헤더에는 나와있는데, 링크시 안됨.

사실은 컴파일은 성공하지만, 링크할 때 확인이 성공된다.

---

동적 라이브러리란?

동적 라이브러리는 런타임에 불완전할 가능성이 있다.

동적 라이브러리는 함수를 마음대로 바꿀 수 있음.
빌드가 된 라이브러리임. .dll

정적 라이브러리와 다르게 함수가 있다는 것을 보장.

바뀐 걸 모른 채 호출하면 죽어버린다.

![image](https://user-images.githubusercontent.com/37138188/126182443-012c7094-3f67-4efb-91e4-226d6c343c73.png)

a와 b 두 개만 넣다가, 함수가 a, b, c를 인자로 받는 것으로 바뀌었는데.

---

**컴파일러의 이해**

A에서 B를 쓰고, B에서 A를 쓰고 >> 자바에서는 가능인데 C++에선 안됨.

솔루션)
1) 클래스를 하나로 나눔.
2) 클래스 세 개로 – 공통 – A – B

---

컴 파일러는 줄 세우기를 함.
A위에 B가 있어야 하고, B위에 A가 있어야 하는데 계속해서 추적하다가 못 오류 발생
>>> 순환 참조 오류

---

순서를 정하기 위해서 Include가 정확한 역할을 함.

![image](https://user-images.githubusercontent.com/37138188/126182456-11fcccae-aca3-45e2-9774-5dd985d88aed.png)

include 하지않고, class가 어디있는지 알려주는 선언만 해주면 의존성 순환을 막을 수 있음.

---

![image](https://user-images.githubusercontent.com/37138188/126182464-ce7b454b-6fba-43ad-a19f-008a521bdaf1.png)

유니코드를 선언을 안하고 하고의 차이

![image](https://user-images.githubusercontent.com/37138188/126182474-1c3f21f5-ac61-4a30-be57-d9a19290b36c.png)

컴파일 옵션을 바꿔서 문자가 하나는 1바이트, 하나는 2바이트로(L인게 유니코드) 바뀐다.

![image](https://user-images.githubusercontent.com/37138188/126182481-e1898563-4d58-444f-96dc-e4bee79f26ef.png)

문자열 처리에 2가지가 있기 때문에

![image](https://user-images.githubusercontent.com/37138188/126182489-4138583a-89d7-48be-b20a-4a506ded81db.png)

유니코드란 값을 넣느냐 안 넣느냐에 차이

### +유니코드 추가 설명

[멀티바이트, 유니코드 그리고 TCHAR](https://honestgame.tistory.com/199)

- SBCS / 1 Byte
- MBCS / 1 Byte(영문), 2 Byte(한글)
- UNICODE / 2 Byte

UNICODE와 MBCS에 따라서 따로 구분해서 프로그램 할 필요가 없도록 하기위해서 사용하는 것이 TCHAR 매크로.

TCHAR 타입이 UNICODE가 정의된 경우 wchar_t 타입으로 작동(2 Byte)

TCHAR 타입이 MBCS가 정의된 경우 char 타입으로 작동(1 Byte)

---

### 중요 요약

1. 소스 코드를 정렬을 하고 전처리를 함.
2. 컴파일 하고
3. 링크를 한다.

---

#이 붙은 것들은 컴파일 지시어.
ex) #include, #define

---

컴파일 기법 – 원소스 듀얼 컴파일

![image](https://user-images.githubusercontent.com/37138188/126182497-f1cc456d-08b4-4e38-9cfb-509f0f8b352c.png)

링커는 오브젝트 파일을 갖다 쓰기 떼문에, 이것을 쓴다.

![image](https://user-images.githubusercontent.com/37138188/126182540-c7126fe4-f8e4-4219-add5-6dc3d248df2f.png)

하나의 소스에 프로젝트 파일 2개 만들고 UNICODE랑 ??바이저 모드로 2개를 설정하고 실행

---

![image](https://user-images.githubusercontent.com/37138188/126182562-2b3b6c0c-6a37-4183-97b4-7d14ea4202df.png)

링커는 완벽하게 동일한 오브젝트 파일은 제거시킨다.

제일 중요한 것 : 우리가 컴파일과 링커의 동작을 알 수 있다

---

개발 툴 준비 사항
- Visual Studio
- Windows : PEView, HxD, void 사의 everything

TCHAR는 컴파일러에 따라서 언제나 형태가 바뀔 수 있는 Transform

---
