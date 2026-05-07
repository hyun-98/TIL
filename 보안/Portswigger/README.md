SQL Injection
사용자가 입력한 값을 이용해서 데이터베이스 명령을 속이는 공격

방지 방법
- 입력값 검증
- Prepared Statement 사용
- ORM 사용

XSS
사용자가 입력한 악성 자바스크립트가 다른 사람 브라우저에서 실행되는 공격

방지 방법
- HTML escape
- 입력값 필터링
- CSP(Content Security Policy)

CSRF (Cross Site Request Forgery)
로그인된 사용자를 속여서 원하지 않는 행동을 하게 만드는 공격
---

-
방지 방법
- CSRF Token 사용
- SameSite Cookie
- 재인증


---
IDOR (Insecure Direct Object Reference)
권한 확인 없이 번호만 바꾸면 다른 사람 정보가 보이는 취약점

서버에서 반드시:
```
"현재 로그인 사용자와 요청 대상이 같은가?"
```
검사해야 함

---

인증 우회 (Authentication Bypass)
로그인을 제대로 안 했는데 로그인된 것처럼 들어가는 문제

방지 방법

모든 민감 페이지에서:

로그인 여부
권한 여부

반드시 검사

---
세션 취약점

* 웹사이트는 사용자를 기억하기 위해 :'세션 ID' 사용

