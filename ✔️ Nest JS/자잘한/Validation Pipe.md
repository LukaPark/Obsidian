

- **파이프 (Pipe)**
	- 요청이 라우터 핸들러 (클라이언트의 요청을 처리하는 엔드포인트 (ex. url) 마다 동작을 수행하는 컴포넌트, 라우트 핸들러가 요청 경로와 컨트롤러를 매핑. ) 으로 전달되기 전에 요청 객체를 변환 할 수 있는 기회를 제공.
	- **미들웨어**와 비슷한 역할이지만, 미들웨어는 애플리케이션의 모든 콘텍스트에서 사용하도록 할 수 없음 -> 현재 요청이 어떤 핸들러에서 수행되는지, 어떤 매개 변수를 갖는지에 대한 실행 콘텍스트를 갖지 못함.

	- 파이프의 사용 목적.
		1. 변환 *transformation* : 입력 데이터를 원하는 형식으로 반환, /users/user/1 의 경우 매개변수 string 1 을 number로 변환해서 컨트롤러에 전달.
		2. 유효성 검사 *validation* : 입력 데이터가 사용자가 정한 기준에 유효하지 않은 경우 예외 처리 -> 컨트롤러에 매핑X

	- 파이프의 종류
		- ValidationPipe
		- ParseIntPipe
		- ParseBoolPipe
		- ParseArrayPipe
		- ParseUUIDPipe
		- DefaultValuePipe
	- **Parse 파이프**들은 전달된 인수의 타입을 검사하는 파이프.
		- @Param 데코레이터의 두 번째 인수로 넘겨 실행 콘텍스트(ExecutionContext)에 바인딩.\
		- @Param 데코레이터의 인수로 넘길 때, 클래스가 아닌 new 인스턴스의 형태로 넣으면서 해당 객체에 커스텀이 가능 ( 에러 코드 등)
		- *입력받은 매개변수 (string)을 내부적으로는 number로 사용하고 있는 경우 , 매번 변환해서 사용하지 않아도 되는 장점.*

	- **DefaultValuePipe** : 인수의 값에 기본값을 설정할 때 사용.
		- 쿼리 매개변수가 생략된 경우, -> 유저 목록을 조회하는 api에서 offset기반 페이징을 사용할 때 등.
		
	- **Validation Pipe** : 커스텀 파이프의 역할
		- PipeTransform 인터페이스를 상속받음.
		- 오버라이딩 해야 하는 transform(value, metadata) 함수가 존재.
		- value: 현재 파이프에 전달 된 인수.
		- metadata: 현재 파이프에 전달 된 인수의 메타데이터
