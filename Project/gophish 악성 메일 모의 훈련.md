
[gophish 블로그]

출처: https://dobby-isfree.tistory.com/83?category=1067545

출처: https://zulloper.tistory.com/131 [zulloper blog:티스토리]


1. 설치
Gophish 사이트에서 다운로드받거나 Gophish Github Repository에서 Clone하는 방법이있다.
설치는 비교적 간단하다. 아래 명령어들을 순서대로 입력하여 설치 후 실행하면 된다

1.1
gophish-v0.12.1-windows-64bit.zip
설치

1.2
config.json
- listen_url : 127.0.0.1:3333 -> 0.0.0.0:3333

1.3
gophish 파일에 실행 권한을 주고, gophish 실행
```
chmod 700 gophish
./gophish
```

1.4
localhost:3333으로 접속

---

## 2. gophish 설정

### 2.1 User & Groups

#### Users & Groups
  - 모의훈련을 하기 위한 대상자의 이름/메일주소/직책을 넣는 정보이다.
  - 각 사용자별로 넣을수도 있고, [Download CSV Template]를 통해 일괄 등록도 가능하다.

<img width="776" height="605" alt="image" src="https://github.com/user-attachments/assets/e4f63973-9c27-49f8-ab2f-771dc3330597" />

### 2.2 Email Templates
  - 훈련 대상자에게 전달되는 피싱메일에 대한 코드정보를 입력하는 화면이다.
  - HTML 형식으로 작성 가능하며, Import Email을 통해 외부의 메일 템플릿 정보를 그대로 가지고 올 수 있다.
  - 특히, 하단의 Add Tracking Image를 추가할 경우 <p>{{.Tracker}}</p>가 추가되며,
     단순 메일 열람한 사용자에 대해서도 확인이 가능하다.

<img width="1025" height="865" alt="image" src="https://github.com/user-attachments/assets/af73a529-c656-432e-9e29-5a53388e3cf2" />


### 2.3 Landing Pages
  - 위 2.의 피싱메일을 받은 사용자가 연결되는 페이지라고 보면 된다. 즉 피싱사이트 정보가 된다.
  - 마찬가지로 Import Site를 통해 외부 임의의 Site 정보를 그대로 받아올 수 있다.
  - 또한, 하단의 Capture Submitted Data / Capture passwords를 통해 사용자가 입력하는 정보를 저장할 수 있다.

<img width="980" height="916" alt="image" src="https://github.com/user-attachments/assets/b41310a0-22ee-4fb1-be6b-47a7c63b0cf5" />

### 2.4  Sending profiles
  - 악성메일 발신자 정보를 넣는 카테고리이다.
  - Gophish는 Mail Proxy의 개념이기 때문에 처음에 악성메일을 보낼 메일서버의 인증값을 받아야 한다.
     해당 인증값을 받기 위한 사용자 정보라고 보면 된다.

<img width="1213" height="936" alt="image" src="https://github.com/user-attachments/assets/f26b5768-ec4c-4349-8e7f-a95240fe3819" />

SMTP FROM : 수신자가 메일에서 보게 되는 "보낸 사람 주소"


### 2.5 Campaigns
  - 위 과정을 모두 다 진행했다면, 이제 모의훈련이 가능하다. 캠페인 카테고리는 실제 모의훈련을 설정하는 페이지이다.

<img width="749" height="750" alt="image" src="https://github.com/user-attachments/assets/61584b48-40af-42ed-8509-cae7c630d606" />

URL : 이메일 안에 있는 링크를 눌렀을 때 연결되는 Landing Page

- localhost:80 = 내 컴퓨터의 웹서버 기본 포트
- 외부에서 접속하려면 도메인 or 공인 IP 필요
