### #Geometry 

- Geometry 는 3D 오브젝트의 뼈대 역할 (*필수*)
- 이미 형태가 정해진 일종의 프리셋들이 존재
- Custom 가능하고 가장 기본이 되는 #BufferGeometry 
- #Geometry  는 3D 공간상의 점들과 면으로 구성되어 있음. 
![[Pasted image 20230919121436.png]]
#### #BufferGeometry 
- ThreeJS 의 모든 Geometry를 구성하는 방식.
- #BufferAttributes 라는 데이터 배열들의 집합으로 구성
- #BoxGeometry, #PlaneGeometry 등은 이미 데이터가 세팅이 되어있는 Geometry.

- #Geometry 는 기본적으로 정점(Vertex)들의 집합.  정점에 속성을 부여해서 특정한 형태와 속성을 가진 #Geometry 를 만들 수 있다. #BufferAttributes 는 바로 이 속성 값을 부여하는데 사용
- #BufferGeometry 가 가진 위치, 색상 등의 데이터의 배열을 평행하게 병렬로 배치했을 때 배열에서 동일한 포지션에 존재하는 값의 집합이 동일한 정점의 속성이 된다.

- #BufferAttributes 의 데이터를 임의로 생성하고 #BufferGeometry 에 추가해서 임의의 Geometry를 생성 할 수 있다.

#### 여러가지 종류의 내장 Geometries
- 모든 내장 Geograpies는 translate(...), rotateX(...), normalize() 등의 메소드를 가진 #BufferGeometry 클래스를 상속 받음

![[Pasted image 20230919121633.png]]

#CircleGeometry : 파이차트와 같이, 평면 원의 특정 비율도 표현 가능.
#ConeGeometry : 콘의 밑면을 여닫을 수 있음. 콘의 밑면이 파이차트와 같은 형태가 될 수 있음.
#CylinderGeometry : 위 둘과 마찬가지

![[Pasted image 20230919121943.png]]
#RingGeometry, #TorusGeometry 역시 Geometry 의 특정 포지션 만을 표현 하는 것이 가능

![[Pasted image 20230919122017.png]]
- 각 각 사면체, 팔면체,  십이면체, 이십면체를 나타내는 데, detail 옵션을 건드려주게 되면, 각 면에 #vertex  를 추가하고 더 둥글게 변형 할 수 있음.
-  #IcosahedronGeometry 의 경우 detail 속성을 늘려주더라도 해당 #Geometry 를 구성하는 삼각형들의 크기가 서로 거의 같은 크기로 유지되면서 #sphere 에 가까워 짐.

![[Pasted image 20230919122455.png]]
#SphereGeometry : 작은 사각형(두 삼각형의 조합)으로 이루어진 큰 구체
#ShapeGeometry : path를 기반으로 한 모양의 #Geometry 
#TextGeometry : 3D 텍스트 #Geometry 


- 3D 소프트웨어를 직접 활용 해 직접 #Geometry 를 제작하고 사용 할 수 있음.


# Geometry의 파라미터와 #Segment

- 모든 #Geometry 들은 생성자에서 파라미터를 받는데, 이는 각 #Geometry 마다 다름.
- #BoxGeometry 의 경우는 6가지
	1. width: 너비 (x축 사이즈)
	2. height : 높이 (y축 사이즈)
	3. depth: 깊이 (z축 사이즈)
	4. widthSegment: 너비가 몇 개의 구간으로 세분화 되어있는지
	5. heightSegment: 높이가 몇 개의 구간으로 세분화 되어있는지
	6. depthSegment: 깊이가 몇 개의 구간으로 세분화 되어있는지
- 세분화( #subdivision) 란 몇개의 삼각형으로 구성될 것인가를 의미.

![[Pasted image 20230919123231.png]]

![[Pasted image 20230919123236.png]]

- #subdivision 을 나누면 나눌 수록 각 삼각형, 즉 #face 를 구분하기 어려워짐.
- 그러나 많은 #vertices 를 추가하면 GPU는 더 많은 연산을 수행해야 하기 때문에, 성능에 문제를 야기 할 수 있음.
- 