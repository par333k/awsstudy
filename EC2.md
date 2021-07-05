## EC2
> Elastic Compute Cloud (EC2) - 유연한 크기의 컴퓨팅 자원 제공
* 사용량에 따라 컴퓨팅 자원을 탄력적으로 운영할 수 있는 서비스
* 지불 방법
    - On-demand : 시간 단위로 가격이 고정되어 있음
        - 오랜 시간 동안 선불을 내지 않고 최소한의 비용을 지불하여 EC2 인스턴스를 사용하고 싶을 때,
        특히 앱/프로그램 개발시 최초로 EC2 인스턴스에 deploy할때 매우 유용
    - Reserved : 한정된 EC2 용량 사용 가능, 1-3년동안 시간별로 할인 적용 받을 수 있음
        - 안정된, 예상 가능한 workload시 Reserved 사용 권장, 선불로 인한 컴퓨팅 비용 대폭 감소
    - Spot : 입찰 가격 적용. 가장 큰 할인율을 적용받으며 특히 인스턴스의 시작과 끝 
     기간이 전혀 중요하지 않을 때 매우 유용
        - 단순히 비용 절감 시 유용함. 인스턴스의 시작/끝 시점에 구애받지 않을 경우 권장.(경매식)

## EBS
> EC2를 사용하기 위해 EBS라는 디스크(일종의 HDD/SDD 역할)를 사용
* 저장 공간이 생성되어지며 EC2 인스턴스에 부착된다
* 디스크 볼륨 위에 File System이 생성된다
* EBS는 특정 Availability Zone에 생성된다.
    - Availability Zone: 가용영역, 재해복구 목적으로 사용. 한 리전에 여러 AV가 존재.
* EBS 볼륨 타입
    - SSD
        1. General purpose SSD(GP2) : 최대 10K IOPS를 지원하며 1GB당 3IOPS 속도가 나옴
        2. Provisioned IOPS SSD(I01) : 극도의 I/O률을 요구하는(매우 큰 DB 관리 등) 환경에서 사용.
        10K 이상의 IOPS를 지원함.
    - 마그네틱 / HDD
        1. Throughput Optimized HDD(ST1) : 빅데이터 Datawarehouse, Log 프로세싱시 주로 사용 (부트 볼륨 사용 불가)
        2. CDD HDD(SC1) : 파일 서버와 같이 드문 volume 접근시 주로 사용, 역시 boot volume으로 사용 불가능, 비용 매우 저렴
        3. Magnetic(Standard) : 디스트 1GB당 가장 싼 비용을 자랑. Boot volume으로 유일하게 사용 가능함.

## ELB
> Elastic Load Balencers
* 수많은 서버의 흐름을 균형있게 흘려보내는데 중추적인 역할을 함
* 하나의 서버로 traffic이 몰리는 병목현상 방지
* Traffic의 흐름을 Unhealthy instance -> healthy instance로
1. Application Load Balancer : OSI Layer7에서 작동됨
    - HTTP, HTTPS와 같은 traffic의 load balancing에 가장 적합함
    - 고급 request 라우팅 설정을 통하여 특정 서버로 request를 보낼 수 있음.
2. Network Load Balancer : OSI Layer4에서 작동됨, 매우 빠른 속도를 자랑하며 Production환경에서 종종 쓰임
    - 극도의 performance가 요구되는 TCP traffic에서 적합함
    - 초당 수백만개의 request를 아주 미세한 delay로 처리 가능
3. Classic Load Balancer : 현재는 Lagacy로 간주됨, 따라서 거의 쓰이지 않음.
    - Layer7의 HTTP/HTTPS 라우팅 기능 지원
    - Layer4의 TCP traffic 라우팅 기능도 지원

> Load Balancer Error : 504 ERROR 반환   
> X-Forwarded-For 헤더
- public IP address ->(DNS)-> ELB(private IP address) -> EC2 
    - EC2는 private IP만 접근가능, 따라서 public ip를 알려면 X-Forwarded-For 헤더 값을 참고해야함.

## Route53
> AWS에서 제공하는 DNS 서비스
* EC2 Instance
* S3 Bucket
* Load Balancer
