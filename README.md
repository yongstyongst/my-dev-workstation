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
| OS | Windows 11 + WSL2 (Ubuntu 26.04.1 LTS) |
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


---

## 🧪 AI 사전평가 보완: 재현 가능한 검증 명령어

> **주의:** 아래는 평가 항목을 재현하고 결과를 수집하기 위한 명령어입니다. GitHub에 작성한 것만으로 실행이 검증되지는 않습니다. 기존 실행 로그와 스크린샷은 과거 실습 기록이며, 현재 상태는 로컬 WSL2 터미널에서 다시 확인해야 합니다.

### 1. WSL2 / Ubuntu 및 권한 확인

Windows PowerShell에서:

```powershell
wsl --status
wsl -l -v
```

Ubuntu(WSL2)에서:

```bash
cat /etc/os-release
whoami
sudo -v
```

**확인할 증거:** WSL 버전 2, Ubuntu 배포판, sudo 인증 성공. 암호나 인증 토큰은 공개 저장소에 올리지 않습니다.

### 2. Docker 설치 상태 및 이미지 목록

```bash
docker --version
docker version
docker info
docker images
```

**확인할 증거:** Docker 클라이언트와 서버 정보, 이미지 목록. Docker 데몬 연결 오류가 발생하면 Docker Engine/Desktop 실행 상태와 WSL 통합 설정을 점검합니다.

### 3. hello-world 실행 확인

```bash
docker run --rm hello-world
```

**성공 기준:** 출력에 `Hello from Docker!`가 나타납니다. 실제 출력 캡처를 첨부하면 검증 근거가 됩니다.

### 4. Dockerfile 및 웹서버 이미지 빌드

이 저장소 루트의 실제 Dockerfile:

```dockerfile
FROM nginx:alpine
COPY site/ /usr/share/nginx/html/
```

저장소 루트에서 실행:

```bash
docker build -t my-webserver:latest .
docker images
```

**성공 기준:** 빌드 명령이 오류 없이 종료되고 이미지 목록에 `my-webserver:latest`가 표시됩니다. 이 Dockerfile은 정적 웹 페이지를 Nginx 기본 문서 경로로 복사합니다.

### 5. 컨테이너 실행과 HTTP 확인

8080 포트가 비어 있을 때:

```bash
docker run -d --name my-web-check -p 8080:80 my-webserver:latest
docker ps
curl -I http://localhost:8080
```

**성공 기준:** 컨테이너가 실행 상태이고 HTTP 응답이 확인됩니다. 이미 8080 포트를 사용하는 컨테이너가 있다면 먼저 `docker ps -a`로 확인하고, 기존 컨테이너를 임의로 삭제하지 않습니다. 필요하면 다른 호스트 포트를 선택합니다.

### 6. 바인드 마운트와 볼륨 검증

바인드 마운트 예시(8081 포트가 비어 있을 때):

```bash
docker run -d --name my-bind-check -p 8081:80 -v "$(pwd)/site:/usr/share/nginx/html:ro" nginx:alpine
curl -I http://localhost:8081
```

Docker 관리 볼륨 예시(8082 포트가 비어 있을 때):

```bash
docker volume create my-site-data
docker run -d --name my-volume-check -p 8082:80 -v my-site-data:/usr/share/nginx/html nginx:alpine
docker volume inspect my-site-data
docker ps -a
```

**주의:** 빈 볼륨을 Nginx 문서 경로에 연결하면 기존 사이트 파일이 보이지 않을 수 있습니다. 볼륨의 데이터 영속성을 증명하려면 컨테이너를 교체한 뒤 같은 볼륨의 파일이 유지되는지 별도로 검사해야 합니다. 기존 README의 8080·8081·8082 기록은 과거 실습 결과입니다.

### 7. Git 설정과 원격 저장소 검증

```bash
git --version
git config --global --list
git status
git branch --show-current
git remote -v
git log --oneline -5
```

**성공 기준:** Git 설정, 현재 브랜치, 원격 저장소 URL, 최근 커밋이 확인됩니다. 이 저장소의 원격 주소는 `https://github.com/yongstyongst/my-dev-workstation`입니다. 개인 이메일, 액세스 토큰, 인증 정보는 공개하지 않습니다.

### 8. 재평가 전 증거 체크리스트

- [ ] WSL2와 Ubuntu 버전 출력 캡처
- [ ] sudo 권한 확인(비밀번호 제외)
- [ ] Docker 클라이언트/서버 버전 출력
- [ ] hello-world 성공 메시지
- [ ] docker build 성공 로그와 docker images 목록
- [ ] docker ps 및 8080 HTTP 응답
- [ ] 바인드 마운트 8081 동작 증거
- [ ] Docker 볼륨 8082 및 데이터 영속성 확인
- [ ] git config, git remote -v, git log 결과
- [ ] 실제 출력 및 오류 해결 과정을 README에 반영

**평가 점수에 대한 안내:** 이 문서 보완은 평가 기준과의 대응성을 높이지만, 로컬 실행 증거 없이 18개 항목의 통과를 보장하지 않습니다.

## 실제 환경 검증 결과 (2026-11-03)

- Ubuntu: 26.04.1 LTS
- WSL2 커널: 6.18.54.1-microsoft-standard-WSL2
- Docker Client / Server Engine: 29.9.2
- Docker Desktop: 4.97.0
- Docker 이미지 빌드: my-webserver:verify 생성 성공 (캐시 사용)
- HTTP 응답: 8080, 8081, 8082 모두 200 OK
- GitHub: main 브랜치 동기화 확인

※ 위 결과는 실제 터미널 출력으로 확인했으며, Docker 볼륨의 재생성 후 데이터 영속성은 별도 검증이 필요합니다.

### Docker 볼륨 영속성 추가 검증 (2026-11-03)

- 테스트 볼륨: persistence-test
- 첫 번째 임시 컨테이너에서 test.txt 생성 및 PERSISTENCE_OK 확인
- 첫 번째 컨테이너 자동 삭제 후 새 컨테이너에서 PERSISTENCE_OK 재확인
- 결과: 컨테이너 삭제 후에도 Docker 명명된 볼륨의 데이터 유지 확인
- 기존 웹서버의 my-vol 재생성 검증은 수행하지 않음
