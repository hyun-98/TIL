# 2일차

local 환경에서만 돌아가는 상황 -> 외부 연결 필요
서버 필요 -> ec2 ubuntu

#### ec2 접속 후 초기 설정
```claude
# 패키지 업데이트
sudo apt update && sudo apt upgrade -y

# 방화벽 설정
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
sudo ufw allow 3333
sudo ufw enable
```

####  GoPhish 설치
```
# 필요 패키지
sudo apt install wget unzip -y

# GoPhish 다운로드 (최신 버전 확인 후)
wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip

# 압축 해제
unzip gophish-v0.12.1-linux-64bit.zip -d gophish
cd gophish
chmod +x gophish

```



#### config.json 수정
```
{
  "admin_server": {
    "listen_url": "0.0.0.0:3333",
    "use_tls": true,
    "cert_path": "gophish_admin.crt",
    "key_path": "gophish_admin.key"
  },
  "phish_server": {
    "listen_url": "0.0.0.0:80",
    "use_tls": false,
    "cert_path": "example.crt",
    "key_path": "example.key"
  },
  "db_name": "sqlite3",
  "db_path": "gophish.db",
  "migrations_prefix": "db/db_",
  "contact_address": "",
  "logging": {
    "filename": "",
    "level": ""
  }
}
```


#### GoPhish 서비스 등록 (자동 실행)
```bash
# 서비스 파일 생성
sudo nano /etc/systemd/system/gophish.service
```

```ini
[Unit]
Description=GoPhish Phishing Framework
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/home/ubuntu/gophish
ExecStart=/home/ubuntu/gophish/gophish
Restart=always

[Install]
WantedBy=multi-user.target
```

```bash
# 서비스 등록 및 시작
sudo systemctl daemon-reload
sudo systemctl enable gophish   # 부팅 시 자동 시작 등록
sudo systemctl start gophish    # 지금 즉시 시작

# 상태 확인
sudo systemctl status gophish
```

#### 인바운드 규칙 & 아웃바운드 규칙

인바운드
- SSH : TCP : 22 : 내 IP : 서버 접속
- HTTP :  TCP : 80 : 0.0.0.0/0 : 피싱 렌딩페이지
- 사용자지정 : TCP : 3333 : 내 IP : GoPhish 관리콘솔

아웃바운드
- 모든 트래픽 : ALL : ALL : 0.0.0.0/0

#### icon 받아오는 사이트 (svg로 다운 없이 직접 받기)

https://simpleicons.org/?q=air




