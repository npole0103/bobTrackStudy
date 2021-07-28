# NTFS

[NFTS 총정리](https://jdh5202.tistory.com/656)

---

## NTFS

FAT보다 뛰어난 서버용 파일시스템의 필요성 대두

---

## NTFS의 특징

* Journaling : 볼륨에 수행되는 모든 작업에 대해서 트랜잭션 단위로 기록함.
* 암호화 : 파일의 데이터 영역에 대한 암호화 기능 제공
* 압축 : 파일의 데이터 영역에 대한 압축 기능 제공
* 디스크 쿼터 : 특정 사용자가 전체 디스크를 다 사용하는 것을 막기 위해, 관리자가 사용자가 사용할 수 있는 디크스 아용량의 한계를 설정하는 기능
* ADS(Alternate Data Stream) : NTFS에서는 하나의 파일이 하나 이상의 데이터를 담을 수 있다.
* Sparse 파일 : 파일의 내용의 대부분이 0으로 차 있을 경우, 실제 저장되지 않고, 0으로 되어있다라는 기록만 가지게 됨. 실제 디스크를 차지 않아도 되는 영역을 제거해서 실제 저장 크기를 줄일 수 있음.
* 대용량 파일 : NTFS 에서는 파일 사이즈를 표현하는 크기가 8 bytes 이고 2^44까지 실제로 처리가능함.
* 유니코드 지원 : NTFS 는 파일시스템에 유니코드로 저장됨 (UTF 16)

---

## MFT

![image](https://user-images.githubusercontent.com/37138188/127321630-fba810f9-b636-44f1-a22e-61fed5a24583.png)

* NTFS 는 정형화된 볼륨 레이아웃이 없고, 전체를 데이터 영역으로 관리한다.
* 볼륨에 존재하는 모든 파일과 디렉토리 정보를 담고있는 MFT가 존재
* MFT만 파싱함으로써, 빠르게 파일 시스템을 분석할 수 있다.
* 파일이나 디렉토리가 많아질 수록 MFT가 커짐
* 한번 커진 MFT는 줄어들지 않음

---

## VBR
![image](https://user-images.githubusercontent.com/37138188/127321460-c70d423e-c676-4e3f-9bd3-df0593d17c91.png)

---

## Data 영역

![image](https://user-images.githubusercontent.com/37138188/127319753-26d10953-2be3-45b3-9a03-f1ae75014d0f.png)
![image](https://user-images.githubusercontent.com/37138188/127319780-4cfefc9e-b67e-4be6-97e6-abb788f8c337.png)


클러스터 단위로 NTFS 볼륨을 전체 읽고 쓸 수 있다.

MFT Entry Size : 0xF6(-10)로 음수라면 2^10으로 간주하고 하나당 1024

Index Record Size : 단위가 클러스터

Byte Per Sector 11부터 2바이트 == 00 02 => 02 00 -> 512바이트
Sector Per Cluster 13부터 1바이트 == 08 => 08 * 512 == 4KB == 4096바이트

Total Sector 40부터 8바이트 : 02 7F FF
02 7F FF * 512(200hex) / 1024 == 79MB **다시 확인하기**

1A AA << MFT 스타트(단위 클라스터)
- 위치 : 1A AA(Hex) * 4096 = 1AA A000

02 << MFT 미러 스타트(단위 클러스터)
- 위치 : 02(Hex) * 4096 = 2000

내 드라이브
- MFT START : C 00 00 * 1000(4096) -> C0000000
- MFT MIRROR START : 2 * 1000(4096) -> 2000

1DA6 9C65 * 200(Hex) / 1024 / 1024 / 1024 = 237GB

---

## MFT Entry Size

**VBR의 값들은 기본적으로 클러스터 단위로 표현**

해당 값이 양수면 MFT Entry Size * 클러스터 크기

해당 값이 음수면 마이너스를 곱한 값 N이라고 할 때 2^N이 값이 된다.

0xF6은 –10이 되고  2^10 = 1024 엔트리 사이즈가 됨.

---

## MFT Entry Header

![image](https://user-images.githubusercontent.com/37138188/127319883-c20ab811-282e-4776-b35a-3ec57b72d330.png)


---

## Resident / Non-Resident

**Resident**
![image](https://user-images.githubusercontent.com/37138188/127321819-53e9be77-9a20-4258-9eca-2228175512e2.png)

**Non-Resident**
![image](https://user-images.githubusercontent.com/37138188/127321927-74cb950c-b49c-4d4a-9426-286f06fbbb16.png)

---

## 전체적인 파일 헤더

![image](https://user-images.githubusercontent.com/37138188/127321985-0a769d4e-c419-4b69-9e8a-443bf2ddd03f.png)

---

## 데이터 주소 찾아가는 법

[NFTS 총정리](https://jdh5202.tistory.com/656)

---

