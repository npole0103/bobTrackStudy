# C++ 객체지향 프로그래밍

*21.07.26.*

- 동적 라이브러리 확장자 : .dll
- 정적 라이브러리 확장자 : .lib

---

## 특수한 헤더파일

- 공통 헤더 파일 : stdafx.h
- 대표 헤더 파일 : 라이브러리명.h

### 공통 헤더 파일 `stdafx.h`
흔히 쓰이는 공통 구문을 모아놓은 헤더

모든 cpp 파일의 첫줄에는 다음과 같이 쓰여야 함. >> `#include "stdafx.h"`

자주 쓰이는 구문 : `#include <stdio.h>` `#include <iostream>`

### 대표 헤더 파일 `Module.h`
내가 만든 소스코드를 다른 사람에게 전달하기 위한 여러 개의 파일로 이루어졌다면 가져다 쓰는 입장에서 어떤 파일을 include 해야할지 난감.

그렇기 때문에 대표 헤더 파일을 하나 생성 해주고

``` c
#pragma once
#include "a.h"
#include "b.h"
#include "c.h"
#include "d.h"

```

**사용자는 대표 헤더 파일만 공통 헤더 파일에 include 해두면 cpp 전역에서 사용 가능해 짐.**

---

## 디버깅 기술


### 중단점 설정 및 헤제
F9 단축기로 중단점 설정 가능 -> 이후 F5로 중단점 이동

### 한 줄 실행
- F10 프로시저 단위 실행
- F11 한 단계의 코드 실행 - **함수 내부까지 들어감**

### 변수 들여다 보기

디버그 도구 - 로컬

- 변수 이름
- 변수 값
- 메모리
- 형식

확인 가능

### 호출 스택 보기

디버그 도구 - 호출 스택

항목이 여러개 나오는데, 맨 밑에서부터 시작된다. STACK 구조.

그 직전에 어떤 함수에서 현재 함수를 불렀는데 조회할 수 있다.

### 조사식

디버그 도구 - 조사식

로컬이랑 비슷하나 프로그래머가 직접 변수, 포인터, 함수 등 문법을 사용하여 정보 확인 가능

### 메모리 보기

앞에서 얻어온 로컬 변수 a의 주소를 디버깅 메모리 창에 입력하면 해당 지점의 메모리 상태 조사 가능.

4바이트 int형에 있으므로, LE 형태의 `0a 00 00 00` 기록

### 스레드 이동

메인 스레드도 돌고 있지만, 다른 스레드인 ThreadFunc도 동시에 실행되는 상태라고 가정하면

스레드 탭으로 변수를 왔다갔다 할 수 있다.

---

## 다양한 프로젝트와 실행방식

임시 프로세스 만들기

솔루션 내에서 프로젝트(콘솔앱) 만듦.

**ReleaseMT로 생성 불가 시에 다른 프로젝트와 솔루션 ReleaseMT 지우고 다시 만들기**

이후 새로 만든 프로젝트도 Build / Inc / Lib / Output / Src 똑같이 셋팅

**서로 통신하도록 작업디렉토리 설정 : 속성 - 구석 속성 - 디버깅 - 작업 디렉터리 : `$(OutDir)`**



**main.cpp**
``` c
#include "stdafx.h"

int ShellExecuteByPipe(const char* pszExeFile)
{
    FILE* pPipe = NULL;
    pPipe = ::_popen(pszExeFile, "r");
    if (NULL == pPipe)
        return -1;

    const size_t tBuffSize = 64;
    char szBuf[tBuffSize];
    while (::fgets(szBuf, tBuffSize, pPipe))
        printf("%s", szBuf);

    return ::_pclose(pPipe);
}

int main()
{
    printf("exit-code:%d\n", ShellExecuteByPipe("TempExe.exe 8756"));

    return 0;
}

```

**TempExe.cpp**
``` c

#include "stdafx.h"
using namespace std;

int main(int arg, char* argv[])
{
    int nExitCode = 0;
    if (1 < arg)
        nExitCode = atoi(argv[1]);

    printf("안녕하세요 김수헌 입니다.\n");
    printf("보안제품개발 트랙\n");

    return nExitCode;
}

```

- 인자 값으로 받은 `nExitCode`를 반환
- `pritnf()` 출력.

---


