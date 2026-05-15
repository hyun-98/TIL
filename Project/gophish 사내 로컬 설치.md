가능해. GoPhish는 **보안 교육/피싱 대응 훈련용으로 설계된 오픈소스 도구**라서, 사내 승인만 제대로 되어 있다면 충분히 합법적으로 활용할 수 있어. 다만 실제 메일 서버/직원 대상으로 쓰는 거라서 **스팸 오인, 보안 정책 위반, 메일 차단** 이슈가 자주 생기니까 그 부분까지 같이 고려해서 설명해줄게.

아래는 **로컬 설치 → SMTP 연결 → 사내 발송 테스트** 기준으로 정리한 기본 세팅 흐름이야.

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

---

# 8. 테스트 방법 (중요)

무조건 먼저:

### 1단계

👉 본인 이메일만 테스트

### 2단계

👉 사내 테스트 그룹 (IT팀 등)

---

# 9. 운영 시 주의사항 (진짜 중요)

## ❌ 하면 안 되는 것

* 승인 없이 전 직원 발송
* 외부 도메인 스푸핑
* 실제 로그인 정보 수집 후 저장

## ✅ 해야 하는 것

* 사전 공지 (보안 교육 목적)
* 결과 데이터 익명 처리
* 로그 보관 정책 확인

---

# 10. 자주 발생하는 문제

## ❌ 메일 안 감

* SMTP relay 차단
* 포트 25 막힘 (회사 방화벽)

## ❌ 스팸함

* SPF 없음
* From 주소 이상

## ❌ 링크 안 열림

* phish_server 외부 접근 불가
* 포트 80/443 방화벽 문제

---

# 필요하면 다음도 도와줄게

원하면 여기까지 확장 가능:

* EC2에 GoPhish 배포 (실전 구조)
* HTTPS 인증서 (Let's Encrypt)
* 사내 SMTP relay 설정 확인 방법
* 피싱 성공률 분석 리포트 읽는 법
* “안 걸리게 만드는 게 아니라 교육 효과 높이는 캠페인 설계”

---

원하면 지금 상황 기준으로
👉 “네 회사 SMTP 환경에서 왜 메일이 안 가는지” 같이 디버깅도 해줄게.
