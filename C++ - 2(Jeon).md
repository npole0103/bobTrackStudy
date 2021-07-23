# C++ 객체지향 프로그래밍

*21.07.22. ~ 21.07.23.*

---

## 프로젝트 셋팅

![image](https://user-images.githubusercontent.com/37138188/126739812-3df72237-0ebf-4357-8155-8a146ec04c35.png)

---

![image](https://user-images.githubusercontent.com/37138188/126739876-7768ba00-2aff-4de4-ac4c-4d25cb3c7985.png)

**디렉토리 구조화 시키고 설정해줘야할 옵션**

1. 출력 디렉토리 : 빌드된 파일이 생성되는 곳 `../../Build/$(Platform)$(Configuration)\` **구성 속성 - 일반**
2. 중간 디렉토리 : 오브젝트 파일이 생성되는 곳 `../../Output/$(Platform)$(Configuration)/$(ProjectName)\` **구성 속성 - 일반**
3. 추가 포함 디렉토리 : Include 모아놓은 곳 `$(ProjectDir)\..\..\Inc` **C/C++ - 일반**
4. 추가 라이브러리 디렉토리 : 라이브러리 파일 모아놓은 곳  `$(ProjectDir)\..\..\Lib` **링커 - 일반**
5. 전처리 옵션 : #define 같은 매크로를 속성에서 대체할 수 있음. **C/C++ - 전처리기**

---

## MT/MD

![옵션 총 정리](https://user-images.githubusercontent.com/37138188/126740481-df1657b6-265e-4bdf-aae9-7e80d748d7f9.png)

옵션 총 정리

![image](https://user-images.githubusercontent.com/37138188/126740305-1387d319-2a30-4f14-a8e3-737c8f7b6f6e.png)

각 런타임 라이브러리 옵션 적용시 크기

이외에 선행 지식
- 일괄 빌드
- 구성 관리자 

---

Q) CPU 프로세서가 32비트에서 64비트로 늘어나면 뭐가 좋을까?  
A) 메모리 주소 표현이 늘어난다.
- 32비트는 메모리 주소 4바이트
- 64비트는 메모리 주소 8바이트

시스템 라이브러리는 모든 경우의 함수를 빌드하여 준비해 둠.

라이브러리 추가하는 법
`#pragma comment(lib, "a.lib")` << 하나의 컴파일러 버전에서 4개를 준비한다. 시스템 디렉토리에.

그래서 Release와 Debug에서 어디든 실행하던 잘 된다.

**추가 라이브러리 디렉토리 설정**으로 설장하도록 하자

---

오픈소스는 빌드된 하나의 라이브러리 파일이 모든 컴파일 옵션에 대응되는 경우도 있다.

오류
- LNK로 시작하는 오류는 링커 오류
- C090이런 오류는 컴파일 오류

---
원소스 듀얼 컴파일

![image](https://user-images.githubusercontent.com/37138188/126740952-730160e1-30c1-420c-b6f3-38f5ccf5e22d.png)

---

## cmake

![image](https://user-images.githubusercontent.com/37138188/126741171-42f61212-b3d8-4385-ad2f-e731e59aab75.png)

필요한 상황에 맞게 각 폴더에서 `CmakeLists.txt`로 옵션을 설정.

이후 Src 폴더에서 다음 명령어 순차 실행
`cmake ../Src`  
`cmake --build .`

---


