
# #material ?

- #material 은 단어 의미 그대로 '소재, 재질' 을 의미 함.
- 종류에 따라 재질이 달라지고, 재질은 얼마나 빛을 반사하는지, 빛에 반응하여 어떤 느낌을 내는 지를 주로 결정
- 빛과의 상호작용 외에도, Texture를 입히지 않은 상태에서는 Material을 통해 물체의 색상을 결정 할 수 있다.

### 기본 재질

-  #MeshBasicMaterial : 광원의 영향을 받지 않음
-  #MeshLambertMaterial : 정점에서만 광원을 계산함
-  #MeshPhongMaterial : 픽셀 하나하나에 전부 광원을 계산함, 반사점 지원
	- #shininess 속성으로 반사 점의 밝기를 조절 할 수 있음 (default: 30)
-  #MeshToonMaterial : 부드럽게 쉐이딩 하는 대신, MeshToonMaterial은 Gradient map 을 사용함 -> 카툰 느낌

### 물리 기반 렌더링을 위한 재질

- #PBR :  물리 기반 렌더링 (Physically Based Rendering)
- 실제 세계처럼 물체를 구현하기 위해 복잡한 수학 사용

- #MeshStandardMaterial : Phong 과 비슷하나 사용 속성이 다름
	- #roughness : #shininess 의 반대, 0에서 1까지
	- #metalness : 금속성, 0에서 1까지
-  #MeshPhysicalMaterial : 상기 #MeshStandardMaterial 과 같지만 추가 옵션이 있음
	- #clearcoat: 표면 코팅 세기
	-  #clearcoatRoughness : 코팅의 거침 정도

#### 속도 가 빠른 순서

- basic > lambert > phong > standart > physical
- 성능 부담이 클 수록 더 현실적인 결과물을 얻을 수 있으나 사양이 좋아야 하고, 저 사양 지원을 위해서는 코드 최적화가 필요함

# 특수 재질

- #ShadowMaterial : 그림자로부터 데이터를 가져오는 데 사용
-  #MeshDepthMaterial : 각 픽셀의 깊이를 렌더링 함
	- 카메라의 마이너스 near에 위치한 픽셀은 0으로, 마이너스 far에 위치한 픽셀은 1로 렌더링
-  #MeshNormalMaterial : 카메라를 기반으로 #Geometry 의 법선을 렌더링 함
	- x축은 ref, y축 green, z축 blue
- #ShaderMaterial : Three.js의 쉐이더 시스템을 이용해 재질을 커스텀
-  #RawShaderMaterial : Three.js의 도움을 받지 않고 재질을 커스텀

# 자주 사용하는 속성

- #FlatShading : 물체를 각지게(faceted) 표현 할 지의 여부, default : false,
-  #side : 어떤 면을 렌더링 할 지의 여부
	- Three.FrontSide (앞, default) , Three.BackSide(뒤), Three.DoubleSide (양 면)