
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

### 2.0 User & Groups

#### Users & Groups
  - 모의훈련을 하기 위한 대상자의 이름/메일주소/직책을 넣는 정보이다.
  - 각 사용자별로 넣을수도 있고, [Download CSV Template]를 통해 일괄 등록도 가능하다.

<img width="776" height="605" alt="image" src="https://github.com/user-attachments/assets/e4f63973-9c27-49f8-ab2f-771dc3330597" />

### 2.1 Email Templates
  - 훈련 대상자에게 전달되는 피싱메일에 대한 코드정보를 입력하는 화면이다.
  - HTML 형식으로 작성 가능하며, Import Email을 통해 외부의 메일 템플릿 정보를 그대로 가지고 올 수 있다.
  - 특히, 하단의 Add Tracking Image를 추가할 경우 <p>{{.Tracker}}</p>가 추가되며,
     단순 메일 열람한 사용자에 대해서도 확인이 가능하다.

<img width="1025" height="865" alt="image" src="https://github.com/user-attachments/assets/af73a529-c656-432e-9e29-5a53388e3cf2" />


### 2.1 Landing Pages




2.2  Sending profiles


2.3 Email Templates


2.4 Campaigns

