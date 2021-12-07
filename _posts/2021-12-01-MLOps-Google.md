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
last_modified_at: 2021-12-07
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

DevOps는 큰 규모의 SW시스템에 대해 CI/CD를 효과적으로 지원하는 방법입니다. 유사하게, MLOps는 기존 SW시스템 대비 ML시스템이 지니는 아래의 특징들을 고려할 수 있어야 합니다.

- ML 프로젝트의 경우, ML 연구원과 해당 서비스를 상용화하는 SW 엔지니어가 주로 구분되어 있음
- ML의 경우 알고리즘, 설정 파라미터 값 등의 추적을 통해 재사용성을 높일 수 있어야 함
- ML 시스템은 데이터, 학습 모델 등 더 많은 검증을 필요로 함
- ML 시스템은 상용 후에도 지속적으로 재학습/배포가 이루어져야 함
- ML 시스템이 지속적으로 신규 데이터를 반영하지 못하면, 그 모델의 성능이 떨어지게 됨

최종적으로, ML시스템에서의 CI는 SW 구성요소 뿐 아니라 검증 데이터, 검증 모델 등 다방면으로 테스트가 필요하며, CD는 단일 서비스가 아닌 시스템 전체에서 이루어져야 하며 다른 서비스에도 자동적으로 적용이 가능해야 합니다. 추가적으로 CT(Continuous Training) 즉, 지속적으로 재학습/배포가 이루어질 수 있어야 합니다.

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
ML설계 및 적용 전 단계가 수동으로 진행되며, 특징은 아래와 같습니다.

- 데이터 분석, 준비, 모델 학습, 검증의 과정이 각각 수동으로 이루어지고, 이 과정은 동작가능한 모델이 생성되기 전까지 data scientist가 직접 코드를 작성하고 실행하여 수행됨
- 모델을 생성하는 data scientist와 그 모델을 상용 서비스에 적용하는 엔지니어가 분리되므로, Trainig-Serving Skew를 유발하게 됨
- 모델의 변경이나 재 학습이 드물게 일어남 -> CI/CD는 무시됨
- 상용 서비스에 적용되는 것은 학습된 모델에 한정되며, 전체 ML시스템은 적용시키지 않음
- 모델 성능에 대한 지속적인 모니터링이 어려움

이러한 특징들로 인해 엔지니어링 팀은 API 구성, 테스트, 적용을 위한 복잡한 설정 과정과 보안, 침체, 부하 및 canary test 등을 수행해야 합니다. 그리고 새 버전의 ML보델을 적용하기 위해선 트래픽이 수반되는 모든 예측을 수행해내도록 테스트하는 과정이 필요합니다.

MLOps lv.0 은 주로 처음 ML을 적용하는 단계에서 사용됩니다. 위와 같은 수동적인 방법은 거의 변동사항이 없는 경우에 충분할지도 모르나, 다양한 변화에 적응이 필요한 실제 상황에서는 이런 모델은 붕괴하기 쉽습니다. 이를 방지하기 위해,
- 모델의 성능을 지속적으로 모니터링하고,
- 모델을 최신 데이터를 이용하여 자주 재학습시키고,
- 지속적으로 새로운 모델 구현 방법들을 실험해보아야 합니다.

다음장에 이러한 수동 과정에서 오는 문제들을 극복하기 위한, MLOps의 CI/CD/CT를 하기 위한 ML training pipeline에 대한 설명이 이어집니다.

#1. ML pipeline automation
#2. CI/CD pipeline automation

