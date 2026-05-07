Kubernetes (K8s) : 컨테이너 기반 애플리케이션을 자동으로 배포, 운영, 확장해주는 오픈소스 플랫폼

“컨테이너 → Docker → Linux → Kubernetes”

```
1. Linux 기초
      ↓
2. 네트워크/서버 기초
      ↓
3. Docker
nginx 컨테이너 실행
직접 Dockerfile 만들기
DB 연결
      ↓
4. Kubernetes 기본 객체
      ↓
5. Kubernetes 실습
Minikube
kind
      ↓
6. Helm 쿠버네티스의 패키지 매니저
      ↓
7. Monitoring / Logging
      ↓
8. CI/CD
      ↓
9. Cloud Kubernetes (EKS/GKE/AKS)
```

---

목표
Pod 이해 : 컨테이너를 실행하는 가장 작은 단위
* 컨테이너 :

Deployment 이해 : Pod 관리자
Service 이해 : Pod 접속 창구


[실습 : PC에서 K8s 실습, nginx 배포)

[ kubectl ]
     ↓ 명령 전달
[ Kubernetes Cluster ]
     ↑ Minikube가 생성
[ Docker Desktop ]
     ↑ 컨테이너 실행 엔진 제공

