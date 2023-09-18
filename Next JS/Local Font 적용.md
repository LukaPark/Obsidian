- Next JS 12버전 까지는 @font-face 를 설정하고 font-family를 적용했지만
- 13버전 부터는 next/font 라이브러리를 이용함

- next/font/google 에서 구글 폰트를 이용할 수 있음
- next/font/local 을 사용할 경우 Local Font 적용 가능

```
const Pretendard = localFont({
    src: "../../public/fonts/PretendardVariable.woff2",
});
```

형태로 localFont 인스턴스 생성후
body tag에 className으로 주입
```
<body className={Pretendard.className}>{children}</body>
```
