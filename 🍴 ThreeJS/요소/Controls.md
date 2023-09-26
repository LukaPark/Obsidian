- 마우스를 이용해 카메라를 조종.

- JS 의 #mousemove 이벤트를 통해서 마우스의 좌표를 알아냄

```js
const cursor = {
    x: 0,
    y: 0
}
// JS 에서 제공하는 값을 그대로 사용해도 무방하지만, 1 이라는 크기를 표준값으로 지정하고 값을 변환해서 사용하는 것을 추천
// 마우스 커서가 중앙에 있을때는 0, 오른쪽으로 .5, 왼쪽으로 -.5 등으로 변환

window.addEventListener('mousemove', (event) => {
    cursor.x = event.clientX / sizes.width - 0.5
    cursor.y = - (event.clientY / sizes.height - 0.5)
  // ThreeJS에서와 브라우저에서 y축을 음양의 방향이 서로 다르므로 -1을 곱해준다.

    console.log(cursor.x, cursor.y)
})
```

#### 카메라의 위치 변환

- 상기 #mousemove 이벤트에서 알아낸 커서 값을 토대로 카메라의 위치 변환

```js
const tick = () => {
    // ...
    camera.position.x = cursor.x
    camera.position.y = cursor.y

    // ...
} 
```

#### 카메라의 각도 변환

- #lookAt 메소드를 추가 해 각도도 조절 

```js
const tick = () =>{
    // ...
    camera.position.x = cursor.x * 5
    camera.position.y = cursor.y * 5
    camera.lookAt(mesh.position)
    // ...
}
```

#### 카메라의 Full Rotation
- Math.sin(), Math.cos() 메소드들을 이용하면 Object 중심으로 카메라를 회전시킬 수 있음.
- Full Rotation 을 위한 "tau" 라는 필드가 존재하지만 이는 JS차원에서 지원하지 않음.
-  sin 과 cos를 조합하여 Full Rotation을 사용

```js
const tick = () => {
    // ...
    camera.position.x = Math.sin(cursor.x * Math.PI * 2) * 2
    camera.position.z = Math.cos(cursor.x * Math.PI * 2) * 2
    camera.position.y = cursor.y * 3
    camera.lookAt(mesh.position)
    // ...
}

tick()
```

# Built-in Controls

- #DeviceOrientationControls : VR experience를 조성하기 위해 활용 가능한 Control. 디바이스를 자동으로 검색하고 OS 나 브라우저가 허용한다면 카메라를 움직여 줌 ( 현재 Deprecate 가능성 )
- #FlyControls : 우주선에 탄 듯한 카메라의 무빙을 가능하게 하는 컨트롤. 앞뒤로 이동 + xyz 세 축으로 회전
- #FirstPersonControls : #FlyControls 와 유사하지만 축이 고정되어 있음. barrel roll 이 불가능한 새의 시점
- #PointerLockControls : JS의 pointer lock API를 활용한 컨트롤. 커서를 숨긴 상태로 가운데에 고정 시킨 후, mouseevent 이벤트의 콜백을 통해 그 움직임을 계속해서 감지한다. FPS 게임에 적합
- #OrbitControls : 마우스 좌측 클릭으로 카메라 회전이 가능하며, 우클릭으로 수직 수평 이동. 휠을 통해 Zoom
- #TrackballControls : 수직 앵글에 제한이 없는 #OrbitControls. #Scene 의 위아래가 바뀌어도 여전히 회전할 수 있음.
- #TransformControls: 특별히 카메라를 컨트롤 할 수 없고, 물체를 움직이기 위한 #gizmo 를 추가하기 위해 사용.
- #DragControls : 카메라를 마주 본 평면에서 물체를 움직이기 위해 사용.


# #OrbitControls 

####  Instantiating 

- 먼저 인스턴스화. 
- 주의할 점은 #OrbitControls 의 일부는 #ThreeJS 에서 기본으로 제공하고 있지 않음. *라이브러리의 무게 줄이기 위함*
- #OrbitControls 임포트 후 인스턴스 화

#### Target

- 기본적으로 카메라는 #Scene 의 중앙을 바라봄. Target 프로퍼티를 이용해 이를 변경해 줄 수 있음.
- Target 프로퍼티 역시 #Vector3 값으로 받으므로 x, y, z에 접근 가능


#### Damping

- #Damping 은 가속과 마찰의 공식을 활용해 애니메이션을 스무스하게 만들어주는 역할을 하는 속성.
-  Controls의 #enableDamping 속성 값을 true -> 활성화
- 이 속성을 올바르게 활용하기 위해서는 컨트롤이  controls.update() 를 통해 매 프레임마다 업데이트 되어야 함.