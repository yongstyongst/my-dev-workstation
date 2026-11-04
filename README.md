# 🖥️ 나의 개발 워크스테이션

> WSL2 + Ubuntu + Docker 환경 구축 및 웹 서버 배포 실습 프로젝트

---

## 📁 프로젝트 구조

```text
my-dev-workstation/
├── Dockerfile          # 웹서버 이미지 빌드 설정
├── README.md           # 프로젝트 설명 및 실행·검증 문서
├── site/               # 웹서버에 제공할 정적 콘텐츠
│   └── index.html      # 메인 웹 페이지
├── practice/           # Linux 파일 및 디렉토리 실습 자료
│   └── hello.txt       # 파일 관리 실습 파일
└── evidence/            # 실제 실행 결과 및 평가 증거 보관
    ├── 01-directory-created.txt
    ├── 02-file-created.txt
    ├── 03-file-moved.txt
    ├── 04-file-deleted.txt
    ├── 05-chmod-755.txt
    ├── 06-permission-comparison.txt
    ├── 07-docker-info.txt
    ├── 08-hello-world.txt
    ├── 09-docker-images.txt
    ├── 10-docker-build.txt
    ├── 11-assessment-image.txt
    ├── 12-http-responses.txt
    ├── 13-volume-persistence.txt
    ├── 14-git-configuration.txt
    ├── 15-port-mapping-http.txt
    └── permission-test.txt
```

### 디렉토리 구성 및 설계 기준

- **Dockerfile:** 웹서버 이미지 생성에 필요한 설정을 프로젝트 루트에 배치하여 빌드 명령을 간결하게 유지한다.
- **site/:** 웹페이지와 Docker 실행 설정을 분리하여 콘텐츠 수정 및 유지보수가 쉽도록 구성한다.
- **practice/:** Linux 명령어 실습에 사용하는 파일을 별도 관리하여 실제 서비스 파일과 혼동하지 않도록 한다.
- **evidence/:** Docker, Linux, Git의 실제 실행 결과를 저장하여 작업의 재현성과 검증 가능성을 높인다.
- **README.md:** 환경 구성, 실행 방법, 검증 결과 및 문제 해결 과정을 통합 관리한다.

이러한 구조는 파일의 역할을 명확하게 구분하고, 향후 웹 콘텐츠와 실습 항목이 증가하더라도 관리하기 쉽도록 설계하였다.
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

## 📖 핵심 기술 개념 및 실습 원리

### 바인드 마운트와 Docker 볼륨 비교

| 구분 | 바인드 마운트(Bind Mount) | Docker 볼륨(Volume) |
|---|---|---|
| 데이터 위치 | 호스트의 지정된 경로 | Docker가 관리하는 저장 공간 |
| 관리 주체 | 사용자 및 호스트 운영체제 | Docker |
| 주요 목적 | 호스트 파일과 컨테이너 파일 공유 | 컨테이너 데이터 영속성 확보 |
| 장점 | 파일 수정이 즉시 반영되어 개발 및 테스트에 편리함 | 컨테이너를 삭제하거나 교체해도 데이터 유지 가능 |
| 단점 | 호스트 경로와 권한 설정에 영향을 받음 | 호스트에서 직접 파일을 관리하기 상대적으로 불편함 |
| 권장 상황 | 웹 페이지 개발, 소스 코드 수정 및 실시간 반영 | 데이터베이스, 운영 데이터 및 장기 보관 |

**실습 적용 및 선택 기준**

본 프로젝트에서는 웹 페이지의 수정 사항을 실시간으로 확인하기 위해 바인드 마운트를 사용하였다. 반면 Docker 볼륨은 컨테이너의 생명주기와 독립적으로 데이터를 보존해야 할 때 적합하다. 따라서 개발 단계에서는 바인드 마운트를, 데이터 영속성이 중요한 운영 환경에서는 Docker 볼륨을 우선적으로 고려한다.

---

### 1. Docker 이미지와 컨테이너의 실행 흐름

Docker 이미지는 애플리케이션 실행에 필요한 파일과 라이브러리, 실행 설정을 포함하는 읽기 전용 템플릿이다. 컨테이너는 이미지를 기반으로 생성되어 실제 프로세스를 실행하는 독립적인 실행 환경이다.

```bash
docker build -t my-webserver:latest .
docker run -d --name my-web-check -p 8080:80 my-webserver:latest
docker ps
docker exec -it my-web-check sh
```

이미지를 빌드한 후 컨테이너를 생성하고 실행한다. 실행 중인 컨테이너 내부의 변경 사항은 기본적으로 해당 컨테이너의 쓰기 가능 계층에 기록된다. 컨테이너를 삭제하면 이 계층의 데이터는 사라질 수 있으므로 영속성이 필요한 데이터는 볼륨이나 바인드 마운트로 관리한다.

### 2. 네트워크 네임스페이스와 포트 포워딩

Linux 네트워크 네임스페이스는 프로세스의 네트워크 인터페이스, IP 주소, 라우팅 테이블 및 포트 공간을 분리하는 기능이다. Docker 컨테이너는 독립적인 네트워크 환경을 사용하므로 컨테이너 내부의 80번 포트가 호스트에서 자동으로 접근 가능한 것은 아니다.

```bash
docker run -d --name my-web-check -p 8080:80 my-webserver:latest
curl -I http://localhost:8080
```

`-p 8080:80`은 호스트의 8080번 포트로 들어온 연결을 컨테이너의 80번 포트로 전달하도록 설정한다. Docker는 네트워크 드라이버와 포트 게시 설정을 통해 이 연결을 처리한다. 포트 게시가 없으면 별도의 네트워크 연결 설정 없이는 호스트에서 컨테이너 서비스에 직접 접근하기 어렵다.

### 3. 절대경로와 상대경로의 선택 기준

- 절대경로(Absolute Path): 루트 디렉토리(`/`)부터 시작하는 전체 경로이다. 현재 작업 디렉토리와 관계없이 동일한 위치를 지정해야 할 때 사용한다.
- 상대경로(Relative Path): 현재 작업 디렉토리를 기준으로 파일이나 디렉토리 위치를 지정한다. 프로젝트 내부 파일을 참조하거나 작업 디렉토리 기준으로 명령을 실행할 때 유용하다.

```bash
# 절대경로
cd /home/dumarii6559/my-dev-workstation

# 상대경로
cd ~/my-dev-workstation
cd site

# Docker 빌드 컨텍스트: 현재 디렉토리
cd ~/my-dev-workstation
docker build -t my-webserver:latest .
```

절대경로는 자동화 스크립트나 외부 경로를 명확하게 지정할 때 유리하다. 상대경로는 프로젝트 이동과 재사용이 편리하지만 실행 위치에 따라 결과가 달라질 수 있다. Docker 빌드 명령의 마지막 점(`.`)은 현재 디렉토리를 빌드 컨텍스트로 지정한다.

**실제 실습 결과 (2026-11-03)**

- 현재 작업 디렉터리: `/home/dumarii6559/my-dev-workstation`
- 절대경로: `/home/dumarii6559/my-dev-workstation/site/index.html`
- 상대경로: `site/index.html`
- 검증 결과: 두 경로가 동일한 파일을 가리키는 것을 확인하였다.
- 실행 증거: `evidence/17-path-verification.txt`

### 4. Linux 파일 권한과 숫자 표기 규칙

Linux 파일 권한은 소유자(User), 그룹(Group), 기타 사용자(Other)의 세 범위로 구분하며 읽기(r), 쓰기(w), 실행(x) 권한으로 구성한다.

| 권한 | 숫자 | 의미 |
|---|---:|---|
| --- | 0 | 권한 없음 |
| --x | 1 | 실행 |
| -w- | 2 | 쓰기 |
| -wx | 3 | 쓰기 + 실행 |
| r-- | 4 | 읽기 |
| r-x | 5 | 읽기 + 실행 |
| rw- | 6 | 읽기 + 쓰기 |
| rwx | 7 | 읽기 + 쓰기 + 실행 |

```bash
chmod 644 evidence/permission-test.txt
ls -l evidence/permission-test.txt

chmod 755 evidence/permission-test.txt
ls -l evidence/permission-test.txt
```

644는 소유자에게 읽기·쓰기 권한을 부여하고 그룹과 기타 사용자에게 읽기 권한을 부여한다. 755는 소유자에게 읽기·쓰기·실행 권한을 부여하고 그룹과 기타 사용자에게 읽기·실행 권한을 부여한다.

실습 결과 644는 `-rw-r--r--`, 755는 `-rwxr-xr-x`로 확인하였다. 일반 데이터 파일은 보통 644, 디렉토리와 실행 스크립트는 용도에 따라 755를 사용한다.

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

컨테이너 실행 전 호스트 포트의 사용 여부를 확인한다.

```bash
docker ps --format 'table {{.Names}}\\t{{.Ports}}'
ss -ltn | grep ':18080 ' || echo 'PORT_18080_AVAILABLE'
```

포트가 사용 가능하면 이미 빌드한 이미지를 이용해 컨테이너를 실행한다.

```bash
docker run -d --name my-web-assessment -p 18080:80 my-webserver:assessment
docker ps --filter name=my-web-assessment
```

`-p 18080:80`은 호스트의 18080 포트를 컨테이너 내부의 80번 포트에 연결한다.

HTTP 응답과 웹페이지 본문을 확인한다.

```bash
curl -i http://localhost:18080
```

**실제 검증 결과 (2026-11-03):** 컨테이너 `my-web-assessment` 실행, 포트 매핑 `18080→80`, HTTP `200 OK`, Nginx 응답 및 HTML 본문 반환을 확인했다. 실행 결과는 `evidence/15-port-mapping-http.txt`에 저장했다.

검증이 끝나면 테스트 컨테이너만 정리한다.

```bash
docker rm -f my-web-assessment
docker ps
```

**주의:** 포트 충돌이 발생하면 `docker ps`와 `ss -ltn`으로 사용 현황을 확인한다. 기존 컨테이너를 임의로 삭제하지 말고 사용 가능한 다른 호스트 포트를 선택한다.

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
- [x] Docker 클라이언트/서버 버전 출력
- [x] hello-world 성공 메시지
- [x] docker build 성공 로그와 docker images 목록
- [x] docker ps 및 8080 HTTP 응답
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

cat > evidence/compose-operations.md <<'EOF'
# E1-1 보너스 과제 3: Docker Compose 운영 명령어

## 1. 실습 환경
- OS: Ubuntu 26.04.1 LTS (WSL2)
- Docker Engine: 29.9.3
- Docker Compose: v5.7.0
- Git: 2.53.0
- 서비스: Nginx 웹 서버
- 포트: 8080:80

## 2. Compose 서비스 실행

명령어:
```bash
sudo docker compose up -d --build
