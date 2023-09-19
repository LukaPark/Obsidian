# #Plane 

- 평평한 바닥. 

```

//plane사이즈
const planeSize = 10;
//plane Geometry생성
const planeGeo = new THREE.PlaneGeometry(planeSize, planeSize);
//material생성
const planeMat = new THREE.MeshPhongMaterial({
  color: 0x66cdaa,
  side: THREE.DoubleSide,
});
//mesh만들기
const plane = new THREE.Mesh(planeGeo, planeMat);
//plane돌려놓기
plane.rotation.x = Math.PI * -0.5;
//scene에 추가
scene.add(plane);
```

- #Plane 은 #Geometry  중 #PlaneGeometry 를 불러와서 사용

- ThreeJS는 각도를 표현 할 때 #radian 을 단위로 사용.
	- #radian : 호의 길이가 반지름과 같게 되는 만큼의 각을 1 라디안(radian) 이라고 정의
- #Plane 을 기본 생성 시 세로로 세워져 있기 때문에 rotation을 시켜줘야 함
- 