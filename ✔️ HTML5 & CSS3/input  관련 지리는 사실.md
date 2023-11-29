
# TextIndent

- 인풋 내부의 여백이 외부에 영향 주지 않슴. 권장

vs 

# Padding




# input:password 글자 안보임 현상

:: 일부 웹 폰트의 경우 input[type=password] 를 지원하지 않기 떄문...
.나눔 스퀘어의 경우에도 지원하지 않슴. 
input[type=password] {
	font-family: "[다른 폰트]"
}

사용해서.. 와일드카드를 보여주자..