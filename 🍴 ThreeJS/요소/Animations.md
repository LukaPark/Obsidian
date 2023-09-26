- ThreeJS 에서 애니메이션을 적용하는 다양한 방법이 있음
- ThreeJS 에서 애니메이션을 실해하는 방법은 스톱모션
	- Object를 조금씩 이동하여 계속해서 렌더링을 수행하는 것
	- 렌더링 사이사이에 Object를 더 많이 움직일 수록 빨리 움직이는 것처럼 보임
	- 때문에 보고있는 화면의 #FrameRate 가 중요한 요소임
	- #FrameRate 는 화면마다 제각각 일 수 있으므로 화면의  #FrameRate 에 구애받지 않고 같은 속도로
	- 애니메이션을 보여줄 수 있어야 함

# 1. RequestAnimationFrame

#RequestAnimationFrame 의 주요 목적은 각 프레임에서 코드를 실행하는 것이 아님.
- #RequestAnimationFrame 은 다음 프레임에 제공한 함수를 실행 -> 다음 함수가 다시 #RequestAnimationFrame 을 사용한다면, 해당 함수가 실행 ( 재귀의 형태 )

## 화면에 구애받지 않고 사용하기

1. 시간을 활용
	- Adaptation to the framerate
```js
let time = Date.now()
const tick = () => {
    const currentTime = Date.now()
    const deltaTime = currentTime - time
    time = currentTime
  
    mesh.rotation.y += 0.01 * deltaTime
    // deltaTime이 0인 경우 mesh가 회전하지 않는다.
    renderer.render(scene, camera);
    window.requestAnimationFrame(tick);
}
tick()
		
```

=> 현재 프레임의 timestamp에서 이전 프레임의 timestamp 를 빼서 deltaTime을 구하고,
=> 60fps 에서 deltaTime 이 16정도 출력되는데, 큐브가 빠른 속도로 회전하게 됨.


# 2. Using Clock

- #ThreeJS 에는 #Clock 이라는 내장 솔루션이 존재.
- #Clock 클래스를 인스턴스화 하고, #getElapsedTime()와 같은 메소드를 사용하는 방법
- #getElapsedTime 은 Clock이 생성되고 몇 초가 지났는지 반환함.

```js
const clock = new THREE.Clock();

const tick = () => {
  const elapsedTime = clock.getElapsedTime();
  
  mesh.position.x = Math.cos(elapsedTime);
  mesh.position.y = Math.sin(elapsedTime);
  camera.lookAt(mesh.position);

  renderer.render(scene, camera);

  window.requestAnimationFrame(tick);
};

tick();
```

- #getDelta 라는 메소드도 있음. 난이도가 있으므로 #getElapsedTime 메소드를 먼저 활용해 볼 수 있도록


# 3. Using a Library

- 특정한 애니메이션을 주고 싶을 때 -> 애니메이션 라이브러리를 활용 할 수 있다.

```js
gsap.to(mesh.position, { duration: 1, delay: 1, x: 2 });

const tick = () => {
  renderer.render(scene, camera);
  window.requestAnimationFrame(tick);
};

tick();
```

- GSAP 라이브러리를 활용 한 예
- 