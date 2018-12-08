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

## [ [시연영상](https://youtu.be/GoBE7Rcq_ks) ]
## [ [직접해보기](http://52.79.242.155/Jindo_Dog/) ]
<br></br>

## 설명
---
- 관리자 계정에서 매장을 추가하고 매장 별 좌석 및 음식관리와 매출관리, 회원관리 등을 처리한다.
-	사용자 계정에서 원하는 매장에 접속하고 매장 별 좌석사용 및 음식주문 등을 이용한다.
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
- 소켓을 통한 실시간 사용 좌석 확인.
- 이미지 업로드를 위한 전용 서버 구현.
### * 업로드 전용 서버에 요청 보내기
~~~html
<form action="insertFood" id="addForm"  method="POST"  enctype="multipart/form-data">
~~~
~~~javascript
var formData = new FormData($('#addForm')[0]); // form태그의 name값을 파라미터 형식으로 변환.
$.ajax({
    async : false,
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
