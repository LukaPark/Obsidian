#Scene  에서 object를 변경하는 4가지 속성

1. position : 위치 변경
2. scale: 크기 변경
3. rotation: 회전
4. quaternion: 회전과 관련된 속성 

#PerspectiveCamera 나 #Mesh 등 Object3D를 상속받는 모든 Class은 위와 같은 4가지 속성을 가짐.
해당 4가지 속성들은 #matrices 라고 부르는 것으로 compile. 
직접 #matrices 에 접근하지 않고 상기 속성들을 이용함


# 1. Position
- position은 x, y, z라는 주요한 속성을 가짐.
- 세 속성은 3D 공간에서의 각 축을 나타냄
- Render 메소드를 호출하기 이전에 이동시켜야 함

- position 속성은 #Vector3 의 인스턴스
	- mesh.position.length() : (0, 0, 0) 부터 점 혹은 mesh 까지의 거리
	- mesh.position.distanceTo(mesh) : object로 부터 mesh 까지의 거리
	- mesh.position.normalize() : 방향을 유지하면서 length를 1로 설정하는 메소드
	- mesh.position.set(x, y, z): x, y, z를 한번에 설정하는 메소드
	

# 2. #AxesHelper

- 축을 시각화 해서 보여주는 속성. 인자로 축의 길이를 넘겨줄 수 있음

```
const axesHelper = new Three.AxesHelper(2);
scene.add(axesHelper)
```


# 3. Scale

- scale도 #Vector3 이므로, 기본적으로 x, y, z 기본값 1인 속성들을 가짐. ( 상기 vector3 메소드들 사용 가능 );
- 사이즈를 다루는 속성. 
- 음수 값을 사용할 수 있지만, 축이 logical direction에 위치하지 않게 되고 이로 인해 나중에 버그 발생할 수 잇으니 지양


# 4.Rotation

- rotation은 두가지 속성 #rotation, #quaternion 
- 두 속성 중 하나를 업데이트 하면 나머지 하나도 자동으로 업데이트 됨.
- #rotation 역시 x, y, z 속성을 갖고 있지만,  #Vector3 가 아닌 #Euler 인스턴스
	- y축 회전 : 회전 목마 형태
	- x축 회전 : 정면에서 다가오는 자동차의 바퀴 형태
	- z축 회전 : 비행기를 정면에서 바라보았을때 프로펠러의 회전
- 단위는 #radian 을 사용하므로 Math.PI 를 이용
```
mesh.rotation.x = Math.PI * .25;
mesh.rotation.y = Math.PI * .25;
mesh.rotation.z = Math.PI * .25;
```

- 회전은 x, y, z 순서로 적용. -> 한 축의 회전을 적용하면 다른 축에도 영향을 미침
- #reorder 메소드를 통해서 순서를 설정해 줄 수 있음
```
 object.rotation.reorder( 'xyz' );
```

# 5. LookAt

- #Objcet3D 인스턴스에는 오브젝트에게 다른 오브젝트를 바라보도록 요청하는 #lookAt() 메소드가 존재.
- 매개 변수는 바라볼 대상 오브젝트이며, #Vector3 이여야 함.
- 이 메소드를 활용해 카메라가 어떤 오브젝트를 바라볼 수 있게 하는데, 게임으로 쳤을 때 총구가 적을 겨누는 등
 ```
camera.lookAt(cube1.position);
camera.lookAt(new Three.Vector3(0, 0, 0));
```


# 6. SceneGraph

- 앞서 살펴본 Transform 오브렉트들을 그룹화 
	1. 그룹을 먼저 인스턴스 화
	2. 인스턴스화한 그룹을 #Scene 에 추가
	3. 그룹에 들어갈 다른 오브젝트는 #Scene 에 바로 add하지 않고, #group 에 Add 
	4. 그룹에 대한 변형을 한번에 시도할 수 있음
	5. 