# #texture ?

- #texture 는 일반적으로 포토샵 같은 이미지 프로그램으로 만든 '이미지'
-  #texture 는 객체의 표면, #material 은 빛과의 상호 작용 표현을 담당


## 1. #TextureLoader 불러오기

```
const loader = new Three.TextureLoader();
```

# 2. #texture 입히기

```
const material = new Three.MeshBasicMaterial({
	color: 0xff8844,
	map: loader.load("url"),
});
```


# 3.  여러 #texture 입히기
```
const materials = [
  new THREE.MeshBasicMaterial({map: loader.load('resources/images/flower-1.jpg')}),
  new THREE.MeshBasicMaterial({map: loader.load('resources/images/flower-2.jpg')}),
  new THREE.MeshBasicMaterial({map: loader.load('resources/images/flower-3.jpg')}),
  new THREE.MeshBasicMaterial({map: loader.load('resources/images/flower-4.jpg')}),
  new THREE.MeshBasicMaterial({map: loader.load('resources/images/flower-5.jpg')}),
  new THREE.MeshBasicMaterial({map: loader.load('resources/images/flower-6.jpg')}),
];

const cube = new THREE.Mesh(geometry, materials);
``` 

# 4. 비동기 처리

```
const loader = new THREE.TextureLoader();
loader.load('resources/images/wall.jpg', (texture) => {
  const material = new THREE.MeshBasicMaterial({
    map: texture,
  });
  const cube = new THREE.Mesh(geometry, material);
  scene.add(cube);
  cubes.push(cube);  // 회전 애니메이션을 위해 배열에 추가
});
``` 

5. 여러 설정들

-  #ClampToEdgeWrapping : Texture의 가장자리 픽셀을 계속해서 반복
-  #RepeatWrapping : Texture 자체를 반복
-  #MirroredRepeatWrapping : Texture 자체를 반복하되, 매번 뒤집어 반복

-  rotation속성은 radian단위로 설정