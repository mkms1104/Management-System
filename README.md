# [팀 프로젝트] 통합 매장 관리 시스템
---
<div>
<img src="https://user-images.githubusercontent.com/19260410/49681660-1ddac280-fae9-11e8-8eaa-47f08a9cd447.PNG" width="420">
<img src="https://user-images.githubusercontent.com/19260410/49681665-2c28de80-fae9-11e8-9444-825027fd420f.PNG" width="420">
</div>

<div>
<img src="https://user-images.githubusercontent.com/19260410/49681669-3a76fa80-fae9-11e8-8875-df1e3cf1aab2.PNG" width="420">
<img src="https://user-images.githubusercontent.com/19260410/49681676-46fb5300-fae9-11e8-92d8-ce37d608483c.PNG" width="420">
</div>

### 테스트용 사용자 아이디: min33 / 비밀번호: 1234 / 매장 jk_pc 
### 테스트용 관리자 아이디: jka / 비밀번호: 1234 / 매장 jk_pc
<br></br>

## [ [시연영상](https://youtu.be/1sraIQycvAM) ]
## [ [직접해보기](http://52.79.242.155/MS/) ]
<br></br>

## 설명
---
- 관리자 계정에서 매장을 추가하고 매장 별 좌석 및 음식관리와 매출관리, 회원관리 등을 처리한다.
- 사용자 계정에서 원하는 매장에 접속하고 매장 별 좌석사용 및 음식주문 등을 이용한다.
- 게시판, 쪽지 기능을 통해 사용자와 관리자 간의 실시간 소통을 할 수 있다.
<br></br>

## 지원
---
- Chrome Extension
- Aws EC2 Server
- Git
<br></br>

## 사용 기술 
---
- HTML5, CSS
- JavaScript, JQuery, Ajax
- Spring, MyBatis, Bootstrap
<br></br>

## 개발 환경
---
- Window OS
- Spring Tool Suite version: 4.3.17.RELEASE
- Tomcat 8.5
- MySql WorkBeanch 8.0
<br></br>

## 개인 역할
---
- 사용자의 좌석 사용과 음식 주문 페이지 설계 및 디자인, 사용자 반응, CRUD 처리.
- 관리자의 좌석 관리와 주문 처리, 음식 추가 및 재고 관리 페이지 설계 및 디자인, 사용자 반응, CRUD 처리.
- 카운트 함수를 통한 실시간 사용시간 처리.
- 스프링 소켓을 통한 실시간 사용 시간 확인.
- 이미지 업로드를 위한 전용 서버 구현.
### * 업로드 전용 서버 처리 과정
#### form 태그 
~~~html
<form action="insertFood" id="addForm"  method="POST"  enctype="multipart/form-data">
~~~
#### 서버에 저장하기
~~~javascript
var formData = new FormData($('#addForm')[0]); // form태그의 name값을 파라미터 형식으로 변환.
$.ajax({
    async : false, // ajax를 동기적 실행.
    type : 'POST',
    url : 'http://52.79.242.155:8080/FileServer/uploadFile/food', // EC2를 통해 배포한 서버 주소로 요청.
    data : formData,
    processData : false,
    contentType : false,
                 
     success : function(data) {
          $('#addTable input[name=food_photo]').val(data); // 서버에서 받은 파일이름으로 DB에 Insert.
          $('#addForm').submit();
     }
});
~~~
#### 서버에서 불러오기
~~~html
<img src="http://52.79.242.155:8080/FileServer/resources/foodImg/파일이름"/>
~~~

### * 실시간 사용 시간 확인 과정
#### 사용자 페이지에서 사용 시간 전달
~~~javascript
var sock = new SockJS("<c:url value="/echo"/>"); // 소켓 연결

// userTime은 초 단위로 저장되어있음.
var min = Math.floor(userTime/60); // 분 계산
var sec = Math.floor(userTime%60); // 초 계산

var timer = setInterval(function (){
	if(sec == 1 && min == 0){ // 사용 시간 종료
		clearInterval(timer);

	} else{
		sec--;
							
	    if(sec < 1){
		    min--;
		    sec = 59;
	    }
	}
						
	var seatUser = { // 서버로 전송할 객체 생성
		seatId : seatId,
		min : min,
		sec : sec,
	};
	
	sock.send(JSON.stringify(seatUser)); // 1초 마다 JSON 형태의 문자열로 변경 후 서버로 전송
}, 1000);						
~~~
#### 웹 소켓 서버
~~~java
@Override
protected void handleTextMessage(WebSocketSession session, TextMessage message) throws Exception {
	logger.info("{}로 부터 {} 받음", session.getId(), message.getPayload());
		
	for(WebSocketSession sess : sessionList){ // 소켓 세션에 물려있는 모든 이용자에게 메시지 전송(보낸이 포함)
        	sess.sendMessage(new TextMessage(message.getPayload()));
        }
}
~~~
#### 관리자 페이지에서 사용 시간 처리 
~~~javascript
sock.onmessage = function(evt){ // 서버에서 메시지가 전송됬을 때 자동 실행되는 콜백 메서드(onmessage) 
	var data = evt.data;
	data = JSON.parse(data); // 받은 JSON 형태의 문자열을 JSON 객체로 변환
	
	var seatId = data.seatId // 좌석 번호
	var min = data.min // 분
	var sec data.sec // 초
}

sock.onclose = function () { // 서버와 연결이 끊어졌을 때 자동 실행되는 콜벡 메서드(onclose)
	// 사용 중인 좌석을 지운다.	
}
~~~
