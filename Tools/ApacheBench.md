# Apache Bench
- Apache 웹서버 성능 검사도구
- 현재 초당 몇개의 요청을 서비스하는지 알려준다

## 옵션 설명

### -A auth-username:password
- 서버에게 BASIC Authentication 정보를 제공한다
- `:`으로 구분한 사용자명과 암호를 base64 인코딩하여 전송한다

### -c concurrency
- 동시에 요청하는 요청수
- 기본적으로 한번에 한 요청만을 보낸다

### -H custom-header
- 요청에 헤더를 추가한다
- 콜론으로 구분한 쌍들의 헤더라인을 입력한다
    - e.g. "Accept-Encoding: multi"


---
## 참고링크
- [apache bench tutorial](https://www.tutorialspoint.com/apache_bench/)