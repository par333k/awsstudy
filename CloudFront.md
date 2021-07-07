## CloudFront
* 정적, 동적, 실시간 웹사이트 컨텐츠를 유저들에게 전달
* Edge Location을 사용 : 세계 곳곳에 있는 서버 컬렉션(은행의 ATM기 같은 역할), 캐싱하여 컨텐츠를 전달. Latency 감소의 역할.
* 컨텐츠 딜리버리 네트워크 Content Delivery Network(CDN)
* 분산 네트워크 (Distributed Network)

### 용어
* Edge Location: 컨텐츠들이 캐시에 보관되어지는 장소
* Origin(오리진): 원래 컨텐츠들이 들어있는 곳, 웹서버 호스팅이 되어지는 곳.
S3, EC2인스턴스가 오리진이 될 수 있음
* Distribution(분산): CDN에서 사용되어지며 Edge Location들을 묶고 있다는 개념

### 분산 설정 옵션
* Origin Domain Name: 컨텐츠 오리진 자원
* Origin Path: 특정 타겟 경로만 제공하길 원할때 경로 작성
* Restrict Bucket Access: 버켓 접근을 cloudfront를 통해서만 가능하게 할지 여부
* Origin Access Identity: 아이덴티티를 생성해서 s3버켓에 접근가능하게 해준다.
* Grant Read Permissions on Bucket: 버켓 읽기 허용을 접근하는 여부. yes를 하면 외부에서 정책 변경 가능, 컨텐츠 접근 가능
* Viewer Protocol Policy: 프로토콜 허용방식(HTTP, HTTPS)
* Restrict Viewer Access: 특정 유저만 접속할 수 있는지에 대한 기능(Signed URLS-IAM URL)
* SSL Certificate: HTTPS 인증서 적용, 기본 / 개인 인증서 적용가능

### 분산 네트워크 생성 후 옵션
* 다중 오리진 생성 가능
* Behavior - path pattern 설정 등의 작업 가능
* Error page - 에러가 발생했을 때 에러페이지 설정가능
* Restriction - 특정 지역의 블랙리스트/화이트리스트 적용가능
* Invalidations - 캐시 새로고침 (TTL 을 무시하고 캐시를 수동 교체), 추가 비용이 든다.

