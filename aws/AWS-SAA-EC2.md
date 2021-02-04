# AWS-SAA 학습 정리-2



## EC2

- ### **Elastic Compute Cloud**

- Provides resizable compute allowing you to quickly scale capacity 

  - 확장 가능한 resize 컴퓨팅 용량 제공

- Reduces the time required to obtain boot new server instances to minutes 

  - 새 인스턴스 가져오는데 분단위

- ### **On Demand**

  - pay a fixed rate by the hour with no commitment (인스턴스를 실행한 시간만큼 지불)
  - applications with short term spiky, or unpredictable workloads that can't be interrupted (중단 x, 예측 불가한 워크로드가 존재하는 애플리케이션에 적합)
  - applictions being developed or tested 

- ### **Reserved** 

  -  provides a capacity reservation, offer a significant discount on the hourly charge for an instance (용량 예약 가능 및 해당 인스턴스의 시간당 요금 할인, 기간은 1~3년)
  - steady state or predictable usage (예약은 안정된 상태 및 예측 가능할때 적합)
  - able to make upfront paymnets to reduce (비용 절감을 위한 선불결제)
    - `Standard`
      - offer up to 75%
      - the more upfront the longer the contract the greater the discount
    - `Convertible`
      - offer up to 54%
      - allows you to change between your different instance types
    - `Scheduled`
      - have scheduled reserved instances and these are available to launch within the time windows

- ### **Spot**  

  - enables you to bid whatever price youwant for instance capacity, providing for even greater savings if you applications have flexible start and end times (시작, 종료시간이 유연할시 큰 절감 효과, 효율적 비용)
  - flexible start and end times (유연한 시작, 끝시간)
  - only feasible at very low compute pirces (매우 낮은 컴퓨팅 가격으로 운용시)

- ### **Dedicated Hosts** 

  - physical EC2 server dedicated for your use (사용자 전용 물리 EC2 서버)
  - greate for licensing which doesn't support multi-tenancy or cloud deploy (클라우드를 배포 또는 테넌트 가상화 지원 안하는 라이센스에 적합)  
  - reservation for up to 70% the on-Demand pirce

## EC2 Instance Types

![image](https://user-images.githubusercontent.com/48043799/106768616-6cf7f000-667f-11eb-8853-681f46ce83e0.png)

> if the spot instance is terminated by amazon ec2, you will not be charged for a partial hour of usage. (ec2에 의해 종료되는 경우 요금 부과 x)
>
> however if u terminate the instance yourself, you will be charged for any hour in which the instance ran (유저가 직접 종료시 실행시간에 대한 요금 부과)



## EC2 Launch

- termination protection is **turned off by default**, you must turn it on (종료 방지 기능은 default -> off)
- on an EBS-backed instance, the **default action is for the root EBS** volume to be deleted when the instance is terminated (EBS 지원 인스턴스 default -> 인스턴스 종료시 root EBS 볼륨 삭제)
- EBS Root Volumes of Default AMI's **Can** be encrypted (AMI 루트 볼륨 암호화 가능)
- additional volumes can be encrypted (추가 볼륨 암호화 가능)



## EC2 콘솔 메뉴

### Description (설명)

- 종료 방지 -> Termination protection = True (on)
- public DNS 주소 확인 가능

### Status Checks (상태)

- 시스템 확인, 인스턴스 확인

### Monitoring

- Cloud Watch를 통해 자세한 사항 확인
- CPI 상태, 네트워크등 확인

### Tag

- EC2 생성시 설정했던 내용 확인

### Actions

- EC2 서버 연결
- 인스턴스 상태 변경(start, stop, reboot, terminate)
- Instance Settings - 인스턴스 설정 변경
  - edit tag
  - auto scaling
  - add role
  - change termination protection

## EC2 Tips

- Termination Protection is turned off by default, you must turn it on
  - 기본적으로 종료방지 기능은 꺼져있고, 실행시 켜야함
- On an EBS-backed instance, the default action is for the root EBS volume to be deleted when the instance is terminated
  - EBS 인스턴스는 종료시 Root EBS 볼륨 삭제



## Quiz

Q1. If an Amazon EBS volume is the root device of an instance, can I detach it without stopping the instance?

a. Yes but only if Windows instance
b. No
c. Yes
d. Yes but only if a Linux instance



Q2. 한 회사가 예약 인스턴스를 사용하여 데이터-처리 워크로드를 실행한다. 야간 작업은 보통 실행에 7 시간이 걸리며 10 시간 내에 완료되어야만 한다. 이 회사는 매월 말 일시적인 수요 증가가 예상되며 현재의 자원 용량으로는 이 작업의 시간 제한 초과 원인이 될 것이다. 처리 작업은 일단 시작되면 완료되기 전에 중단될 수 없다. 이 회사는 가능한 한 비용-효율적으로 용량을 늘릴 수 있는 솔루션을 구현하고 싶어한다. 어떤 것을 솔루션 아키텍트가 해야하는가? 

a. 수요가 많은 기간 동안 온디맨드 인스턴스를 배포한다.
b. 추가적인 인스턴스를 위해 두 번째 Amazon EC2 예약을 생성한다.
c. 수요가 많은 기간 동안 스팟 인스턴스를 배포한다.
d. 증가된 워크로드의 지원을 위해 Amazon EC2 예약에서 인스턴스의 인스턴스 크기를 늘린다.



Q3. 한 회사의 보안 팀은 클라우드에 저장된 모든 데이터가 온프레미스에 저장된 암호화 키를 사용하여 항상 암호화될 것을 요구한다. 어느 암호화 옵션이 이러한 요구사항을 충족하는가? (2개  선택)

a. Amazon S3 관리형 키(SSE-S3)의 서버 측 암호화를 사용한다.
b. AWS KMS 관리형 키(SSE-KMS)의 서버 측 암호화를 사용한다.
c. 고객 제공 키(SSE-C)의 서버 측 암호화를 사용한다.
d. 클라이언트 측 암호화를 사용하여 저장 중 암호화를 제공한다. 
e. Amazon S3 이벤트에 의해 구동되는 AWS Lambda 함수로 고객 키를 사용해 데이터를 암호화한다.

>  Answer
>
> Q1: b
>
> Q2: a
>
> Q3: c, d

## References

- https://www.inflearn.com/course/aws-%EC%9E%85%EB%AC%B8
- https://www.udemy.com/course/aws-certified-solutions-architect-associate/learn/lecture/13886244#overview
- http://pyrasis.com/book/TheArtOfAmazonWebServices/Chapter1s