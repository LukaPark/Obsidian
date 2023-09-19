*몇몇 디바이스나 Browser가 WebGL 을 지원하지 않음*

지원 여부를 체크하는 메서드를 실행해 지원 여부를 체크할 필요가 있음

```

import WebGL from 'three/examples/jsm/capabilities/WebGL';
if ( WebGL.isWebGLAvailable() ) {
	// Initiate function or other initializations here
		animate();
	 } else {
			 const warning = WebGL.getWebGLErrorMessage();
			 document.getElementById( 'container' ).appendChild( warning ); 
	 }

```