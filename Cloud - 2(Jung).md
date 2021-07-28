# Clude 

---

## S3 시작

[S3 시작](https://console.aws.amazon.com/console/home?region=ap-northeast-2#)

---

## 버킷 만들기

[버킷 만들기](https://console.aws.amazon.com/s3/home?region=ap-northeast-2) : 리포지토리 개념이라고 생각하면 될듯하다.

### 권한 설정
버킷 생성 시
- Private 버킷이라면? **권한 - 모든 퍼블릭 엑세스 차단**
- Public 버킷이라면? **권한 - 모든 퍼블릭 엑세스 차단 비활성화**

### 버킷 버전 관리
활성화

### 기본 암호화
비활성화

---

## Web에서 객체 업로드

파일 추가 / 폴더 추가로 가능

권한 관리 - 미리 정의된 ACL
- 프라이빗
- 퍼블릭 읽기 엑세스 권한 부여

---

## S3 Command in Ubuntu

`aws --profile lecture s3 ls` : S3에 있는 디렉토리 목록 확인

`aws --profile lecture s3 ls --recursive` : S3에 있는 디렉토리 목록 Recursive 하게 폴더 안에 있는 것까지 확인 가능

`aws s3 --profile lecture cp backup s3://bob-s3-directorylisting/backup –recursive`
- backup은 로컬에 있는 폴더임
- backup이 FROM / S3가 TO 이므로 backup에 있는 파일들이 S3로 가는 구조임.

`aws s3 --profile lecture sync backup s3://bob-s3-directorylisting/backup --exclude '*.tmp'` : .tmp 확장자를 제외하고 로컬에 있는 backup 폴더 내용 모두 업로드

`aws s3 --profile lecture rm s3://bob-s3-directorylisting --recursive --exclude "*.sh"` : .sh 확장자를 제외하고 S3에 있는 것들 모두 삭제

`aws --profile lecture s3 mb s3://bob-new` : bob-new 라는 버킷을 새로 생성

`aws s3 --profile lecture mv s3://mybucket s3://mybucket --recursive` : mybucket에 있는 것들 mybucket으로 이동

`aws s3 --profile lecture mv s3://mybucket/test.txt s3://mybucket/test2.txt --acl public-read-write` : test1.txt 파일을 test2.txt 파일로 만듦. public-read-write 모드로

`aws s3 --profile lecture mv file.txt s3://mybucket/ --grants read=uri=http://acs.amazonaws.com/groups/global/AllUsers` : 모든 유저한테 공개?

`aws s3 rb s3://bob-s3-directorylisting --force` : 버킷 삭제 (빈 버킷만 삭제 가능)

---







