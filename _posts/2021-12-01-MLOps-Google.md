---
title: "[요약] MLOps: Continuous delivery and automation pipelines in machine learning"
excerpt: "Google Cloud에서 작성한 MLOps에 대한 문서 요약/정리"

categories:
  - MLOps
tags:
  - [MLOps, Google Cloud]

toc: true
toc_sticky: true

date: 2021-12-01
last_modified_at: 2021-12-01
---

원문: [MLOps: Continuous delivery and automation piplelines in machine learning](https://cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning#characteristics_2)

- MLOps? ML 시스템에 대해 CI/CD/CT를 진행하기 위한 기법
- Why MLOps? 실제로 ML code 자체는 ML 시스템에서 작은 부분만을 차지함
  - [Machine Learning: The high-interest credit card of technical debt(NIPS 2014) 참고](https://research.google/pubs/pub43146/)
- 해당 문서는 아래 세 가지 주제로 구성
  - DevOps vs. MLOps
  - Steps for developing ML models
  - MLOps maturity levels

## DevOps vs. MLOps

DevOps는 큰 규모의 SW시스템에 대해 CI/CD를 효과적으로 지원하는 방법이다. MLOps는 기존 SW시스템 대비 ML시스템이 지니는 아래의 특징들을 고려할 필요가 있다.
- ML 프로젝트의 경우, ML 연구원과 해당 서비스를 상용화하는 SW 엔지니어가 주로 구분되어 있음
- ML의 경우 알고리즘, 설정 파라미터 값 등의 추적을 통해 재사용성을 높일 수 있어야 함
- ML 시스템은 데이터, 학습 모델 등 더 많은 검증을 필요로 함
- ML 시스템은 상용 후에도 지속적으로 재학습/배포가 이루어져야 함
- ML 시스템이 지속적으로 신규 데이터를 반영하지 못하면, 그 모델의 성능이 떨어지게 됨

최종적으로, ML시스템에서의 CI는 SW 구성요소 뿐 아니라 검증 데이터, 검증 모델 등 다방면으로 테스트가 필요하며, CD는 단일 서비스가 아닌 시스템 전체에서 이루어져야 하며 다른 서비스에도 자동적으로 적용이 가능해야 한다. 추가적으로 CT(Continuous Training) 즉, 지속적으로 재학습/배포가 이루어질 수 있어야 한다.

## Data science steps for ML

1. Data extraction: ML task를 위한 다양한 데이터 수집/통합
2. Data analysis: ML 모델 설계를 위한 형태로의 데이터 분석
3. Data preparation: 모델 학습을 위한 데이터 정제 및 학습/검증/테스트 용으로 분류 진행, 필요한 경우 데이터 변환 및 feature engineering 진행
4. Model training: 여러 알고리즘 활용 및 하이퍼파라미터 튜닝을 통한 최적의 ML모델 학습
5. Model evaluation: 테스트 셋을 이용한 모델 평가
6. Model validation: 상용 적용을 위한 모델 검증
7. Model serving: 모델 상용 적용
  - API를 이용하여 실시간 예측 결과 제공
  - edge/mobile에 임베딩
  - batch로 예측 결과 제공
8. Model monitoring: 예상되는 성능 모니터링을 통해 필요시 ML 프로세스 재 진행

## MLOps level (to be updated)
#0. Manual process
#1. ML pipeline automation
#2. CI/CD pipeline automation

