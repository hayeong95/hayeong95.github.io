---
title: "[Docker] M1 Chip에서 Docker Container 환경으로 Tensorflow 사용하기"
excerpt: "M1 Chip에서 Docker Container 환경으로 Tensorflow 사용하기"

categories:
  - docker
tags:
  - [Docker, Container, M1, Tensorflow]

permalink: /docker/docker-macos/

toc: true
toc_sticky: true

date: 2023-01-27
last_modified_at: 2023-02-17
---

## 이슈: tensorflow docker image에서 `M1` 칩 지원이 안됨
- `qemu: uncaught target signal 6 (Aborted) - core dumped`

## 해결방법:  도커 이미지 빌드/런 시 `platform` 옵션 추가
- `Rosetta 2` 설치 선행되어야 함
  
  - 참고: https://support.apple.com/ko-kr/HT211861

- 도커 이미지 빌드/런 명령어
  
  ```powershell
  docker build --platform=linux/amd64 . -t tensorflow
  docker run --platform=linux/amd64 tensorflow
  ```
  - docker desktop 에 경고 문구 보임
  - platform을 `linux/arm64/v8` 로 지정 시, 경고 문구 사라지고 tensorflow 잘 작동하나 여전히 `amd64` 기반이 아니여서 사용 시 일부 이슈 존재
  - 우선 `linux/amd64`로 사용
  

- Dockerfile 예시
  
  ```powershell
  FROM python:3.7-slim
  
  COPY requirements.txt /home/usr/app/requirements.txt
  WORKDIR /home/usr/app/
  
  RUN apt update
  # python cv related packages
  RUN apt-get install -y libglib2.0-0 libgl1-mesa-glx
  RUN apt-get install -y graphviz gcc git vim
  
  RUN pip install --upgrade pip setuptools wheel
  RUN pip install tensorflow==2.10.0 # tensorflow-io==0.27.0
  RUN pip install -r requirements.txt
  ```
