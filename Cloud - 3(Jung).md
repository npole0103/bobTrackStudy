# EC2 생성 - Web / Cli

AWS EC2 생성

---

## Web에서 EC2 생성하기
###  인스턴스 시작
1. AMI(Amazon Machine Image) 선택 - Ubuntu20.04 Server
2. 인스턴스 유형 선택 - 프리티어
3. 인스턴스 세부 정보 구성 - Default
4. 스토리지 추가 - Default
5. 태그 추가 - 키 : Name, 값 : BoB10@ProductDev.8756
6. 보안그룹 할당 - 새 보안 그룹 : BoB10@ProductDev.8756 / 설명 : BoB10@ProductDev.8756
7. 키 페어 선택 - **키페어 꼭 다운로드 해야함**

**[EC2 SSH 연결 Putty에서 하는 법](https://mozi.tistory.com/191)**

#### Port추가
좌측 메뉴바 보안그룹 -> 본인 보안그룹 찾기 -> 규칙 추가

### EC2 사용자 데이터 작성 후 서비스 자동 실행

인스턴스 생성 시 세부 정보 구성 - 고급 세부 정보 - 사용자 데이터

``` bash
#!/bin/bash
sudo apt update -y && sudo apt upgrade -y
sudo apt-get install python3.7 -y
sudo apt install python3-pip -y
cd /home/ubuntu/
git clone https://github.com/SeungGiJeong/lecture-aws-ec2.git 
pip3 install -r /home/ubuntu/lecture-aws-ec2/requirements.txt
python3 /home/ubuntu/lecture-aws-ec2/manage.py &
```

### EC2 볼륨 확장 또는 수정

좌측 메뉴바 Elastic Block Store -> 볼륨 -> 작업 -> 볼륨 수정

### EC2 삭제

인스턴스 종료가 EC2 삭제임

---

## CLI로 EC2 생성하기

``` bash
#!/bin/bash

#VPC
## Create VPC
aws ec2 --profile lecture create-vpc --cidr-block 10.8.0.0/16
aws ec2 --profile lecture describe-vpcs --query "Vpcs[?CidrBlock == '10.8.0.0/16'].VpcId"

# Set the vpcid in env
vpcid=$(aws ec2 --profile lecture describe-vpcs --query "Vpcs[?CidrBlock == '10.8.0.0/16'].VpcId" --output text)

echo "------------------VPC-----------------"

# Availability Zone
aws ec2 --profile lecture describe-availability-zones --query "AvailabilityZones" | jq -r ".[0].ZoneId"
azid1=$(aws ec2 --profile lecture describe-availability-zones --query "AvailabilityZones" | jq -r ".[0].ZoneId")

echo "------------------AZ-----------------"

# subnet
## Create Subnet in VPC
aws ec2 --profile lecture create-subnet --vpc-id $vpcid --cidr-block 10.8.0.0/24 --availability-zone-id $azid1
aws ec2 --profile lecture describe-subnets --query "Subnets[?VpcId=='$vpcid'] | [?starts_with(CidrBlock, '10.8.0')]" | jq -r ".[0].SubnetId"

## Set the subnet ID
subnetid1=$(aws ec2 --profile lecture describe-subnets --query "Subnets[?VpcId=='$vpcid'] | [?starts_with(CidrBlock, '10.8.0')]" | jq -r ".[0].SubnetId")

echo "------------------SUBNET-----------------"

#Gateway

## Create Internet Gateway
aws ec2 --profile lecture create-internet-gateway
aws ec2 --profile lecture describe-internet-gateways --query "InternetGateways[?Attachments[0].State==null]" | jq -r ".[0].InternetGatewayId"
igwid=$(aws ec2 --profile lecture describe-internet-gateways --query "InternetGateways[?Attachments[0].State==null]" | jq -r ".[0].InternetGatewayId")

aws ec2 --profile lecture attach-internet-gateway --vpc-id $vpcid --internet-gateway-id $igwid
aws ec2 --profile lecture describe-internet-gateways --query "InternetGateways[?Attachments[0].VpcId=='$vpcid']" | jq -r ".[0].InternetGatewayId"
igwid=$(aws ec2 --profile lecture describe-internet-gateways --query "InternetGateways[?Attachments[0].VpcId=='$vpcid']" | jq -r ".[0].InternetGatewayId")

echo "-------------------Gateway-----------------"

#Route table

aws ec2 --profile lecture create-route-table --vpc-id $vpcid
aws ec2 --profile lecture describe-route-tables --query "RouteTables[?VpcId=='$vpcid'] | [?Associations[0].Main==null]" | jq -r ".[].RouteTableId"
user_rtableid=$(aws ec2 --profile lecture describe-route-tables --query "RouteTables[?VpcId=='$vpcid'] | [?Associations[0].Main==null]" | jq -r ".[].RouteTableId")

aws ec2 --profile lecture create-route --route-table-id $user_rtableid --destination-cidr-block 0.0.0.0/0 --gateway-id $igwid

echo "------------------Route-----------------"

#Subnets
## Attach the subnetid1 and rtableid at one EC2

aws ec2 --profile lecture associate-route-table --subnet-id $subnetid1 --route-table-id $user_rtableid
aws ec2 --profile lecture modify-subnet-attribute --subnet-id $subnetid1 --map-public-ip-on-launch
aws ec2 --profile lecture describe-route-tables --query "RouteTables[?VpcId=='$vpcid'] | [?Associations[0].SubnetId=='$subnetid1']" | jq -r ".[0].Associations[0].RouteTableAssociationId"

user_rtable_aid1=$(aws ec2 --profile lecture describe-route-tables --query "RouteTables[?VpcId=='$vpcid'] | [?Associations[0].SubnetId=='$subnetid1']" | jq -r ".[0].Associations[0].RouteTableAssociationId")

echo "------------------SUBNET-----------------"

sshkeyname=BoB10@ProductDev.8756
# SSH Key generate

echo "------------------KEY GENERATE-----------------"

# AMI
ami_id=ami-04876f29fd3a5e8ba

echo "------------------AMI ID-----------------"

# Security Group
aws ec2 --profile lecture create-security-group --group-name BoB10@ProductDev.cli.8756 --description BoB10@ProductDev.cli.8756 --vpc-id $vpcid
aws ec2 --profile lecture describe-security-groups --query "SecurityGroups[?VpcId=='$vpcid'] | [?contains(Description, 'BoB10@ProductDev.cli.8756')]"

## Set sg_id
sg_id=$(aws ec2 --profile lecture describe-security-groups --query "SecurityGroups[?VpcId=='$vpcid'] | [?contains(Description, 'BoB10@ProductDev.cli.8756')]" | jq -r ".[0].GroupId")

echo "------------------Security Group-----------------"

## Set sg_id to EC2 group with NACL
aws ec2 --profile lecture authorize-security-group-ingress --group-id $sg_id --protocol tcp --port 22 --cidr 0.0.0.0/0

aws ec2 --profile lecture run-instances --image-id $ami_id --count 1 --instance-type t2.micro --key-name $sshkeyname --security-group-ids $sg_id --subnet-id $subnetid1 --tag-specifications 'ResourceType=instance, Tags=[{Key=Name, Value=BoB10@ProductDev.cli.8756}]' --user-data file://./userdata.txt
aws ec2 --profile lecture run-instances --image-id $ami_id --count 1 --instance-type t2.large --key-name $sshkeyname --security-group-ids $sg_id --subnet-id $subnetid1 --tag-specifications 'ResourceType=instance, Tags=[{Key=Name, Value=BoB10@ProductDev.cli.8756}]' --user-data file://./userdata.txt
echo "------------------SUCCESS-----------------"

```

---
