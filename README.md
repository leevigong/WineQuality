# WineQuality_Classification

## Dataset
WineQT.csv는 기존 모델에서 사용하던 dataset이고, 데이터셋을 추가확보한 상태가 WineQT_add.csv이다.

WineQT_add.csv는 총 12개의 행으로 이루어져있으며, 행의 각 특성은 fixed acidity, volatile acidity, citric acid, residual sugar, chlorides, free sulfur dioxide, total sulfur dioxide, density, pH, sulphates, alcohol, quality로 이루어져 있다.

WineQT.csv는 총 13개의 행으로 이루어져 있으며, WineQT_add.csv의 12개 특성에 Id가 추가된 상태였었고, 전처리과정에서 Id는 drop하였다.

WineQT.csv가 1143개 데이터, WineQT_add가 2742개 데이터로 이루어져 있다. 

## Model

학습에 사용한 모델은 RandomForestClassifier, DecisionTreeClassifier, KNeighborsClassifier, SVC, LogisticRegression을 사용하였다.  

## 정확도를 향상시킬 방안
### 1) 학습데이터량의 확보 -> Wine Quality 1) Datasets_Increase

기존모델의 경우 데이터량이 1143개 밖에 되지않아 정확도가 87%정도 나오지 않았나 하는 가설에서 출발하였다. dataset확보를 위해 kaggle.comd에서 WineQuality에 관한 데이터를 더 찾아보았다. 혹여나 기존 모델이 쓰는 dataset과 같을 수 있어 유사도 검증을 통해 추가적으로 1599개의 데이터를 추가적으로 확보하였다.

데이터를 추가 확보한 것만으로도 정확도의 성능이 96%로 눈에 띄게 올라감을 보여주었다.

### 2) 가중치 부여 후 정규화 -> Wine Quality 2) Correlation

분류에 큰 영향을 끼치는 데이터에 가중치를 부여하면 classfication에 더 도움을 줄 수 있을까 하여 가중치를 부여하는 방향으로 데이터셋에 가중치를 곱하는 방향으로 학습을 진행하였다.

생각한 요소는 '상관계수'였다. quality와 다른 특성들간의 상관계수를 구하여 그 상관계수를 단순히 데이터에 곱한 후 정규화를 진행하였다. 하지만, 정확도가 83%정도로 떨어졌다.

상관계수는 -1과 1사이에서 값을 가지기 때문에 큰 영향을 주지 않았나는 추론에 상관계수에 10배의 값을 곱해주었더니 오히려 정확도가 83% 정도로 떨어졌다. 

음수값들이 오히려 정확도를 떨어뜨릴 수 있다는 가정하에 상관계수의 절댓값을 곱한 값들로 학습을 진행하였지만, 정확도는 0.04% 정도 상승하였다. 

다른 방안으로 1에 상관계수를 더하여 가중치를 설정해보았다. 이 방법 또한 정확도 상승에 영향을 주지 않았다.

1에 가중치의 절댓값을 더한것들을 20배하여 가중치를 설정하는 방법 또한 정확도 상승에 영향을 주지 않았다.

결국, 상관계수의 절댓값을 가중치로 설정하였을 경우 미미한 정확도 상승이지만 가장 좋은 정확도를 보여주었다.

상관계수 말고 다른 요소들로 가중치를 설정하려는 시도 또한 해보았다. '유전알고리즘'을 통해 가중치를 설정하는 방안을 생각해보았지만, 유전알고리즘은 현재 WineQulity의 데이터셋으로 가중치를 설정하기엔 적합한 알고리즘이 아니었다.


### 3) 이진분류로 재라벨링 -> Wine Quality 3) Binary_Classification

현재 datase의 정답지에 해당하는 quality는 2~8의 범위의 정수값들을 가지고 있다. 이진분류를 통한 재라벨링을 통해 학습을 하면 SVM, LogisticRegression과 같은 선형모델들을 효과적으로 활용해보기로 하였다.

이진분류의 기준을 정하기위하여 데이터의 분포도를 quality를 기준으로 살펴보았다. 평균은 5.6 이지만, quality의 50% 와 75%에 해당하는 값 모두 6.0인 것을 통해 이진분류의 기준을 6.5로 정하였다.

2 와 6.5 사이의 quality값은 'bad'라는 집단으로, 6.5 와 8 사이의 quality값은 'good'이라는 집단으로 재라벨링하여 학습을 진행하여 선형모델의 장점을 활용하기로 하였다.

이진분류하였을때 정확도는 96%로 상승함을 보였고, SVM과 LogicalRegression 모델의 성능 또한 기존 방안인 데이터양을 늘리는 방법과 가중치 부여 후 정규화 방법에 비해 확연히 좋은 결과를 보여주었다. 데이터양을 늘려주었을때는 SVM은 70% 정확도를 LogicalRegression은 52% 정확도를 보였고, 가중치를 부여 후 정규화 하였을 때는 SVM은 71%, LogicalRegression은 58%의 정확도를 보였다. 이진분류하였을 때는 각각 89%, 83%의 정확도를 보여주었다. 이를 통해 SVM과 LogicalRegression은 이진분류에 탁월한 성능을 보여줌을 알았고, 이를 통해 이진분류로 재라벨링을 하여 SVM과 LogicalRegression을 활용할 수 있음을 알았다. 

