## RDS - Relational DB Service
> 여러 관계형 데이터 베이스를 서비스로서 제공   
> MS-SQL, Oracle, MySQL, Postgre, Aurora, MariaDB

## Data Warehousing
* Business Intelligence
* 리포트 작성, 데이터 분석시 사용 (Production Database -> Data Warehousing)
* 매우 방대한 분량의 데이터 로드시 사용 (트랜잭션 프로세싱이 적합하지 않다)

## OLTP VS OLAP
* OLTP : INSERT와 같이 종종 사용되어지는, 혹은 규모가 작은 데이터를 불러올 때 사용되는 SQL 쿼리가 필요할 떄 유용
    - ex) Order #210에만 해당되는 customer 이름, 주소, 시간 정보 INSERT
* OLAP : 매우 큰 데이터를 불러올 때 사용. 주로 덩치가 큰 SELECT 쿼리가 사용됨 - 트랜잭션 처리하지 않음
    - ex) 특정 회사 부서의 Net Profit, Products

### RDS - Database Backup
* Automated Backups(AB)
    1. Retention Period(1-35일) 안의 어떤 시간으로 돌아가게 할 수 있음 (Point In Time 기능-PIT)
    2. AB는 그날 생성된 스냅샷과 Transaction logs(TL)을 참고함
    3. 디폴트로 AB기능이 설정되어 있으며 백업 정보는 S3에 저장
    4. AB동안 약간의 I/O suspension이 존재할 수 있음 -> Latency
* DB Snapshots
    1. 주로 사용자에 의해 실행됨
    2. 원본 RDS Instance를 삭제해도 스냅샷은 존재함 (vs AB- 인스턴스 삭제시 복구 불가)

* 데이터베이스 백업
    - original -> restored로 백업
        - 1. 새로운 RDS Instance
        - 2. 새로운 RDS Endpoint

### Multi AZ
* 원래 존재하는 RDS DB에 무언가 변화(write, update, delete)가 생길 때 다른 AZ에 똑같은 복제본이 만들어짐 = Synchronize
* AWS에 의해서 자동으로 관리가 이루어짐 (No admin intervention)
* 원본 RDS DB에 문제가 생길 시 자동으로 다른 AZ의 복제본이 사용됨
* 오직 재해 복구를 위한 방식, 성능 개선을 위해서 사용하지 않음.

### Read Replica
* Production DB의 읽기 전용 복제본이 생성됨
* 주로 Read-Heavy DB 작업시 효율성의 극대화를 위해 사용됨 (Scaling)
* 재해복구 용도가 아니다.
* 최대 5개 Read Replica DB 허용
* Read Replica의 Read Replica 생성 가능 (단, Latency 발생)
* 각각의 Read Replica는 자기만의 고유 Endpoint 존재

### ElastiCache
* 클라우드 내에서 In-memory 캐시를 만들어줌
* 데이터베이스에서 데이터를 읽어오는 것이 아니라 캐시에서 빠른 속도로 데이터를 읽어옴
* Read-Heavy 어플리케이션에서 상당한 Latency 감소 효과를 누림
* 종류 
    - Memcached
        - Object 캐시 시스템으로 잘 알려져 있음
        - ElastiCache는 Memcached의 프로토콜을 디폴트로 따른다
        - EC2 Auto Scaling처럼 크기가 커졌다 작아졌다 가능함
        - 오픈소스
        - 사용례 : 가장 단순한 캐싱 모델이 필요할 때, Object caching이 주된 목적일 때, 캐시 크기를 마음대로 scaling하기를 원할 때.
    - Redis
        - Key-Value, Set, List와 같은 형태의 데이터를 In-Memory에 저장 가능함
        - 오픈 소스
        - Multi-AZ 지원(재해복구)
        - 사용례 : List, Set과 같은 데이터셋을 사용할 때, 리더보드처럼 데이터셋의 랭킹을 정렬하는 용도가 필요할 때, Multi-AZ기능을 사용할 때.
            