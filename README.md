# Paper Study: XGBoost vs Deep Learning
논문 [Tabular data: Deep learning is not all you need](https://www.sciencedirect.com/science/article/pii/S1566253521002360) 에서 기술된 대로 Tabular Data에서 Deep Learning이 일반적으로 좋은 성능을 내지 못하는 데 반해 XGBoost는 좋은 성능을 낸다고 밝힘. 이것이 신용카드 부정 사용 데이터의 경우에도 성립하는지 탐구함.

데이터셋은 [Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)을 사용함.

소스코드는 `xgboost-vs-dnn.ipynb`에서 확인할 수 있음.

XGBoost는 `GridSearch`를 통해 적절한 하이퍼파라미터를 구함. 딥러닝 모델의 경우 `tensorflow`를 통해 구현함. 과적합을 방지하기 위해 `Dropout` 기법을 적용하고 Batch Normalization 기법도 적용함. 테스트 지표로 봤을 때 과적합은 일어나지 않은 것으로 보임.

## Result

### Training Resources
#### Training Env.
- Common

||||
|-|-|-|
|OS|Ubuntu-Linux|20.04 LTS|
|Python Runtime|CPython|3.10.6|

- XGBoost

|||
|-|-|
|CPU|Ryzen 5 5600H|

- Deep Learning Model

|||
|-|-|
|CPU|Ryzen 5 5600H|
|GPU|RTX 3060 Laptop GPU|

#### Training Time

|||
|-|-|
|XGBoost|14.3s|
|DL|17s|

### Metrics

||XGBoost|Deep Learning|
|-|-:|-:|
|accuracy|0.9997|0.9984|
|recall|0.8309|0.9984|
|F1|0.8898|0.4996|

Accuracy의 경우 XGBoost가 딥러닝 모델보다 소폭 높으나 recall의 경우 딥러닝 모델의 성능이 압도적임. 신용카드 부정 사용의 경우 recall이 중요한 지표라고 볼 수 있으므로 딥러닝 모델의 성능이 좋음.

Reference)
- Shwartz-Ziv, Ravid, and Amitai Armon. "Tabular data: Deep learning is not all you need." _Information Fusion_ 81 (2022): 84-90.
