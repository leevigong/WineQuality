# WineQuality_Classification

## Dataset
WineQT.csv는 기존 모델에서 사용하던 dataset이고, 데이터셋을 추가확보한 상태가 WineQT_add.csv이다.

WineQT_add.csv는 총 12개의 행으로 이루어져있으며, 행의 각 특성은 fixed acidity, volatile acidity, citric acid, residual sugar, chlorides, free sulfur dioxide, total sulfur dioxide, density, pH, sulphates, alcohol, quality로 이루어져 있다.

WineQT.csv는 총 13개의 행으로 이루어져 있으며, WineQT_add.csv의 12개 특성에 Id가 추가된 상태였었고, 전처리과정에서 Id는 drop하였다.

WineQT.csv가 1143개 데이터, WineQT_add가 2742개 데이터로 이루어져 있다. 

## 정확도를 향상시킬 방안
### 1) 학습데이터량의 확보 -> Wine Quality 1) Datasets_Increase

기존모델의 경우 데이터량이 1143개 밖에 되지않아 정확도가 87%정도 나오지 않았나 하는 가설에서 출발하였다. dataset확보를 위해 kaggle.comd에서 WineQuality에 관한 데이터를 더 찾아보았다. 혹여나 기존 모델이 쓰는 dataset과 같을 수 있어 유사도 검증을 통해 추가적으로 1599개의 데이터를 추가적으로 확보하였다.

데이터를 추가 확보한 것만으로도 정확도의 성능이 96%로 눈에 띄게 올라감을 보여주었다.

### 2) 가중치 부여 후 정규화 -> Wine Quality 2) Correlation

분류에 큰 영향을 끼치는 데이터에 가중치를 부여하면 classfication에 더 도움을 줄 수 있을까 하여 가중치를 부여하는 방향으로 데이터셋에 가중치를 곱하는 방향으로 학습을 진행하였다.

제일 먼저 생각한 요소는 '상관계수'였다. quality와 다른 특성들간의 상관계수를 구하여 그 상관계수를 단순히 데이터에 곱한 후 정규화를 진행하였다. 하지만, 정확도 0.04%정도로 미미한 상승을 이루었다.

상관계수는 -1과 1사이에서 값을 가지기 때문에 큰 영향을 주지 않았나는 추론에 상관계수에 10배의 값을 곱해주었더니 오히려 정확도가 83%정도로 떨어졌다. 

음수값들이 오히려 정확도를 떨어뜨릴 수 있다는 가정하에 상관계수의 절댓값을 곱한 값들로 학습을 진행하였지만, 정확도가 83%정도에 계속 머물렀다. 
그래서 (여기까지 수정)



### 3) 이진분류로 재라벨링 -> Wine Quality 3) Binary_Classification
