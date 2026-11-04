# E1-1 보너스 과제 3: Docker Compose 운영 명령어

## 1. 실습 환경
- Ubuntu 26.04.1 LTS (WSL2)
- Docker Engine 29.9.3
- Docker Compose v5.7.0
- Git 2.53.0
- Nginx 웹 서버 (8080:80)

## 2. 서비스 실행 (up)
명령어: `sudo docker compose up -d --build`

결과:
- Image my-dev-workstation-web Built
- Network my-dev-workstation_default Created
- Container my-dev-workstation-web-1 Started
- `curl http://localhost:8080` 실행 후 HTML 응답 확인

## 3. 상태 확인 (ps)
명령어: `sudo docker compose ps`

결과:
- 컨테이너: my-dev-workstation-web-1
- 상태: Up 52 seconds
- 포트: 0.0.0.0:8080->80/tcp

## 4. 로그 확인 (logs)
명령어: `sudo docker compose logs`

결과:
- Configuration complete; ready for start up
- GET / HTTP/1.1 응답 코드 200
- 웹 서버의 정상적인 요청 처리 확인

## 5. 서비스 종료 (down)
명령어: `sudo docker compose down`

결과:
- Container my-dev-workstation-web-1 Removed
- Network my-dev-workstation_default Removed

검증: `sudo docker compose ps -a` 결과 컨테이너 목록이 비어 있음.

## 6. 학습 결과
Docker Compose의 up, ps, logs, down 명령어로 컨테이너 실행, 상태 확인, 로그 분석, 종료를 직접 수행하였다. 기존 Dockerfile과 compose.yaml을 활용해 동일한 서비스를 재현할 수 있음을 확인하였다.
