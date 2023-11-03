일반적으로 디바이스 크기로 pc와 mobile을 구분 하지만,
pc에서 작은 화면으로 볼 수도 있고 13인치 iPad를 사용하는 등 디바이스 크기로만 구분짓기 어려움.

이를 해결해주는 hover, pointer 쿼리를 이용하면 Mobile, PC 환경을 구분 지을 수 있음

![[Pasted image 20231004123437.png]]
해당 CSS Media Queries 를 사용하기 위해서

window api, matchMedia() 를 활용.
**현재 화면이 미디어쿼리의 범위에 들어가는지** 
```js

window.matchMedia('(max-width: 600px)').matches; // boolean

// 여러 쿼리를 확인 하고 싶을 경우and 키워드를 사용
window.matchMedia('(hover: none) and (pointer: coarse)').matches;

// NextJS에서는 기본적으로  SSR이 실행되기 때문에 window === undefined 임
export const isTouchScreen = 
	  typeof window !== 'undefined' &&
		  window.matchMedia('(hover: none) and (pointer: coarse)').matches;
```