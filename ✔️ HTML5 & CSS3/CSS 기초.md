1. **link** , **@import** 방식 차이
	- 비교: 사용은 비슷하게 하지만, link 방식을 사용하는 것이 @import 방식을 사용하는 것보다 페이지의 로딩 속도 측면에서 뛰어남.
	- **Link 방식**
		1. HTML 의 <link> 태그 사용
		2. 유지보수 용이 - CSS 연결 방식이 아닌 하나의 파일에 여러 페이지의 스타일을 일괄 수정 및 추가. 직렬 방식이 아닌 병렬 방식으로 다운로드 하기 때문에, 로딩속도 빠름
	- **@import 방식**
		1. CSS 파일 내에 @import 데코레이터를 이용하여 CSS를 연결하는 방식
		2. 하나의 CSS 파일에 여러개의 페이지 CSS 를 로드하여 편리함.

2. **CSS Inline-style** 
	- HTML Inline Style로 태그 내에 style 필드에 직접 CSS를 작성하는 행위

3. **CSSOM** *CSS Object Model*
	- 브라우저는 DOM을 생성하는 동안 외부 StyleSheet를 접하고 리소스에 대한 요청을 즉시 발송하고 요청.
	- CSSOM도 트리 구조를 가지고, DOM과 같은 프로세스를 진행하며, HTML 대신 CSS에 대해 프로세스를 진행함.
	- CSSOM 에서 Cascading 룰을 가지고 스타일을 세분화.