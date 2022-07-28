# Testcontainers 도커 Compose 사용하기

## Docker compose란?
- 도커 컨테이너를 여러개를 띄워 사용하는 경우에 컨테이너간의 관계, 네트워크, 볼륨 설정 등의 일련의 동시 관리를 하는 것을 말한다.

## 과정
1. docker-compose.yml 작성
	- 각 컨테이너의 실행 정의를 작성
2. docker-compose up 커맨드를 입력하여 docker-compose.yml에 작성한 컨테이너를 실행

## 공식문서
- Docker compose: [https://docs.docker.com/compose/](https://docs.docker.com/compose/)
- Testcontainers의 docker compose: [https://www.testcontainers.org/modules/docker_compose/](https://www.testcontainers.org/modules/docker_compose/)