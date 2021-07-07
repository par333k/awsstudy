## DynamoDB
* NoSQL(Not Only SQL) 데이터베이스
* 매우 빠른 쿼리 속도
* Auto-Scaling 기능 탑재
* Key-Value 데이터 모델 지원
* 테이블 생성시 스키마 생성 필요 없음
* 모바일, 웹, IoT데이터 사용시 추천됨
* SSD 스토리지 사용

### DynamoDB의 구성
- 테이블 (Table)
- 아이템 (Items) - 행(row)과 개념이 비슷함
- 특징 (Attributes) - 열(column)과 개념이 비슷함
- Key-Value (Key: 데이터의 이름, Value: 데이터 자신)
    - 예) JSON, XML

### DynamoDB의 Primary Key(PK)
- PK를 사용하여 데어터 쿼리
- DynamoDB에는 두가지의 PK 유형이 있음
    - 파티션키(Partition Key)
        - 고유 특징(Unique Attribute)
        - 실제 데이터가 들어가는 위치를 결정해줌
        - 파티션키 사용시 동일한 두개의 데이터가 같은 위치에 저장될 수 없음
    - 복합키 (Composite Key)
        - 파티션키(Partition Key) + 정렬키(Sort Key)
            - 예시: 똑같은 고객이 다른 날짜에 다른 물건을 구매
                - 파티션키는 한 고객으로 일치하나 정렬키는 날짜가 달라서 별개
                - 같은 파티션키의 데이터들은 같은 곳에 저장되며 정렬키에 따라 정렬

### DynamoDB 데이터 접근 관리
- AWS IAM으로 관리할 수 있음
    - 테이블 생성과 접근 권한을 부여할 수 있음
    - 특정 테이블만, 특정 데이터만 접근 가능케 해주는 특별한 IAM역할 존재

### Index
- 특정 컬럼만을 사용하여 쿼리
- 테이블 전체가 아닌 기준점(pivot)을 사용해 쿼리가 이루어짐
- 매우 큰 쿼리 성능 효과
- 두 가지의 Index 유형 존재
    - Local Secondary Index (LSI)
        - 테이블 생성시에만 정의해줄 수 있음
        - 따라서 테이블 생성 후 변경, 삭제가 불가능
        - 똑같은 파티션키 사용, 그러나 다른 정렬키 사용
    - Global Secondary Index
        - 테이블 생성후에도 추가, 변경, 삭제 가능
        - 다른 파티션키, 정렬키 사용