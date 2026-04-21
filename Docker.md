Docker는 애플리케이션을 신속하게 구축, 테스트 및 배포할 수 있는 소프트웨어 플랫폼입니다. Docker는 소프트웨어를 컨테이너라는 표준화된 유닛으로 패키징하며, 이 컨테이너에는 라이브러리, 시스템 도구, 코드, 런타임 등 소프트웨어를 실행하는 데 필요한 모든 것이 포함되어 있습니다. Docker를 사용하면 환경에 구애받지 않고 애플리케이션을 신속하게 배포 및 확장할 수 있으며 코드가 문제없이 실행될 것임을 확신할 수 있습니다.


Docker

핵심 개념 3가지
1. 이미지 (Image) — 설계도
2. 컨테이너 (Container) — 실제 집
3. Dockerfile — 설계도를 만드는 방법

Dockerfile      =  햄버거 레시피
Image           =  레시피대로 만든 반죽/재료 세트
Container       =  실제로 만들어진 햄버거
Docker Hub      =  레시피 공유 사이트 (유튜브처럼!)

Dockerfile 예시
```
# 베이스 재료 선택 (파이썬 3.11이 설치된 환경에서 시작)
FROM python:3.11

# 내 앱 파일들을 컨테이너 안으로 복사
COPY app.py /app/app.py

# 필요한 라이브러리 설치
RUN pip install flask

# 앱 실행!
CMD ["python", "/app/app.py"]
```
