
- Three.js 를 이용해 3D world를 만들기 위해서는 다음 4가지 기본 구성요소가 필요
- Renderer, Camera, Scene, Objects(Geometry, Mesh, Object3D, Light, ... etc)

이 중 한가지라도 누락된다면 텅 빈 캔버스를 만나게 됨.

Object: 그리고자 하는 요소
Scene: Object들을 담을 3D 공간,
Camera: Scene을 비추는 시야,
Renderer: 전체 Scene에서 Camera에 담기는 부분을 2D 이미지로 캔버스에 실시간 렌더링
****

* Three.js 로 무언가를 구현하려면 Scene, Camera, Renderer 가 필요.
* 일반적으로 PerspectiveCamera를 사용, 몇가지 Camera가 더 있음.

### #PerspectiveCamera 의 인자는 fov, aspect, near, far 순.

1.  fov (field of view, 시야각): 해당 시점의 화면이 보여지는 정도, 각도 값으로 설정 (degree)
2. aspect ratio (종횡비) : 요소의 높이와 너비에 맞추어 표시
3. near, far: far 값보다 멀거나, near 값보다 가까운 객체는 렌더링 X, 앱 성능 향상에 도움

## #Scene
- 3D 오브젝트가 존재하는 공간
- scene 아래에 다양한 요소들이 추가되어 3D화면을 구성하게 된다.

```
const scene = new THREE.Scene();
scene.add([scene graph에 추가할 요소])
```

- #SceneGraph 의 기초 요소
- #Mesh : 3D 오브젝트
	- mesh = geometry + material + (texture)
	- mesh 즉, ThreeJS의 3D 오브젝트를 만들기 위해서는 geometry와 material을 결합 해야함.
-  #Geometry  : 도형, 여러 도형들의 정점 데이터. 3D오브젝트의 뼈대
-  #material : 재질(소재). geometry의 표면의 속성을 나타냄
	- 재질, 색상, 광택 등
	- texture를 걸친다.
- #texture : #Mesh 를 둘러싸는 껍데기. 주로 이미지 파일로 사용

### #Camera
- 카메라. 3D 오브젝트가 존재하는 #Scene 을 바라보는 역할.
- 여러 카메라가 존재할 수 있으며, #SceneGraph 에 추가되지 않음

### #Renderer
1. ThreeJS의 메인 객체로, Scene과 Camera로 구성된 3D화면을 canvas에 render
2. renderer 인스턴스를 생성하고 렌더링 할 곳의 size를 설정해주어야 함.
3. 사이즈는 유지하고 해상도를 낮추거나 할 수 있음 ( 3번째 인자, undateStyle: Boolean);
4. render.domElement 를 html문서 안에 append 함으로써 삽입

#### #BoxGeometry
* 큐브에 필요한 vertice(꼭지점) , faces(면)이 포함되어 있음

#### #MeshBasicMaterial
* 물체의 색상을 결정하는데 사용

#### #Mesh
*  Geometry와 Material을 결합하여 객체를 생성
*  기하학을 받아 재질을 적용, 화면 안에 삽입, 자유롭게 움직일 수 있게 함


## In NextJS

#### useRef hook을 이용해 ref 객체를 생성하고 div 요소에 부착

* 이유
*1. React Dom 외부가 아닌 내부 노드의 자식으로 캔버스 요소 및 Threejs renderer.domElement를 삽입 하기 위해
2*. 의도치 않은 reFlow가 발생해도 동일한 요소에 대한 ref를 유지하기 위해서
*3. 원하는 시점, 원하는 상황에 unmount 하기 위해. 
*특히 컴포넌트 unmount 시에 useEffect hook의 cleanup 함수를 이용한 메모리 누수방지.
우아한 퇴장 (graceful exit)를 위해

