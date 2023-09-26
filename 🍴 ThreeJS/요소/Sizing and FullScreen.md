#immersive 한 experience를 제공하기 위해 Full Screen을 제공해야 할 상황이 있음.
- Full Screen 에서 ThreeJS를 활용한다면, 반응형에 잘 대응 할 필요가 있음.

#### Fit in the ViewPort

- window.innerWidth, window.innerHeight 를 이용하면, 캔버스가 뷰포트에 딱 들어맞게끔 조정 할 수 있음.
```js
const sizes = {
    width: window.innerWidth,
    height: window.innerHeight
}
```
```css
// styles.css
* {
    margin: 0;
    padding: 0;
}
html,
body
{
    overflow: hidden;
}
.webgl {
    position: fixed;
    top: 0;
    left: 0;
    outline: none;
    // ThreeJS에서 renderer.setSize를 사용해주고 있기 때문에, 
    // 따로 정확한 width와 height 속성을 입력해주지 않아도 된다.
}
```

- Full Screen 에서 ThreeJs를 적용 . resize에는 대응 X

#### Handle Resize

- 윈도우 리사이즈에 대응하기 위해 
	1. 이벤트 리스터를 통해 resize를 감지할 수 있도록 설정.
	2.  윈도우 사이즈가 변화함에 따라 sizes, camera.aspect를 수정

*camera.aspect* : 카메라 절두체의 종횡비. 
*절두체* : 사각뿔의 윗부분을 밑면에 평행하게 잘라낸 입체 형상을 가리킴. 일반적으로 캔버스 너비를 캔버스의 높이로 나눈 값.
![[Pasted image 20230919120834.png]]

- camera.aspect 를 업데이트 할 때는 camera.updateProjectionMatrix()  메소드를 활용해 프로젝션의 매트릭스를 같이 업데이트 해주어야 함.
- renderer 까지 업데이트 해주어야 함

```js
window.addEventListener('resize', () => {
  sizes.width = window.innerWidth
  sizes.height = window.innerHeight
  
  camera.aspect = sizes.width / sizes.height
  camera.updateProjectionMatrix()
  
  renderer.setSize(sizes.width, sizes.height)
})
```

#### Handle Pixel Ratio

디스플레이의 Pixel Ratio 에 따라 이미지를 정확하게 표현 할 수 있음.

- window.devicePixelRatio 를 통해 스크린의 Pixel Ratio 를 받아 
- renderer.setPixelRatio(...) 로 활용 가능.

```js
window.addEventListener('resize', () => {
    sizes.width = window.innerWidth
    sizes.height = window.innerHeight

    camera.aspect = sizes.width / sizes.height

    renderer.setSize(sizes.width, sizes.height)
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
    // Math.min() 메소드를 활용해 값을 제한 해줌
})
```

#### Handle Full Screen

- Full Screen 일때와 아닐때를 유저가 선택할 수 있게 만들기.

```js
// 더블클릭시 풀스크린 토글 함수
window.addEventListener('dblclick', () => {
    if(!document.fullscreenElement) {
        canvas.requestFullscreen()
    } else {
        document.exitFullscreen()
    }
})
```

```js

// Safari 까지 대응 하기 위한 메소드
window.addEventListener('dblclick', () => {
    const fullscreenElement = document.fullscreenElement || document.webkitFullscreenElement

    if(!fullscreenElement) {
        if(canvas.requestFullscreen) {
            canvas.requestFullscreen()
        } else if(canvas.webkitRequestFullscreen) {
            canvas.webkitRequestFullscreen()
        }
    } else {
        if(document.exitFullscreen) {
            document.exitFullscreen()
        } else if(document.webkitExitFullscreen) {
            document.webkitExitFullscreen()
        }
    }
})
```