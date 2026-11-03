## ⚙️ 실행 환경

| 항목 | 내용 |
|------|------|
| OS | Windows 11 + WSL2 (Ubuntu 22.04) |
| 쉘/터미널 | bash / Windows Terminal |
| Docker 버전 | 29.9.2 (build a82e528) |
| Git 버전 | 2.53.0 |

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

## 🚨 트러블슈팅

### 3️⃣ 포트 중복 오류

| 항목 | 내용 |
|------|------|
| **문제** | `Bind for 0.0.0.0:8080 failed: port is already allocated` |
| **원인 가설** | my-site 컨테이너가 8080 포트 선점 중 |
| **확인** | `docker ps -a` → my-site(8080) 실행 중 확인 |
| **해결** | 신규 컨테이너는 8081, 8082 포트로 변경하여 실행 |
