# GPT & FAT32

---

GPT

![image](https://user-images.githubusercontent.com/37138188/126352967-2a872ad7-c6df-4972-a33a-01a6b4366a29.png)

단위는 Sector임.

처음 시작은 EFI PART. BackUp Header가 존재한다.

---

파티션 엔트리 사이즈가 128이기 때문에

한 섹터당 엔트리 갯수는512/128 = 4개

![image](https://user-images.githubusercontent.com/37138188/126353289-553c1c71-6609-4a13-9c86-05d7c1def114.png)

2 ~ 33까지 총 32 섹터를 사용하는데, 최대 엔트리 갯수 == 섹터 1개당 4개의 파티션 정보를 사용하니까 32 * 4 = 128

---

GPT 헤더

![image](https://user-images.githubusercontent.com/37138188/126353500-d6b0d8e4-c76d-4780-968e-ef11214158ac.png)


GPT 1번 섹터는 헤더 정보가 들어 있음.

GPT 2번 섹터부터 파티션 테이블 정보

![image](https://user-images.githubusercontent.com/37138188/126354124-fe328ee7-d2d4-403e-a395-21b3dadf98c5.png)

![image](https://user-images.githubusercontent.com/37138188/126354266-6c2451f4-51e8-481f-8033-2f58d965ff1a.png)

- 3 FFFF : BackUp Header
- 3 FFDE : BackUp Partition

---

[GPT 참고 블로그](https://c0msherl0ck.github.io/file%20system/post-GPT/)

---


# FAT32

FAT FILE ALLOCATE TABLE

0번 1번 클러스터는 존재하지 않는다.

![image](https://user-images.githubusercontent.com/37138188/126358297-ffcaf2ec-b1c5-4279-89e0-764e095ceb0d.png)

![image](https://user-images.githubusercontent.com/37138188/126355588-6e1df3d8-066b-4f7e-9e6f-f320b97b48c3.png)

---

**클러스터 크기가 작을수록**
- 장점 : 내부적 단편화가 적다.
- 단점 : 더 많은 FAT 엔트리가 필요하다.

**클러스터 크기 클수록**
- 장점 : FAT 엔트리 사용량이 적다.
- 단점 : 내부적 단편화가 심하다.

---

![image](https://user-images.githubusercontent.com/37138188/126355964-d23f403e-94e0-44a9-9ab2-74904974c06f.png)
![image](https://user-images.githubusercontent.com/37138188/126356031-5ecaf0b7-d92a-4550-bcd9-9e03d2374ad3.png)


Reserved Sector Count : 1EBE FAT Table이 여기서 시작함.

Byte Per Sector : 섹터 크기가 얼마인지 파악. 유심히 봐야함  
Sector Per Cluster : 클러스터의 크기가 결정.

Byte Per Sector 11위치 : 200이라서 512임  
Sector Per Cluster 13위치 : 2라서 1024

히든 섹터 28부터 4바이트 : 80  
토탈 섹터 32부터 4바이트 : 2 8000  
FAT 사이즈 36위치 4바이트 : 0261  

실제 데이터가 시작하는 곳 : Reserved Sector Count + FAT SIZE * Number of fats + Root dir sector(FAT32는 고려안해줘도 됨)
= 1B 3E + (261*2) = 8,129

8,192 * 512 = 40 0000(Hex) **이것은 2번 클러스터 위치**

---

FAT는 오직 파일 할당 데이터만 저장되어 있다.

그래서 메타데이터를 찾으려면 디렉토리 인포라는 곳으로 가야 정보를 얻을 수 있다.

---

디렉토리 엔트리 하나당 32바이트 크기

512/32 = 한 섹터당 16개의 엔트리를 가짐.

---

![image](https://user-images.githubusercontent.com/37138188/126356676-b3c2d6c8-b977-4955-9b8c-48332d614bee.png)

LFN(Long File Name) = Name 1 + Name 2 + Name 3

42이면 엔트리가 2개인다.

속성 0F이면 LFN
- Name 1은 1부터 10개
- Name 2는 14부터 12개
- Name 3는 28부터 4바이트

---

파일을 삭제할 때 Fat Table에 내가 쓰던 항목을 0으로 바꿔버린다.

Fat Table에서 삭제되면 정확한 파일의 클러스터 위치는 알기 어렵다.

But, 파일 사이즈 알고 클러스터 사이즈 아니까 연속적으로 할당되었다고 가정하면 어디부터 읽어야하는지 알 수 있다.

---

Fragment 된 파일의 복구는 힘들다.

---

[FAT32 참고 블로그][(](https://c0msherl0ck.github.io/file%20system/post-VBR/))

---