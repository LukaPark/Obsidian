# #texture ?

- #texture 는 #Geometry 의 표면을 감싸는 '이미지'
-  #texture 는 객체의 표면, #material 은 빛과의 상호 작용 표현을 담당

#### Texture의 타입

![[Pasted image 20230919140303.png]]

- Color ( or albedo) : 기본 텍스처 타입. 파일의 픽셀만 가져와 #Geometry 에 적용
- Alpha: 이미지의 흰색은 표시, 검정색은 표시 X, #GrayScale 텍스쳐.
- Height : #relief 를 만들기 위해 #vertex 를 이동시키는 텍스쳐. 이 텍스처를 활용하려면  #subdivision  을 추가해야 함.
- Normal : #vertex 들 자체를 이동시키지 않으면서, 표면이 서로 다른 방향을 향하고 있다고 보이도록 빛의 방향만을 조정. #Geometry  를 따로 #subdivision 할 필요가 없기 때문에 디테일을 추가하는데 유용.
- Ambient Occlusion: #GrayScale 텍스쳐.  표면의 틈새에 가짜 그림자를 만듬. 물리적으로 정확하지는 않지만  #contrast 를 만드는데 유용.
- Metalness : 흰색으로 금속성 부분을 지정하고 검은색으로 비금속성 부분을 지정해둔 텍스쳐. 반사를 구현할 때 유용
- Roughness : 흰색으로 거친 부분, 검은색으로 부드러운 부분을 지정. 빛을 어떻게 분산시키는가를 결정.

#### #PBR 

 - 이러한 질감( 금속성 및 거칠기 등)은 #PBR 원칙을 따름.
 - PBR은 물리적 기반 렌더


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