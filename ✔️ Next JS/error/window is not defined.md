- Nextjs 에서 SSR을 진행할 때 처음 페이지를 렌더링 하는 과정에서는 
- window, document 나 LocalStorage 등 전역 객체가 존재하지 않슴.
- SSR 과정에서 해당 객체에 접근할 경우 undefined 참조 오류

**해결**

1. typeof 연산자를 통해 해당 객체가 undefined 인지 검사

2. useEffect Hook 을 통해서 렌더링 이후에 window, document 등 객체에 접근

3. next/dynamic : ES2020의 dynamic import 를 지원하기에 ssr: false 옵션을 사용해 SSR없이 컴포넌트를 동적으로 접근