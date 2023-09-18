- @apollo/client / graphql / react-router-dom / styled-component
- Styled-component In Typescript -> @types/styled-components

1. client(endpoint, 캐시 설정 등을 진행하는 ApolloClient의 인스턴스)를 생성하고 , Provider로 앱을 감싸서 전역적으로 사용가능
2. RTK 와 유사하게 구조분해할당을 통해서 이용함, Loading, Error에 관한 결과를 받아올 수 있음.
3.  @apollo/client 패키지에서 제공하는 gql 메소드를 통해서 gql Query를 작성하고 useQuery() 훅을 이용하는 형태
4. Variable을 포함한 useQuery를 작성할 떄는,  useQuery([gql], { variable : { id: $id }}); 형태로 Variable을 포함시켜서 전달함
5. Apollo Cache는 한번 진행했던 쿼리에 대해서 설정에 맞게 저장
6. Local Only Field : 서버나 DB상에서는 존재하지 않기 때문에 API요청을 하지않고, Apollo Cache 상에서만 저장되어있는 Field. 
	절대 API에 요청을 보내지 않음 ex) 다크모드, 유저의 타임존 , Youtube의 볼륨 크기나 화질 등등 휘발성있는 정보