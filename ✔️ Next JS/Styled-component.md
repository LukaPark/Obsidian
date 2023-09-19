1.  styled-component, -D @types/styled-components 설치

 **NextJS 는 기본적으로 SSR을 이용해 pre-rendering 진행하는데 ServerSide 에서 html 파일을 구성하여 브라우저 측에 전달해 렌더링하는데(css 포함)  스타일이 적용되지 않은 html코드가 먼저 렌더링 되는 문제가 발생합니다.**

- 해결
1.  babel-plugin-styled-components 설치 
2. .babelrc 파일 생성
```
{
    "presets": ["next/babel"],
    "plugins": [
        [
            "styled-components",
            {
                "ssr": true,
                "displayName": true,
                "preprocess": true
            }
        ]
    ]
}
```

4. 위와 같이 .babelrc 작성