## Lambda 
* 서버리스의 주축을 담당
* Events를 통하여 lambda를 실행시킴
* Node.js, Python, Java, Go등 다양한 언어 지원
* Lambda Function

### 비용
* Lambda Function이 실행될때만 돈 지불
* 매달 1,000,000 함수 호출까지 무료(그 이상은 유료)

### 기타
* 최대 300초(5분) 런타임 시간 허용
* 512MB의 일시적인 디스크 공간 제공(/tmp/)
* 최대 50MB Deployment Package 허용
    - 50MB 초과될 시 S3 버켓에 올리고 경로를 설정

#### 활용
> 함수생성-> 직접/블루프린트/컨테이너/리파짓토리 선택 후 함수 작성 및 구성   
> aws 자원의 이벤트에 대해 트리거를 걸면 cloudwatch등을 통해 해당 람다함수의 실행확인이 가능   
> 몹시 다양한 활용성을 지님