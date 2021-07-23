#  초간단 OS 리얼모드

---

WDK : 윈도우 드라비어 킷

Ring 3 : 유저 모드

Ring 0 : 커널 모드

GDT(Global Descriptor Table) : GDT에 있는 base 주소를 참조해서 각 세그먼트들의 주소로 접근할 수 있다.

IDT(Interrupt Descriptor Table) : 인터럽트 상황이 왔을 때 호출해주어야 하는 함수 목록을 가지고 있는 테이블

---

호스트에서 `vmmon64.exe` 실행

게스트에서 `target64\vminstall.exe` 실행

F8 누른 후 서명 안함 선택

시작하자마자 멈춤. Windbg에서 `g` 키 누르면 실행

게스트에 `커널 드라이버 로더` 설치

`.sys` 파일 커널 드라이버 로더하면 Windbg에 출력값 표현됨.

---


