# [팀 프로젝트] 통합 매장 관리 시스템
---
<div>
<img src="https://user-images.githubusercontent.com/19260410/49681660-1ddac280-fae9-11e8-8eaa-47f08a9cd447.PNG" width="400">
<img src="https://user-images.githubusercontent.com/19260410/49681665-2c28de80-fae9-11e8-9444-825027fd420f.PNG" width="400">
</div>
<div>
<img src="https://user-images.githubusercontent.com/19260410/49681669-3a76fa80-fae9-11e8-8875-df1e3cf1aab2.PNG" width="400">
<img src="https://user-images.githubusercontent.com/19260410/49681676-46fb5300-fae9-11e8-92d8-ce37d608483c.PNG" width="400">
</div>

## [ [시연영상](https://youtu.be/GoBE7Rcq_ks) ]
## [ [직접해보기](http://52.79.242.155/Jindo_Dog/) ]
<br></br>

## 설명
---
- 서울시 자전거 대여소 좌표 정보 API를 활용하여 간첩의 위치를 임의로 설정하고 다음 지도 API를 통해 보여준다. 
- 자신의 촉과 아이템을 활용하여 설정된 간첩 수의 50% 이상을 찾아내면 클리어된다.
- 클리어 후 잡은 간첩들의 이름을 카카오톡 메신저를 통해 전송할 수 있다.
<br></br>

## 지원
---
- Chrome Extension
- Aws EC2 Server
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
- MySql WorkBeanch 8.0
<br></br>

## 개인 역할
---
- javascript SDK를 이용한 카카오 로그인 API를 통해 로그인 구현.
- javascript SDK를 이용한 카카오 링크 API를 통해 잡은 간첩들의 이름을 메신저로 전송하는 기능 구현.
- 다음 지도 API와 서울시 좌표기반 근접 지하철역 정보 API를 통해 역 근처 간첩 위치 조회 서비스 구현.

### * Ajax 통신을 통한 좌표 가져오기

