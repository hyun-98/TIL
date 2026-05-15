**로컬 설치 → SMTP 연결 → 사내 발송 테스트**

---

# 1. GoPhish 로컬 설치

## (1) 다운로드

* 공식: [https://getgophish.com](https://getgophish.com)

OS에 맞는 zip 다운로드 후 압축 해제

## (2) 실행

### Windows

```bash
gophish.exe
```

### Linux / EC2

```bash
chmod +x gophish
./gophish
```

---

## (3) 초기 접속

실행하면 아래가 뜸:

* Admin URL:
  `https://127.0.0.1:3333`

* 기본 계정:

  * username: `admin`
  * password: 로그에 출력됨

⚠️ SSL 인증서 경고 뜨는 게 정상 (로컬이라서)

---

# 2. 핵심 설정 파일 (config.json)

GoPhish 폴더에 있음.

```json
{
  "admin_server": {
    "listen_url": "127.0.0.1:3333",
    "use_tls": true
  },
  "phish_server": {
    "listen_url": "0.0.0.0:80",
    "use_tls": false
  }
}
```

## 중요 포인트

* `admin_server` = 관리자 UI
* `phish_server` = 실제 피싱 링크 서버 (랜딩 페이지)

---

# 3. SMTP (사내 메일 서버 연결)

GoPhish에서 가장 중요한 단계

## (1) 경로

Dashboard → **Sending Profiles** → New Profile

---

## (2) 예시 설정

### 기본 입력

* Name: `company-smtp`
* From: `security@company.com` (또는 사내 승인된 주소)

---

### SMTP 설정

예: 질문에서 준 경우

```
smtp.pantechcni.com:25
```

설정은 이렇게:

* Host: `smtp.pantechcni.com`
* Port: `25`
* Username: (사내 SMTP 인증 계정)
* Password: (사내 계정 비밀번호)
* Encryption:

  * 25번 → 보통 NONE 또는 STARTTLS 없음
  * 587이면 STARTTLS
  * 465이면 SSL

---

## ⚠️ 매우 중요 (실무 이슈)

### 1) 인증 필요 여부

사내 SMTP는 보통 둘 중 하나:

* IP 허용 방식 (relay 허용)
* ID/PW 인증 방식

👉 이걸 모르고 쓰면 100% 실패함

---

### 2) 릴레이 허용 (가장 흔한 문제)

사내 메일 서버에서 GoPhish 서버 IP를:

* SMTP relay 허용 목록에 추가해야 함

예:

```
192.168.0.10 (GoPhish 서버)
```

---

### 3) SPF / DKIM

메일이 스팸 처리되는 이유:

* SPF 미설정
* DKIM 없음
* From 주소 위조처럼 보임

👉 사내 도메인 사용 권장:

```
security@company.com
```

---

# 4. 랜딩 페이지 설정

GoPhish → **Landing Pages**

예:

* 로그인 페이지 흉내
* 공지사항 페이지
* 비밀번호 변경 페이지

설정 옵션:

* Capture Submitted Data: ON (훈련 목적이면 켜도 됨)
* Capture Passwords: (사내 정책 따라 조심)

---

# 5. Email Template 설정

GoPhish → **Email Templates**

예:

```
제목: [보안 점검] 비밀번호 재설정 필요

내용:
보안 정책에 따라 비밀번호를 재설정해주세요.
```

---

# 6. Target List (직원 목록)

GoPhish → **Users & Groups**

CSV 업로드:

```csv
first_name,last_name,email
홍,길동,hong@company.com
김,철수,kim@company.com
```

---

# 7. Campaign 생성

GoPhish → **Campaigns**

설정:

* Email Template
* Landing Page
* Sending Profile
* Group 선택


