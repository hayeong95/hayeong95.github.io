---
title: "[Docker] Docker Compose 사용 방법"
excerpt: "Docker Compose 사용 방법을 간단하게 소개"

categories:
  - dev
tags:
  - [Docker, Container, DockerCompose]

permalink: /dev/docker-compose/

toc: true
toc_sticky: true

date: 2024-01-31
last_modified_at: 2024-01-31
---


## 사용 시나리오
- Docker Image 빌드를 위한 정보는 `Dockerfile`로 관리
- 해당 `Dockerfile`을 이용하여 컨테이너 앱을 띄우기 위한 서비스 정의는 `docker-compose`로 관리

## Docker Compose 파일 작성하기
```vim
# compose.yml
version: "3" # 도커 컴포즈 버전
services:
  container_1:
    build: # 이미지를 도커파일로 빌드 필요한 경우
      context: . # 도커파일 위치
      dockerfile: DockerFile # 도커파일 파일명
    image: # 빌드될 도커 이미지명
    ports:
      - {host port}:{container port}
    volumes:
      - 
  container_2:
    depends_on:
      - container_1
    environment:
      - # 환경변수 지정
    image:
    command:
    working_dir: 
    restart:
    networks:
    
volumes:

networks:

```


## 유용한 명령어
```
docker compose up --build
docker compose down
docker compose start
docker compose stop
docker compose restart
docker compose ps
docker compose logs 
```