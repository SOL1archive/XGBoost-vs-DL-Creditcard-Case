# Paper Study: XGBoost vs Deep Learning
논문 [Tabular data: Deep learning is not all you need](https://www.sciencedirect.com/science/article/pii/S1566253521002360) 에서 기술된 대로 Tabular Data에서 Deep Learning이 일반적으로 좋은 성능을 내지 못하는 데 반해 XGBoost는 좋은 성능을 낸다고 밝힘. 이것이 신용카드 부정 사용 데이터의 경우에도 성립하는지 탐구함.

데이터셋은 [Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)을 사용함.

소스코드는 `xgboost-vs-dnn.ipynb`에서 확인할 수 있음.

XGBoost는 `GridSearch`를 통해 적절한 하이퍼파라미터를 구함. 딥러닝 모델의 경우 `tensorflow`를 통해 구현함. 과적합을 방지하기 위해 `Dropout` 기법을 적용하고 Batch Normalization 기법도 적용함. 테스트 지표로 봤을 때 과적합은 일어나지 않은 것으로 보임.

- Deep Learning Model Summary
```
_________________________________________________________________
 Layer (type)                Output Shape              Param #   
=================================================================
 dense_56 (Dense)            (None, 40)                1200      
                                                                 
 batch_normalization_46 (Bat  (None, 40)               160       
 chNormalization)                                                
                                                                 
 re_lu_46 (ReLU)             (None, 40)                0         
                                                                 
 dropout_36 (Dropout)        (None, 40)                0         
                                                                 
 dense_57 (Dense)            (None, 50)                2000      
                                                                 
 batch_normalization_47 (Bat  (None, 50)               200       
 chNormalization)                                                
                                                                 
 re_lu_47 (ReLU)             (None, 50)                0         
                                                                 
 dropout_37 (Dropout)        (None, 50)                0         
                                                                 
 dense_58 (Dense)            (None, 50)                2500      
                                                                 
 batch_normalization_48 (Bat  (None, 50)               200       
 chNormalization)                                                
                                                                 
 re_lu_48 (ReLU)             (None, 50)                0         
                                                                 
 dropout_38 (Dropout)        (None, 50)                0         
                                                                 
 dense_59 (Dense)            (None, 40)                2000      
                                                                 
 batch_normalization_49 (Bat  (None, 40)               160       
 chNormalization)                                                
                                                                 
 re_lu_49 (ReLU)             (None, 40)                0         
                                                                 
 dropout_39 (Dropout)        (None, 40)                0         
                                                                 
 dense_60 (Dense)            (None, 20)                800       
                                                                 
 batch_normalization_50 (Bat  (None, 20)               80        
 chNormalization)
                                                                 
 re_lu_50 (ReLU)             (None, 20)                0         
                                                                 
 dropout_40 (Dropout)        (None, 20)                0         
                                                                 
 dense_61 (Dense)            (None, 10)                200       
                                                                 
 batch_normalization_51 (Bat  (None, 10)               40        
 chNormalization)                                                
                                                                 
 re_lu_51 (ReLU)             (None, 10)                0         
                                                                 
 dense_62 (Dense)            (None, 2)                 22        
                                                                 
 softmax_10 (Softmax)        (None, 2)                 0         
                                                                 
=================================================================
Total params: 9,562
Trainable params: 9,142
Non-trainable params: 420
_________________________________________________________________
```

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
