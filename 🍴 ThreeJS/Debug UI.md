- dat.GUI 와 같은 방식으로 이용 할 수 있는 lil-gui를 이용 할 예정


```js
import * as dat from 'lil-gui'

const gui = new dat.GUI()
// GUI 인스턴스 생성

// y축으로 카메라를 커스텀 하는 패널
gui.add(mesh.position, 'y', - 3, 3, 0.01)

// 👇🏼 아래와 같은 방식으로 작성할 수도 있음
gui.add(mesh.position, 'y').min(- 3).max(3).step(0.01)

// .name() 메소드를 통해 GUI에 표기 될 label의 이름을 설정해 줄 수 있음.

// 다양한 속성들을 GUI로 컨트롤 할 수 있음.
const gui = new dat.GUI()
gui.add(mesh.position, 'y', - 3, 3, 0.01).name('elevation')
gui.add(mesh, 'visible')
gui.add(material, 'wireframe')

// 색상 
const parameters = {
    color: 0xff0000
}
gui.addColor(parameters, 'color').onChange(() =>
{
    material.color.set(parameters.color)
})

// 함수를 트리거
const parameters = {
    color: 0xff0000,
    spin: () =>
    {
        gsap.to(mesh.rotation, { duration: 1, y: mesh.rotation.y + Math.PI * 2 })
    }
}
gui.add(parameters, 'spin')
```

- 이외에 다양한 옵션들
	- autoPlace: (boolean / default: true) : GUI 를 페이지의 오른쪽 상단에 고정할 것인가에 대한 필드
	- container: (HTMLElement / optional) : GUI를 특정 HTMLElement에 추가하고 싶을 때 활성화. 해당 속성을 사용시 autoPlace 속성을 뒤집어 쓰게 됨.
	- width : (number / default: 245) : GUI 패널의 넓이 지정.
	- title: (string / default: Controls) : 패널 상단에 표시되는 이름.
	- injectStyles: (boolean / default true) : 기본으로 제공되는 styleSheet을 활용한다면 true, 커스텀 -> false.
	- touchStyles (boolean / default true) : 터치 가능한 디바이스에서 컨트롤러를 더욱 크게 보여주는 옵션
	- parent (GUI / optional) : 해당 GUI 를 또 다른 GUI의 자식으로 추가하기 위한 옵션, 보통 addFolder() 와 함께 활용하게 됨.
	- 