### #Geometry 

- Geometry 는 3D 오브젝트의 뼈대 역할 (*필수*)
- 이미 형태가 정해진 일종의 프리셋들이 존재
- Custom 가능하고 가장 기본이 되는 #BufferGeometry 

#### #BufferGeometry 
- ThreeJS 의 모든 Geometry를 구성하는 방식.
- #BufferAttributes 라는 데이터 배열들의 집합으로 구성
- #BoxGeometry, #PlaneGeometry 등은 이미 데이터가 세팅이 되어있는 Geometry.

- #Geometry 는 기본적으로 정점(Vertex)들의 집합.  정점에 속성을 부여해서 특정한 형태와 속성을 가진 #Geometry 를 만들 수 있다. #BufferAttributes 는 바로 이 속성 값을 부여하는데 사용
- #BufferGeometry 가 가진 위치, 색상 등의 데이터의 배열을 평행하게 병렬로 배치했을 때 배열에서 동일한 포지션에 존재하는 값의 집합이 동일한 정점의 속성이 된다.

- #BufferAttributes 의 데이터를 임의로 생성하고 #BufferGeometry 에 추가해서 임의의 Geometry를 생성 할 수 있다.
