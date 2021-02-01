#  AWS-SAA 학습 정리-1



## Region

Geographical Area (each Region consists of 2(or more) Availability Zones) (지리적 영역)

## AZ

- Think of an Availability Zone as A Data Center
- isolated locations within each Region.
- Multiple

## Edge Locations

- Endpoints for aws which are user for caching content.
- typically this consists fo CloudFront, amazon's content Delivery Network

> Edge Locations > AZ's > Regions (갯수 기준)

## IAM Offers

- Centralised control of your AWS account (중앙 집중)
- Shared Access to your AWS account (공유 엑세스 권한)
- Granular Permissions (세분화 권한)
- Identity Federation (신원 제공)
- Multifactor Authentication (다중 인증)
- Provide temporary access for users/devices and services where necessary (임시 엑세스 제공)
- Allows you to set up your own password rotation policy (기간 주기로 패스워드 교체)
- Integrates with many different AWS services (다양한 aws 서비스 통합)
- Supports PCI DSS Compliance (framework)
- IAM is `universal` (지역 설정 x)
- `"root account"` is simply the account created when first setup your AWS account (처음 생성한 aws의 계정이 root 사용자)
- New Users have `No permissions` when first created (새 사용자 권한 없음)
- New Users are assigned Access Key ID & Secret Access Keys when first created (유저 생성시 엑세스키, 비밀 엑세스키 할당)
  - `These are not the same as a password`. you can't user the access Key ID & Secret Access Key to Login in to the console. (위에 두 키는 다르며 이를 통해 콘솔에 로그인 불가)
  - `You only get to view these once.` If you lose them, you have to regenerate them. so save them in a secure location(일회용으로 잃어버릴시 복구 불가)
- Always setup Multifactor Authentication on your root account(root 계정 MFA 인증 설정 -> 안정적 운영)

Identity and Access Management(식별 및 접근관리)라는 뜻으로 사용자 또는 사용자별 그룹을 생성하여 AWS의 각 리소스(자원)에 대해 제어 및 권한 관리를 제공하는 것을 말합니다. IAM은 실제 서비스를 제공하는 AWS 자체 리소스가 아니라 사용 요금을 발생하지 않습니다.

IAM의 기능을 예로 들자면 A라는 IAM의 설정된 사용자는 EC2만 관리할 수 있거나, 다른 AIM의 사용자는 S3의 내용만 읽을 수 있도록 구성할 수 있습니다. 개인 사용자와 달리 사용자 그룹은 동일한 권한을 여러 IAM 사용자에게 부여할 때 사용합니다.

![te](https://user-images.githubusercontent.com/48043799/105719346-87d2b200-5f65-11eb-8b14-45de1b8fe7b7.png)

> IAM Concept IMG



## IAM Terminology

- Group: A collection of users (permissions of the group)
  - 그룹 사용자의 권한 설정
- User: End Users such as people (employees)
  - 사용자 혹은 조직, 팀원
- Role: create roles & assign them to aws resources
  - 역할 생성 및 자원 할당
- Policies: Policy documents (JSON format) 
  - they give permissions as to what a user/group/role is able to do
  - 사용자, 그룹, 역할에 권한 추가 및 제거

## S3

- S3 is a safe place to `store your files` (파일 저장소)
  - 안전하고 가변적 object 저장공간 제공(간단한 웹 서비스 인터페이스)
- `Object-based` storage (객체 기반)
- data spread across multiple devices and facilities (여러 장치 분산 데이터)
- Files can be from `0Bytes ~ 5TB` (파일 저장 범위)
- unlimited storage and Files are stored in buckets (버킷에 저장되며 무제한)
- `universal namespace` (unique globally) (전역 네임스페이스)
- upload file to S3 -> receive a `HTTP 200 code` (success)

### S3 Objects 

- Key (simply name)
- Value (simply data & made up of a sequence of bytes) 
- Version ID (important versioning)
- Metadata (additional information)
- SubResouirces (Access Control Lists, Torrent)
  - CORS(Cross Origin Resource Sharing): 한 버킷의 파일을 다른 버킷에서 접근 가능하도록 하는 기능(다른 지역에서도 가능)

### Consistency work for S3 (데이터 일관성)

- Read after write consistency for PUTS of new Objects 
  - S3 버킷에 **업로드한다면 즉시 바로 사용**할 수 있다는 의미
- Eventual Consistency  for overwrite PUTS and DELETES 
  - 버킷의 내용을 **수정(덮어쓰기)하거나 삭제할시** 복제하는데 시간이 걸리는 의미

> if you write a new file and read it immediately afterwards you will be able to view that data. (새 파일 업로드시 즉시 파일을 read 가능)
>
> if you update an existing file or delete a file and read it immediately you may get the older version, or you may not. basically changes to objects can take a little bit of time to propagate (기존 파일을 덮어쓰기 또는 삭제한다면 이전 버전의 파일 또는 아예 없는 경우도 발생하며 기본적으로 객체의 변경사항은 약간의 시간이 소요)

### S3 features

- Tiered Storage Available
- Lifecycle Management
- Versioning
- Encryption
- MFA Delete
- Secure your data using Access Control Lists and Bucket Policies

## S3 Storage Classes

### S3 Standard (default)

- 99.99% availability
- stored redundantly across multiple devies in multiple facilities, and is designed to sustain the loss of 2 facilities concurrently.





## Cloud watch

AWS 리소스 사용의 실시간 모니터링을 지원합니다.

모니터링 및 감시하는 방법으로 청구에 따른 경보를 지정할 수 있으며, 다양한 이벤트를 로그파일로 저장할 수 있으며 경보 설정을 통해 SNS, lambda로 전송이 가능합니다.

CloudWatch를 사용 가능한 서비스로는 EC2, RDS, S3, ELB등이 있습니다.

# 실습

## Cloud Watch

알람은 지역을 버지니아 북부로 설정해야 지정이 가능하며 다음과 같이 설정할 수 있습니다.

- CloudWatch -> Billing -> Create alarm button -> Select metric -> 모든지표 탭 -> 예상 요금 합계 -> 통화선택

### 모니터링 종류

- basic -> default
  - 무료
  - 5분 간격 지표 제공
- detailed
  - 유료
  - 1분 간격 지표 제공

사용하는 예로는 다음과 같습니다.

- use case: 매일 얼마나 많은 사용자들이 서비스를 사용하는지 
- potential issue: 특정한 날에 많은 트래픽이 몰려 병목현상이 생길 수 있는 부분을 예측
- solution: 매일 평균 트래픽과 특정 버튼의 평균 유저의 클릭 횟수를 분석하여 효율적인 서버관리가 가능

### 조건

정적(static) 또는 대역(이상탐지)을 사용할지 유형을 지정할 수 있습니다. 해당 조건에 따른 비교연산자를 통해 추가할 수 있습니다.

<img width="766" alt="스크린샷 2021-01-26 오후 11 26 52" src="https://user-images.githubusercontent.com/48043799/105857810-fda25080-602d-11eb-8b10-296364c60487.png">

> 이후 다음화면에서 알람의 이름과 설명을 입력하면 프리뷰를 확인할 수 있고
>
> 마지막으로 생성버튼을 누르면 알람 생성이 완료됩니다 :)

![image](https://user-images.githubusercontent.com/48043799/105858302-7ef9e300-602e-11eb-8457-7f9b9c1f3083.png)



### S3 생성

1. aws 서비스 -> S3 클릭 -> 버킷 만들기 버튼
2. 일반 구성
   1. 버킷 이름 작성
   2. 리전(지역) 선택(기존 버킷 설정을 복사할 수 있음)
3. 퍼블릭 액세스 차단을 위한 버킷 설정
   1. default 설정만으로도 보안 최적화
4. 버전관리
   1. 활성화 및 비활성화
5. 태그 관리
6. 서버측 암호화
7. 생성 버튼

![image](https://user-images.githubusercontent.com/48043799/106003432-8afca800-60f5-11eb-8acd-c271a1234865.png)

> S3 생성 완료 :)



## S3 상세페이지

![image](https://user-images.githubusercontent.com/48043799/106003565-a9fb3a00-60f5-11eb-8652-cf746fd7ec7d.png)

<br>

### 객체 : 버킷에 넣을 파일

- 업로드 -> 파일 추가 -> 업로드버튼 -> 나가기 -> 객체 리스트 확인

![image-20210127231905625](/Users/lj/Library/Application Support/typora-user-images/image-20210127231905625.png)

이후 위에 업로드된 파일을 누르면 아래와 같이 S3에 업로드된 파일에 대한 정보를 확인할 수 있습니다.

객체 URL을 통해 파일을 확인할 수 있지만 경로로 이동하게 되면 AccessDenied라는 에러를 띄우게 됩니다. 이는 접근 금지에 대한 에러이며 파일에 접근할 권한이 없기때문에 발생하는 현상입니다. 

![image](https://user-images.githubusercontent.com/48043799/106005156-440fb200-60f7-11eb-844c-d7ecf6e70127.png)

해당 파일의 상세페이지에 접근하여 객체 작업 -> 퍼블릭으로 설정으로 제한을 풀면 되지만 이는 버킷의 권한이 모든 부분에서 차단되었기에 해당 권한을 우선적으로 설정을 변경해줘야합니다.

**권한** 탭을 눌러 편집 -> 모든 퍼블릭 액세스 차단을 체크해제 후 -> 저장

이후 다시금 업로드된 파일 상세페이지에 접근하여 객체 작업 -> 퍼블릭으로 설정 -> 이후 객체 URL에 접근한다면 정상적으로 이미지가 보이는 것을 확인할 수 있습니다.

### S3의 버킷 특징

버킷은 동일한 이름을 가질 수 없는 특징을 가지고 있습니다. 따라서 고유한 이름을 지정해야하며 버킷 자체는 글로벌하게 조회가 가능하지만 실제 버킷을 생성시 개별 지역에서 교차를 통해 한쪽 버킷의 파일 및 데이터를 다른 버킷에 자동으로 복제할 수도 있습니다.

예를 들어 서울지역의 S3 버킷을 미국 버지니아 북부의 S3로 복제할 수 있으며 동시에 객체의 스토리지클래스 및 암호화도 수정이 가능합니다. 이를 CORS의 예로 들 수 있습니다.

마지막으로 버킷 액세스를 제한하는 방법으로는 총 3가지가 있습니다.

- 버킷 정책 사용 (전체 버킷에 적용)
- 객체 정책을 사용하여 제어 (ACL)
- 계정내 사용자 그룹의 정책으로 제어

### [S3 요금](https://aws.amazon.com/ko/s3/pricing/)

![image](https://user-images.githubusercontent.com/48043799/106135815-c5c11780-61ab-11eb-8902-a33cc7419f94.png)

### 적합한 S3 버킷 사용 방법 (아래로 갈수록 절약)

- S3 Standard
- S3- IA
- S3 - Intelligent Tirering
- S3 One Zone - IA
- S3 Glacier
- S3 Glacier Deep Archive

## S3 암호화

파일 업로드/다운로드시

- SSL/TLS -> aws 내부적으로 암호화
  - 서버측, 클라이언트측에서 지원할 수 있으며 서버측은 아마존이 객체 암호화를 클라이언트측은 객체를 암호화 후 S3에 업로드합니다.

default 아무런 동작하지 않을시 (서버측 유형)

- SEE-S3: aws에서 자동으로 키관리 
- SSE-KMS: 키관리 서비스
- SSE-C: 고객이 제공한 키를 사용해 서버측 암호화 수행

![image](https://user-images.githubusercontent.com/48043799/106011918-432e4e80-60fe-11eb-9749-7ee3072bd3a8.png)

> 파일 자체를 할때는 파일 상세페이지 -> 서버측 암호화 설정 접근
>
> 버킷 자체를 할때는 버킷 상세페이지 -> 속성 -> 기본 암호화 -> 편집 접근

![image](https://user-images.githubusercontent.com/48043799/106012341-a91ad600-60fe-11eb-851e-97998281d4a1.png)



## 버전관리

모든 객체의 버전을 저장하고 객체를 삭제하더라도 모든 권한을 aws 콘솔에 로그인시 확인할 수 있습니다. (즉 스냅샷과 비슷한 의미)

버전 관리에서는 MFK 삭제 기능도 제공되는데 이는 기본적으로 추가 인증을 사용하는 것으로 실수로 객체를 삭제하는 것을 막기 위한 보안 기능입니다.

버전관리를 활성화 시키는 방법은 버킷 생성시 **버킷 버전 관리** 부분에서 가능합니다.



## 수명주기관리 규칙

서로 다른 스토리지 계층간 객체 이동을 자동화 할 수 있으며 버전관리와 함께 사용할 수 있으며 관리탭에서 사용 가능하며 하나 이상의 규칙을 사용하여 규칙 범위를 제한할 수 있습니다.

- 스토리지 클래스 간 객체 현재 버전 전환
  - 체크 후 기간 일 범위 입력
- 스토리지 클래스간 객체 이전 버전 전환
  - 체크 후 기간 일 범위 입력
- 현재 버전 만료



## CloudFront

콘텐츠 전송 네트워크라 불리는 서비스입니다. 사용자의 지역 위치 기반으로 웹페이지 및 기타 웹 콘텐츠를 제공합니다. 예를 들어 런던에 호스팅할 웹사이트가 전세계를 대상으로 서비스한다고 했을때 런던에 위치한 서버를 통해 콘텐츠와 파일을 내려받게 됩니다. 이는 속도나 파일을 주고받는데 있어서 매우 비효율적인 방법이기 때문에 엣지로케이션(콘텐츠 캐시 위치)을 통해 클라우드 프론트 서비스를 적용할 수 있습니다. 예시는 아래와 같습니다.

> 1. 런던에 웹서버가 존재
> 2. 전 세계에서 사용자가 접근하며 엣지로케이션도 존재
> 3. A라는 사용자가 엣지로케이션에 대한 쿼리를 수행 또는 비디오 파일 요청 (캐싱 여부 확인)
> 4. 해당 위치에 사본이 없을시 원본 서버로 비디오를 다운로드 요청, 요청이 끝난 후 엣지 서버에 캐싱 처리와 동시에 응답
> 5. 이후 접근시 캐시가 되어진 위치로 우선 접근하여 있는지 확인후 존재한다면 캐시데이터로 처리, 아니라면 다시 원본 서버로 접근 



## 요약

- 정책은 지역에 적용되지 않습니다.
- root 계정은 aws 처음 설정시 생성된 계정으로 완전한 관리자 권한을 가지고 있습니다.
- 새 사용자는 처음 생성시 권한이 존재하지 않습니다.
  - 새 사용자를 생성시 해당 사용자에게 권한을 부여해야합니다.
- S3를 볼때 버킷을 생성시 잠겨있으므로 해당 객체를 공개헤야 접근이 가능합니다.
- 새 사용자에게는 access key와 ID 보안 access key가 할당되는데 이는 로그인때 사용하는 것이 아니라 API와 커맨드 명령으로 aws에 접근할때만 사용합니다.
- 또한 사용자를 위한 암호 정책을 생성하고 이를 지정할수도 있습니다.
- S3는 객체 기반 서비스입니다.
- S3는 파일은 최대 5TB까지 업로드 가능하며 버킷이라는 곳에 파일을 저장합니다.
- S3의 버킷 이름은 고유한 이름을 사용해야하며 업로드 성공시 200 상태코드를 리턴합니다.
- S3 기본 생성시 default로 버킷은 비공개입니다.
- S3 버킷은 버킷 정책을 사용하여 액세스 제어를 설정할 수 있으며 버킷단위가 아닌 파일 개별적으로도 지정이 가능합니다.
- S3 버킷은 액세스 로그를 생성할 수 있으며 aws계정내에 A라는 버킷에서 B 버킷으로 전송할 수 있습니다.
- S3 스토리지 클래스중 S3 standard는 드물게 접근합니다.
  - S3 Standard > IA > One Zone IA > Intelligent Tiering > Glacier > Glacier Deep Archive





## References

- https://www.inflearn.com/course/aws-%EC%9E%85%EB%AC%B8
- https://www.udemy.com/course/aws-certified-solutions-architect-associate/learn/lecture/13886244#overview
- http://pyrasis.com/book/TheArtOfAmazonWebServices/Chapter16