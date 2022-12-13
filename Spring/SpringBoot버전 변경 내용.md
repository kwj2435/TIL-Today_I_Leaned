### Spring Boot의 버전별 업데이트 내용 정리
2022.12.13 기준

#### Spring Boot 3.0
1. Java 17 기반으로 변경(최소 요구 사항 java 17)
2. XML이 점차적으로 Spring에서 사라지게 될 것을 명시
3. HttpMethod가 enum에서 Class로 변경
4. Commons FileUpload, Tiles 등 서블릿 기반 기능이 지원 종료
5. 새로운 AOT 엔진 도입
6. URL에서 마지막에 / 붙일경우 '/'가 없을 URL경로와 자동으로 매칭 해주는 trailing slash matching configuration이 기본 -> 옵션으로 변경