**Next/Image** 컴포넌트에서 제공하는 대표적인 기능.
1. **lazy-loading**
2. **이미지 사이즈 최적화**
3. **placeholder 제공.**

#### **lazy loading**
- 이미지를 로드하는 시점까지. 필요할 때까지 지연시키는 기술.
- 스크린 밖에 있는 이미지들은 로딩을 지연시키고, 스크린 안에 포함되는 이미지만 빠르게 로드.

- **lazy-loading**을 적용하고 싶지 않을 때 : 
	- Image 컴포넌트의 priority props를 true로 주거나, *(권장)*
	- loading prop에 "eager" 값을 설정

#### **이미지 사이즈 최적화**
- Next/Image는 디바이스 크기 별로 srcSet을 미리 지정해두고, 사용자의 디바이스에 맞는 이미지를 다운로드해서 사용하게끔 지원.
- layout prop 설정에 따라 어떤 srcSet 목록이 변경.
- 이미지를 webp와 같은 용량이 작은 포맷으로 변환하여 이미지를 제공.

- 사용자의 디바이스에 맞는 이미지 사이즈를 만들고, 용량이 작은 webp 포맷으로 변환하는 작업은 이미지에 대한 최초 요청 시에 Next.js 서버에서 진행.
- 이후 요청에는 캐시가 만료될 때까지 캐시 된 이미지가 제공되기 때문에 첫 번째 요청보다 훨씬 빠르게 이미지를 서빙할 수 있슴.
- 캐시가 만료된 후, 요청이 들어오면 오래된 이미지를 우선 제공하고, 백그라운드에서 이미지 최적화를 다시 진행.
- *이미지가 캐싱되는 기간: next.config.js의 image.minimumCacheTTL 구성 또는 CDN에서 응답한 이미지의 Cache-Control 헤더 중 더 큰 것으로 정의됨.*

#### **Placeholder 제공**
- 이미지가 로드되기 전, 이미지 영역의 높이가 0이었다가 이미지가 로드된 후 이미지만큼 영역이 늘어 레이아웃이 흔들리는 현상 -> **CLS(Cumulative Layout Shift)** 라고 부름.
- 이러한 레이아웃 흔들림을 방지하기 위해 Next/Image는 **placeholder**를 제공해, 이미지가 로드 되기 전에도 해당 높이만큼 영역을 표시해 레이아웃 흔들림을 방지.

- **placeholder** 는 빈 영역또는 blur 이미지(로컬이미지의 경우 build 타임에 생성, 리모트 이미지의 경우에는 base64로 인코딩 된 data url을 지정해 주어야 함.)로 적용할 수 있고, 커스텀 하게 지정할 수 있음.


# 경험
- Next/Image를 사용 할 때 
- prop width, height에 0을 넣고 tailwind css 를 이용해 w, h를 동적으로 주려고 했을 경우 
- 사진의 srcSet에서의 quality가 낮게 나오는 현상이 발생
-> prop width, height 에 변수를 바인딩 하는 방식으로 해결