
- npm install [package] : ./node_modules 폴더에 패키지를 설치하기 위한 명령어
	- npm i : 줄임말
	- npm install [package] --save : [pacakage]를 설치하면서 package.json에 있는 dependencies 객체에 지금 설치한 정보를 추가
	- npm install [package] --save --dev : devDependencies 객체에 추가
- devDependency 에 있는 패키지들은 --production 명령어로 빌드시 설치 되지 않음 