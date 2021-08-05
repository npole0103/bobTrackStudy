# C++

21.08.05

---
## C++

![image](https://user-images.githubusercontent.com/37138188/128359248-47afc34a-888c-4e59-9d42-224cf89c0687.png)

C언어와 C++ 다른점
![image](https://user-images.githubusercontent.com/37138188/128359317-b580b5ed-285e-4354-b68f-959583ec7fbe.png)

new-delete를 사용하면 생성자 소멸자가 있기에 메모리 누수 걱정을 할 필요가 없다.

![image](https://user-images.githubusercontent.com/37138188/128359543-ae84a536-6d78-45dc-ba0d-0cc09a524f06.png)

하지만 가능한 쓰지말자

---

## `using namespace std;` 쓰지 않는 이유

std에서 제공하는 것과 자기가 만든 것이 충돌되는 경우를 방지하기 위해서

---

## 메모리 풀이란?

미리 메모리 공간을 만들어놓고 재사용함.

---

## 클래스와 구조체

클래스 : 무겁고 단단하고 안정적이다. 디폴트 변수
구조체 : 노출되어 있다. 가볍다.

## OOP
상속성(Inheritance)
* 동일한 기능의 상하간 소통

다형성(Polymorphism)
* Overloading – 동일한 함수명을 여러 개 둘 수 있음
* Overriding – 부모의 함수를 덮어 쓰거나 사용할 수 있음
* 
은닉성(Encapsulation) : 
* private –모두에게 통제
* protected – 내 자식에게만 허용
* public – 모두에게 허용
* friend – 친구에게만 허용
 
추상성(Abstraction)
* 유사한 것을 묶음
* 세부적인 구현을 숨김

---

## 변수형

![image](https://user-images.githubusercontent.com/37138188/128360456-1723e316-5f8e-4569-b803-c42e1459dfd3.png)
![image](https://user-images.githubusercontent.com/37138188/128360494-46a3b0b6-deaa-4825-9bff-d2e5ec683293.png)

WORD는 unsigned short
DWORD는 unsigned long

Long만 차이가 나는 이유 : 윈도우의 DWORD 타입 때문이다. MS의 실수이다.

![image](https://user-images.githubusercontent.com/37138188/128360928-8e9370f3-db92-4e8c-b4eb-bac48508f18c.png)
![image](https://user-images.githubusercontent.com/37138188/128361012-0edc17a8-eda4-4bf1-9526-84e41d614aa4.png)
![image](https://user-images.githubusercontent.com/37138188/128361040-3ad69d81-9c05-4ca3-a8ff-03acb7f9dbfc.png)
![image](https://user-images.githubusercontent.com/37138188/128361057-f0457588-6e23-44f3-97bb-666aafa62b42.png)

**CPU 프로세스가 연산하기에 가장 좋은 변수 = int**

---

## 유니코드

유니코드 / EUC-KR 서로 표현하는 방법이 다르다.
![image](https://user-images.githubusercontent.com/37138188/128361545-c7bf6852-69a7-4ec4-a7a8-5c28891c5ccb.png)
UTF-16 인코딩을 사용하면 1바이트로도 표현할 수 있는 문자에 그보다 더 많은 바이트를 소비해야 하는데, UTF-8 인코딩을 사용하면 그런 문제점이 없다. 그러나 한자나 한글은 주로 3바이트 영역에 집중되어 있기 때문에 거의 모든 문자에 균일하게 2바이트만 사용하는 UTF-16에 비해 오히려 크기가 커진다. 그럼에도 불구하고 세계적으로는 UTF-8 인코딩이 가장 널리 쓰이기 때문에 유니코드를 지원하는 대부분의 프로그램들은 일단 UTF-8을 디폴트 상태로 지정해 주는 경우가 많다. 웹 등지에서 유니코드 적용이 서구권을 중심으로 퍼졌기에 서구권 입장에서는 기존 8비트 코드(1바이트 아스키 코드)와 호환성이 있는 UTF-8을 많이 선택했고, 결국 이것이 대세가 된 것이다.

**BOM : 파일의 가장 첫머리에 들어가서 어떤 UTF인지 알려주는 것**

![image](https://user-images.githubusercontent.com/37138188/128362301-87491471-0ed0-49d7-8cb0-d17a15eaeca4.png)

**왜 UTF8을 사용할까?**
- 아스키 : 표현되지 않는 문자열 존재
- UTF16 : 표현이 안되는 문자열 존재
- UTF32 : 저장 공간을 많이 사용한다.
**UTF8 : CPU 소비**

---


