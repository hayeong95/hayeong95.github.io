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
last_modified_at: 2023-01-27
---



이슈: tensorflow docker image에서 `M1` 칩 지원이 안됨
- `qemu: uncaught target signal 6 (Aborted) - core dumped`

해결방법:  `linux/arm64/v8`로 인식되도록 도커 이미지 빌드/런 시 옵션 추가
- `Rosetta 2` 설치 선행되어야 함
  
  - 참고: https://support.apple.com/ko-kr/HT211861

- 도커 이미지 빌드/런 명령어
  
  ```powershell
  docker build --platform=linux/arm64/v8 . -t tensorflow
  docker run --platform=linux/arm64/v8 tensorflow
  ```
  
  출처: https://github.com/tensorflow/tensorflow/issues/52845#issuecomment-1272337911

- Dockerfile
  
  ```powershell
  FROM python:3.7-slim
  
  COPY requirements.txt /home/usr/app/requirements.txt
  WORKDIR /home/usr/app/
  
  RUN apt update
  # python cv related packages
  RUN apt install -y libglib2.0-0 libgl1-mesa-glx
  RUN apt install -y graphviz gcc git vim
  
  RUN pip install --upgrade pip setuptools wheel
  RUN pip install tensorflow==2.10.0 # tensorflow-io==0.27.0
  RUN pip install -r requirements.txt
  ```
