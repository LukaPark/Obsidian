- #PerspectiveCamera 뿐만 아니라 #Camera 추상클래스를 상속받은 다양한 하위 클래스들이 있음.
	1. #ArrayCamera : 여러 대의 카메라를 활용하여 #Scene 을 여러 차례 렌더링 해야할 때 사용.
	2.  #StereoCamera : 사람의 시점을 흉내내는 카메라. 카메라 두 대를 이용해 사람의 눈을 묘사함. 깊이감을 조성하고 이를 통해 #parallaxa 효과 등을 만들 수 있음. VR headset 같은 장치들로 확인할 수 있음
	3. #CubeCamara :  상하좌우전후를 각각 렌더링 할 때 사용. #EnvironmentMap 이나 #ShadowMap 을 위해 활용.
	4. #OrthographicCamera : 시점이나 공간감, 원근감을 가능한 배제한 형태를 보여주는 카메라. 오브젝트와 카메라 사이의 거리가 얼마나 되는지와 무관하게 모든 요소들이 같은 사이즈로 렌더링 됨.
	5. #PerspectiveCamera : #OrthographicCamera 와 반대로 공간감과 원근감을 느낄 수 있도록 렌더.

![[Orthographic vs Perspective.png]]

### #PerspectiveCamera 

- 파라미터
	1. #FOV : Field of view, 카메라 뷰의 수직 각도 너비.
	
      ![[Pasted image 20230919110416.png]]
	- 앵글이 작아지면 망원렌즈의 카메라 처럼 보이게 되고, 앵글이 넓어지면 카메라에 담기는 풍경이 넓기 때문에 #어안효과 를 얻을 수 있음. 일반적으로 45~75 의 각도를 이용

![[Pasted image 20230919110539.png]]

### #AspectRatio

- width를 height로 나눈 값, 종횡비
- #AspectRatio 는 여러 곳에서 활용 되므로 따로 변수로 만들어 활용하는 것을 추천

```js
const sizes = {
    width: 800,
    height: 600
}
```

### #NearAndFar

- 카메라가 얼만큼 멀리 볼 수 있는가? 얼마나 가까이까지 접근할 수 있는 지 결정해주는 인자


* #OrthographicCamera 
	* 원근감이 배제되어 있어 특정 프로젝트에 아주 유용하게 활용될 수 있음
	* #FOV 대신 카메라가 각 방향으로 얼마나 멀리 볼 수 있는 지를 알려주고 near, far 변수를 전달
	
```js
const aspectRatio = sizes.width / sizes.height
const camera = new THREE.OrthographicCamera(- 1 * aspectRatio, 1 * aspectRatio, 1, - 1, 0.1, 100)
```