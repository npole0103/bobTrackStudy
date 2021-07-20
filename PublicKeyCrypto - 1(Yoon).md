# 공개키 암호 이론 및 구현

---

[gcd / lcm 참고한 블로그](https://myjamong.tistory.com/138)
[ubuntu 20.04 openssl 설치](https://hothoony.tistory.com/1022)

## 최대공약수 GCD(Greatest Common Divisor)
최대공약수는 두 자연수의 공통된 약수 중 가장 큰 수를 의미한다.

ex) 72 와 30의 최대공약수는 6이다.


## 최소공배수 LCM(Least Common Multiple)
최소공배수는 두 자연수의 공통된 배수 중 가장 작은 수를 의미한다.

최소공배수 = 두 자연수의 곱 / 최대공약수

ex) 72 와 30의 최소공배수는 360이다.

---

## 유클리드 호제법(Euclidean Algorithm)
2개의 자연수를 받아 최대공약수를 받기 위해 2부터 두 자연수 중 작은 자연수까지 모두 나누어보면서 가장 큰 공약수를 구할 수 있다.

위와 같은 방법으로 문제를 풀면 시간복잡도는 O(N)이 된다. 나쁜 방법은 아니지만 효율을 높이기 위해 유클리드 호제법이란 알고리즘을 사용하면 시간복잡도를 O(logN)으로 줄일 수 있다.

![image](https://user-images.githubusercontent.com/37138188/126351399-b43caf2f-7937-4060-a42c-3061b88a5f20.png)

---

## C++ 코드

``` C++

#include <iostream> // gcd & lcm 백준 2609
using namespace std;

int gcd(int a , int b)
{
	while (b) // 나머지인 b가 0이 될 때까지 
	{
		int c = a % b; // (b, a % b)
		a = b;
		b = c;
	}

	return a; //그 때의 a의 값을 리턴
}

int lcm(int a, int b) // a * b / gcd(a, b)
{
	return a * b / gcd(a, b);
}

int main()
{
	int a, b;
	cin >> a >> b;

	cout << gcd(a, b) << endl;
	cout << lcm(a, b) << endl;
}

```

---

## C언어 코드 with openssl

``` C

#include <stdio.h>
#include <openssl/bn.h>

void printBN(char *msg, BIGNUM * a)
{
        /* Use BN_bn2hex(a) for hex string * Use BN_bn2dec(a) for decimal string */
        char * number_str = BN_bn2dec(a);
        printf("%s %s\n", msg, number_str);
        OPENSSL_free(number_str);
}


BIGNUM *euclid1(BIGNUM *a, BIGNUM *b)
{
  BIGNUM *t;

  while (!BN_is_zero(b)) {
        if (BN_cmp(a, b) < 0) {
          t = a;
          a = b;
          b = t;
        }
        if (!BN_sub(a, a, b)) {
          goto err;
        }
  }
  return a;
err:
  return NULL;
}


BIGNUM *euclid2(BIGNUM *a, BIGNUM *b)
{
  BN_CTX *ctx = BN_CTX_new();
  BIGNUM *r = BN_new();
  BIGNUM *t;

  if (BN_cmp(a, b) < 0) {
     t = a;
     a = b;
     b = t;
  }

  while (!BN_is_zero(b)) {
        if(!BN_mod(r,a,b,ctx)){
          goto err;
        }
        BN_copy(a,b);
        BN_copy(b,r);
  }
  BN_copy(r,a);
  if(ctx != NULL) BN_CTX_free(ctx);
  return r;
err:
  return NULL;
}

int main (int argc, char *argv[])
{
        BIGNUM *a = BN_new();
        BIGNUM *b = BN_new();
        BIGNUM *res;
        //BIGNUM *res = BN_new();

        if(argc != 3){
                printf("usage: mygcd num1 num2");
                return -1;
        }
        BN_dec2bn(&a, argv[1]);
        BN_dec2bn(&b, argv[2]);
        //BN_dec2bn(&a, "111231231231231231");
        //BN_dec2bn(&b, "2123131231221");
        printBN("a = ", a);
        printBN("b = ", b);
        res = euclid2(a,b);
        printBN("(a,b) = ", res);

        if(a != NULL) BN_free(a);
        if(b != NULL) BN_free(b);
        if(res != NULL) BN_free(res);

        return 0;
}

```

---