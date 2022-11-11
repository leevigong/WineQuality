# WineQuality_Classification

## Dataset
WineQT.csv는 기존 모델에서 사용하던 dataset이고, 데이터셋을 추가확보한 상태가 WineQT_add.csv이다.

WineQT_add.csv는 총 12개의 행으로 이루어져있으며, 행의 각 특성은 fixed acidity, volatile acidity, citric acid, residual sugar, chlorides, free sulfur dioxide, total sulfur dioxide, density, pH, sulphates, alcohol로 이루어져 있다.

WineQT.csv는 총 13개의 행으로 이루어져 있으며, WineQT_add.csv의 12개 특성에 Id가 추가된 상태였었고, 전처리과정에서 Id는 drop하였다.

WineQT.csv가 1143개 데이터, WineQT_add가 2742개 데이터로 이루어져 있다. 

## 정확도를 향상시킬 방안
###1) 학습데이터량의 확보 -> Wine Quality 1) Datasets_Increase

기존모델의 경우 데이터량이 1143개 밖에 되지않아 정확도가 87%정도 나오지 않았나 하는 가설에서 출발하였다. dataset확보를 위해 kaggle.comd에서 WineQuality에 관한 데이터를 더 찾아보았다. 혹여나 기존 모델이 쓰는 dataset과 같을 수 있어 유사도 검증을 통해 추가적으로 1599개의 데이터를 추가적으로 확보하였다.

데이터를 추가 확보한 것만으로도 정확도의 성능이 96%로 눈에 띄게 올라감을 보여주었다.

###2) 가중치 부여 후 정규화 -> Wine Quality 2) Correlation


###3) 이진분류로 재라벨링 -> Wine Quality 3) Binary_Classification
