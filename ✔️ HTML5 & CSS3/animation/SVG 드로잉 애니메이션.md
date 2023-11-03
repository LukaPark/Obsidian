
SVG 드로잉 애니메이션의 핵심은 **dash-array**, **dash-offset**

- **stroke-dasharray**: path 전체의 length 값 이상의 gap을 주어야 그려지는 것처럼 보임.
	- **path length**: 일러스트의 옵션 중 document info palette using the object option에서 전체값 확인.
- **stroke-offset**: path를 이동시켜 움직임을 주는 옵션. 이를 이용해 시작점을 변경 할 수 있음.
	1. 간편하게 일러스트, 벡터 프로그램에서 svg로 path를 작성. *직접 svg path 나 line을 이용해 작성 할 수 도 있음.*
	2. CSS 에서 stroke-dasharray와 dash-offset에 값을 주어 움직임을 만든다.
