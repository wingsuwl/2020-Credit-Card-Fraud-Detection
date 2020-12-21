# 2020-Credit-Card-Fraud-Detection
The project in Machine Learning Class.

**Notion Link** : https://www.notion.so/d4fd5b48a527490e9ee5dc56c9b8f9fc?v=5747d966126b4ac8b37db71905959220

## Anomaly Detection with Extremely Imbalanced Data


### Motivation
불균형 데이터를 효과적으로 학습할 방법을 모색해 최적의 Input 전략과 모델 제시

### Experiment
1. Data 전처리 - Scaling, 이상치 제거
2. Raw Data(scaled data), Under Sampling Data, Over Sampling Data 비교
3. 하이브리드 모델( 앙상블과 오토인코더) 구현 후 성능 평가

### Used Model
Logistic Regression, Random Forest, SVM, KNN, Ada Boost, Extra Trees, AutoEncoder

### Data
**Kaggle** : https://www.kaggle.com/mlg-ulb/creditcardfraud

<img width="272" alt="스크린샷 2020-12-21 오전 10 32 12" src="https://user-images.githubusercontent.com/54855238/102730399-ff665d80-4377-11eb-92f1-3a884c7f5e12.png">

This is Highly Imbalanced Data.

### Raw Data vs Under Sampling vs Over Sampling
=> 분류기에서는 Over Sampling, Neural Net에서는 Raw Data가 가장 성능이 좋을 것으로 예측 됨.

<img width="468" alt="스크린샷 2020-12-21 오전 10 36 32" src="https://user-images.githubusercontent.com/54855238/102730567-7a2f7880-4378-11eb-80f6-578fabd53fcd.png">
<img width="517" alt="스크린샷 2020-12-21 오전 10 36 38" src="https://user-images.githubusercontent.com/54855238/102730574-7c91d280-4378-11eb-8f10-efaebf87a7ae.png">
<img width="541" alt="스크린샷 2020-12-21 오전 10 36 53" src="https://user-images.githubusercontent.com/54855238/102730581-7e5b9600-4378-11eb-96d7-ea79ab14e481.png">

### Ensemble
- Combination 1 : Logistic Regression, Random Forest, KNN, SVC
- Combination 2 : Comb1 + Ada Boost, Extra Trees
- Combination 3 : Random Forest, Extra Trees, Ada Boost

1. Voting
  => Over Sampling을 넣을 때 AUC score 는 향상되지만 Precision 은 낮아지는데, 특히 SVM, KNN이 들어가는 Comb1, 2 의 경우가 그러함.
  => Comb3 의 경우 전체적으로 좋은 성능을 보임

2. Stacking
  => Voting 보다 AUC가 향상되지만 학습 시간이 매우 오래 걸림.
  
### Hybrid Model
<img width="364" alt="스크린샷 2020-12-21 오전 10 42 07" src="https://user-images.githubusercontent.com/54855238/102730792-35f0a800-4379-11eb-9634-b57147347253.png">

1. With Raw Data
  => 높아진 Recall, 낮아진 Precision, 전반적으로 좋아진 성능
  => Random Forest의 경우 단독 모델 성능이 더 좋음
  
  
2. With Over Sampling Data
  => 높아진 Recall, 많이 낮아진 Precision, 전반적으로 나빠진 성능
  => Random Forest의 경우 Precision이 많이 낮아지지 않음
  
### Result of Experiments
<img width="322" alt="스크린샷 2020-12-21 오전 10 45 13" src="https://user-images.githubusercontent.com/54855238/102730920-9ed82000-4379-11eb-98d1-b22c4ddd70f8.png">



### Conclusion
- Under Sampling으로 학습하면 Precision이 낮다.
- 분류기의 경우 Over Sampling으로 학습 시 Knn, SVC 등 모델에서는 Precision이 낮아지지만 Random Forest 와 이를 이용해 조합한 앙상블 모델에서는 OVer Sampling 결과가 좋았다. Random Forest, Ada Boost, Extra Trees 를 조합한 모델이 가장 결과가 좋음.
- 신경망은 매우 불균형한 Raw Data로도 평균 0.9의 AUC score 달성.


### Proposal of Future Project
- 새로운 데이터 구축
- 전반적으로 Random Forest의 성능이 좋았다는 점에서 Forest 모델을 이용한 이상 탐지 기법 연구
