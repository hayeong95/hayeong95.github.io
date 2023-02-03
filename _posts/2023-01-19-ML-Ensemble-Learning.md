---
title: "[ML/머신러닝] 앙상블 학습 (Ensemble Learning)"
excerpt: "머신러닝 앙상블 학습 정리"

categories:
  - machine-learning
tags:
  - [ML, 머신러닝, EnsembleLearning, 앙상블학습, bagging, boosting, randomforest, adaboost]

toc: true
toc_sticky: true

date: 2023-01-19
last_modified_at: 2023-01-19
---

### Ensembling Learning

- 머신러닝에서 성능향상을 위해 여러 모델(`weak models`)을 같이 사용(`aggregation`)하는 방법
  
  - weak model 은 `variance` 또는 `bias`에 취약한 모델을 의미, ensembling은 여러 모델을 합해서 variance 또는 bias를 낮추는 방법을 제시함

- 방법
  
  - weak model을 선택
    
    - `homogeneous`: 종류가 같은 모델을 다르게 학습 (bagging, boosting)
    
    - `heterogeneous`: 종류가 다른 모델을 학습 (stacking)
  
  - aggregation 방법을 선택
    
    - `variance` 감소: bagging
    
    - `bias` 감소: boosting, stacking

- 예시: `random forest`, `Adaboost`, `mixture of experts`



### Bootstrap

- 여러 weak 모델을 학습시키기 위해 일반적으로 training data를 `RSR`(random sampling w/ replacement) 이용하여 샘플링하는 방법



### Bagging (Boostrap aggregating)

- Bootstrap으로 샘플링한 데이터로 여러 모델을 `parallel`하게 학습시켜 평균 값을 구함

- 특징: robustness, lower variance (overfitting 해소)

- 예시: `random forest`, `dropout`
  
  - Random Forest: Decision Tree의 variance를 감소



### Boosting

- 학습 모델에서 성능이 낮게 나온 부분을 해결하기 위해 데이터에 가중치를 두어 다음 모델을 `sequential` 하게 학습시켜 가중치 기반 평균 값을 구함

- - 에러가 큰 데이터에 큰 가중치를 부여하는 방식

- 특징: lower bias (underfitting 해소)

- 예시: `AdaBoost`, `gradient boosting machines`



### Stacking

- `non-homogeneous`한 weak model을 `base learner`로 사용, base learner의 예측값을 input으로 사용하는 `meta-model`을 학습 

- 학습 데이터를 둘로 나누어, 각각 `base learner`와 `meta-model`을 학습시키는 데 사용
  
  ex. `MoE`(Mixture of Experts)
  
  - task를 `subtask`로 나누고, 각 `subtask`를 잘 수행하는 expert를 학습
  
  - 어떤 expert를 얼마만큼의 `확률`로 선택할 지 결정하는 `gating model`을 사용하여 aggregation(ex. argmax, weighted sum) 진행



참고 자료

- https://medium.com/towards-data-science/ensemble-methods-bagging-boosting-and-stacking-c9214a10a205
