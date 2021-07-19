# MBR

---

## MBR : 마스터 부트 레코드

**운영체제를 주기억장치에 적재될 수 있도록 하기 위한 정보로서 첫 번째 섹터에 위치한다. MBR은 파티션 섹터 또는 마스터 파티션 테이블이라고 불린다.**

## 디스크 접근 방식
- CHS : Cylinder Head Sector
- LBA : Logical Block Addressing

## CHS
Sector : Track을 작게 나눈 디스크 최소 저장 공간
Track : Sector의 집합
Cylinder : 수직으로 잘랐을 대 같은 위치에 있는 Track들의 집합

---

## MBR : Master Boot Record (0번 섹터)
## EBR : Extended Boot Record

VBR : Volume Boot Record 볼륨의 첫 번째 섹터에 존재

GPT : GUID Partition Table

CHS : Cylinder-Head-Sector

LBA : Logical Block Addressing

---

Partition Table Entry 는 하나의 사이즈가 16바이트다

MBR에서 어드레싱 할 수 있는 영역

4바이트 안에 표현할 수 있는 넘버 = 2^32 == 4GB

512 * 4GB(2^32) = 2TB (총 크기)

MBR쓰는 디스크는 2TB 넘는 디스크는 쓰지 못함. 2TB 이상의 디스크를 쓰고 싶다면 GPT를 써라.

---

내가 분석한 디스크 Flow

파티션이 4개보다 많을 경우 EBR을 통해서 관리가 된다.
- Partition Table Entry

### 1) MBR 분석하기
MBR : Partition Table Entry(16) * 4 = 64바이트
- 1) 07-NTFS / 시작위치 80 00 00 00 / 크기 00 00 A0 00
- 2) 07-NTFS / 시작위치 80 A0 00 00 / 크기 00 00 A0 00
- 3) 07-NTFS / 시작위치 80 40 01 00 / 크기 00 00 A0 00
- 4) 05–EBR / 시작위치 80 E0 01 00 / 크기 00 10 02 00

4개 이상이기 때문에 마지막 4번 엔트리가 EBR 시작 주소임.

### 2) EBR-1 : 1 E080(123,008) * 512 = 03C1 0000 << EBR 1 시작 주소

- 현재 파티션 정보 : 07 - NTFS, Start - 80, Size - A000 , 1E080 + 80, 3c20000
- 다음 EBR 정보 : 05 - EBR, Start - A080, Size - A080, 1E080 + A080
(1 E080에서 넘어왔기 때문에 다음 주소는 + 1 E080을 해야함)

### 3) EBR-2 : (1 E080 + A080) * 512 = 0502 0000 << EBR 2 시작 주소
- 현재 파티션 정보 : 07 - NTFS, Start - 80, Size - A0 00 , 164,224
- 다음 EBR 정보 : 05 - EBR, Start - 14100, Size – C080

### 4) EBR-3 : (1 E080 + 1 4100)(205,184) * 512 = 0643 0000
- 현재 파티션 정보 :  07 - NTFS, Start - 80, Size - C000, (205,312)644 0000
- 다음 EBR 정보가 없으므로 이것이 마지막 파티션임.

---

[디스크 분석 참고용 블로그](https://c0msherl0ck.github.io/file%20system/post-MBR/)
[MBR 구조](https://galid1.tistory.com/56)
[MBR EBR](https://kali-km.tistory.com/entry/NTFS-File-System-2)

---