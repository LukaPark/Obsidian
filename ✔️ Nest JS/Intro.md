- Nest 는 **효율적이고 확장 가능한 Node.js** 서버 앱을 구축하기 위한 프레임워크.
- **TypeScript** 지원, OOP(*객체 지향 프로그래밍*), FP(*기능 프로그래밍*), FRP(*기능 반응 프로그래밍*) 요소를 결합.
		- 내부적으로 **Nest**는 **Express**와 같은 강력한 HTTP 서버 프레임워크를 제공하며, 선택적으로 **Fastify** 역시 사용할 수 있음.
		- **Nest**는 이러한 일반적인 Node.js 프레임워크(Express/Fastify) 보다 높은 수준의 추상화를 제공하지만, 해당 API를 개발자에게 직접 공개.
		- 이를 통해 개발자는 수 많은 타사 모듈들을 자유롭게 이용 할 수 있음.

- Babel 컴파일러 사용.
- Nodejs 기반을 둔 웹 API 프레임워크로서, Express or Fastify 프레임워크를 래핑하여 동작.
- Fastify가 Express 보다 2배 정도 빠른 속도를 보장하지만, Express의 사용자가 더 많고 다양한 미들웨어가 NestJs 와 호환되기 때문에 Default = Express.
- 

#### **Main.ts**

- Nest 애플리케이션 인스턴스를 생성하기 위해 NestFactory 클래스를 사용.
- 애플리케이션은 인바운드 HTTP 요청을 기다릴 수 있도록 HTTP Listener를 시작.
- Nest CLI로 스캐폴드 된 프로젝트는 개발자가 각 모듈을 자체 전용 디렉토리에 유지하는 규칙을 따르도록 권장하는 초기 프로젝트 구조 생성.
- 