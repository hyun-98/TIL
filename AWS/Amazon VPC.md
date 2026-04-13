# ☁️ Amazon VPC란?

**Amazon VPC (Virtual Private Cloud)**는  
👉 AWS 클라우드 안에 내가 직접 설계하는 **전용 네트워크**입니다.

---

## 🧠 쉽게 이해하면

- AWS = 큰 인터넷 공간  
- VPC = 그 안에 만든 **내 회사 네트워크**

👉 즉,  
**클라우드에서 사용하는 ‘사설망(Private Network)’**

---

## ⚙️ VPC의 핵심 역할

### 1️⃣ 네트워크 공간 제공
- Amazon EC2 같은 서버를  
👉 VPC 안에 배치해서 운영

---

### 2️⃣ 네트워크 구역 나누기 (Subnet)
- **Public Subnet** 👉 외부 인터넷 연결됨  
- **Private Subnet** 👉 내부 전용 (보안 강화)

👉 서비스 구조를 안전하게 설계 가능

---

### 3️⃣ 인터넷 연결 제어
- **Internet Gateway** 👉 외부 인터넷 연결  
- **NAT Gateway** 👉 내부 서버 → 외부만 가능

👉 “누가 외부와 통신할지” 제어

---

### 4️⃣ 보안 관리
- **Security Group** 👉 서버 단위 방화벽  
- **Network ACL** 👉 네트워크 단위 방화벽  

👉 접근 허용/차단을 세밀하게 제어

---

### 5️⃣ 회사 네트워크처럼 확장
- VPN 연결 → 사무실 ↔ AWS 연결  
- 온프레미스(On-Premise) 서버와 연동 가능  

---

## 🧩 구성 요소 한눈에

| 구성 요소 | 설명 |
|----------|------|
| VPC | 전체 네트워크 |
| Subnet | 네트워크 구역 |
| Route Table | 트래픽 경로 설정 |
| Internet Gateway | 인터넷 출입구 |
| Security Group | 서버 단위 방화벽 |

---
