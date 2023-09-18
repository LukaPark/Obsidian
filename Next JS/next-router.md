next 13에서 app directory를 이용한 경우,  
client에서 렌더링 하도록 하려면 "use client" 키워드를 사용해야 합니다.

하지만,  
`"use client"`를 사용하면 `useRouter`은  
`NextRouter was not mounted.`라는 에러가 발생하며 사용할 수없습니다.

대신하여, `useNavigation`을 사용해야 합니다.  
하지만, `useNavigation`에는 queries/dynamicPaths/paths과 같은 데이터가 존재하지 않아,  
query 등의 정보가 필요한 경우에는 `usePathname`를 같이 사용하면 됩니다.