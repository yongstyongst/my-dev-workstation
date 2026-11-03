# 🖥️ 나의 개발 워크스테이션

> WSL2 + Ubuntu + Docker 환경 구축 및 웹 서버 배포 실습 프로젝트

---

## 📁 프로젝트 구조

```
my-dev-workstation/
├── Dockerfile          # 웹서버 이미지 빌드 설정
├── README.md           # 프로젝트 문서
└── site/
    └── index.html      # 웹 페이지 (한글 인코딩 적용)
```
---

## ⚙️ 실행 환경

| 항목 | 내용 |
|------|------|
| OS | Windows 11 + WSL2 (Ubuntu 22.04) |
| 쉘/터미널 | bash / Windows Terminal |
| Docker 버전 | 29.9.2 (build a82e528) |
| Git 버전 | 2.53.0 |

---

## 🚀 실습 목표

- WSL2 환경에서 Docker를 활용한 웹 서버 구축
- Dockerfile 작성 및 커스텀 이미지 빌드
- 바인드 마운트 / 볼륨을 활용한 데이터 영속성 실습
- GitHub 원격 저장소 연동 및 버전 관리

---

## 🐳 Docker 운영 로그

### docker ps -a

| CONTAINER ID | IMAGE | NAME | STATUS | PORTS |
|---|---|---|---|---|
| 142bbfc72081 | my-webserver | my-web-vol | Up | 0.0.0.0:8082→80/tcp |
| cdd8d28e3c29 | my-webserver | my-web-mount | Up | 0.0.0.0:8081→80/tcp |
| 288ec7e93063 | my-webserver | my-web | Created (포트 충돌) | - |
| abb804a8e759 | my-web-server | my-site | Up | 0.0.0.0:8080→80/tcp |

---

## 📌 Git 커밋 로그

| 커밋 해시 | 메시지 |
|-----------|--------|
| 0575acd | Update README.md with project description |
| 53a45d2 | Complete: Docker web server setup with Korean support |
| 879a72f | Initial commit |

---

## ✅ 수행 항목 체크리스트

| 항목 | 내용 | 완료 |
|------|------|------|
| 터미널/권한 | WSL2 + Ubuntu 설치 및 sudo 권한 확인 | ✅ |
| Docker 설치 | Docker Engine 설치 및 버전 확인 | ✅ |
| Dockerfile | Nginx 기반 웹서버 Dockerfile 작성 | ✅ |
| 포트 매핑 | -p 8080:80 으로 컨테이너 실행 | ✅ |
| 바인드 마운트 | 호스트 디렉토리 컨테이너에 마운트 | ✅ |
| Docker 볼륨 | 볼륨 생성/연결/삭제 후 영속성 확인 | ✅ |
| Git 설정 | 사용자 정보 및 기본 브랜치 설정 | ✅ |
| GitHub 연동 | 원격 저장소 Push 완료 | ✅ |

---
## 📸 실행 화면

### 기본 웹서버 (포트 8080)
<img width="2392" height="1021" alt="스크린샷 2026-11-03 170238" src="https://github.com/user-attachments/assets/c2692bb2-73cc-4310-b240-3379ef042792" />

### 바인드 마운트 (포트 8081)
<img width="2404" height="1025" alt="스크린샷 2026-11-03 170221" src="https://github.com/user-attachments/assets/02598795-70b2-4504-b965-407c070a8044" />

### Docker 볼륨 (포트 8082)
<img width="2392" height="1019" alt="스크린샷 2026-11-03 170208" src="https://github.com/user-attachments/assets/5c00e818-94d1-4e85-80cc-f3b348e62fcd" />

---

## 🚨 트러블슈팅

### 1️⃣ 한글 인코딩 오류

| 항목 | 내용 |
|------|------|
| **문제** | 브라우저에서 한글이 깨져 보임 |
| **원인 가설** | HTML 파일에 charset 미설정 |
| **확인** | 브라우저 인코딩 설정 확인 → UTF-8 미적용 상태 |
| **해결** | `<meta charset="UTF-8">` 태그를 index.html에 추가 |

### 2️⃣ Docker 이미지 빌드 오류

| 항목 | 내용 |
|------|------|
| **문제** | `docker build` 실행 시 오류 발생 |
| **원인 가설** | Dockerfile 내 COPY 경로 잘못 지정 |
| **확인** | Dockerfile 내용 및 디렉토리 구조 재확인 |
| **해결** | COPY 경로 수정 후 이미지 재빌드 성공 |

### 3️⃣ 포트 중복 오류

| 항목 | 내용 |
|------|------|
| **문제** | `Bind for 0.0.0.0:8080 failed: port is already allocated` |
| **원인 가설** | my-site 컨테이너가 8080 포트 선점 중 |
| **확인** | `docker ps -a` → my-site(8080) 실행 중 확인 |
| **해결** | 신규 컨테이너는 8081, 8082 포트로 변경하여 실행 |

---

## 📚 배운 점

- Docker 이미지와 컨테이너의 차이를 실습으로 이해
- 바인드 마운트(`-v 호스트경로:컨테이너경로`)로 실시간 파일 반영 확인
- 볼륨(`docker volume`)을 통한 데이터 영속성 확인
- GitHub Personal Access Token을 활용한 원격 저장소 인증 방법 습득
- 포트 충돌 문제를 `docker ps -a`로 진단하고 해결하는 방법 습득
