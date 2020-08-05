# :hourglass_flowing_sand:모델링

> 데이터 전처리를 끝낸 dataset이 준비되었다면, 그 다음은 훈련시킬 모델을 정할 차례다. 얼굴 이미지 데이터를 활용하기에 Convolution Neural Network, 약칭 CNN 기반의 모델들을 시험했으며, 이러한 과정을 결과로 최종 모델을 선정하였다. 

![Example-CNN-architecture](https://user-images.githubusercontent.com/58945760/88549724-a1994800-d05b-11ea-9d49-73f884a88302.png)



 이하의 과정은 `django`을 통한 웹 서비스 개발, 데이터 전처리와 병행하여 진행되었으며, 모델링을 한 후에는 실제 웹페이지에서 `test`를 진행하였다.  



## 1. 전이학습(Transfer learning)

![1_1CxVzTNILTHgDs5yJO4W9A](https://user-images.githubusercontent.com/58945760/88550116-1ec4bd00-d05c-11ea-964f-6e868ef8f008.png)



**Deep Neural Network**와 **Convolution Neural Network**를 기반으로 한 모델링은 크게 두 가지로 나뉜다. 

 첫 번째는 Layer를 한 층 한 층 쌓아올려 자체적인 모델을 만드는 것이다. 보통 처음 모델링을 하고 개념을 이해할 때는 이 방법을 사용한다. 그러나 코드를 계속 돌려보며 하이퍼 파라미터를 조정하여야 하기에 최적을 모델을 찾는 데 시간이 오래 걸린다는 단점이 있다. 훈련할 데이터 양과 분류할 항목이 많아질 시 이 단점은 더욱 심화된다.  

 그렇기에 두 번째 방법으로 미리 훈련시켜놓은 모델을 불러와 사용하는 방법을 사용하는 경우가 많다. keras에는 이미 `imagenet`이라는 거대한 dataset으로 훈련시켜 놓은 많은 모델들이 존재한다. keras 내에서 `import` 하기만 하면 그 모델들을 자유롭게 사용할 수 있다.  

  

### 1.1 모델 후보 선정

> 공식 [keras API 문서](https://keras.io/api/applications/)에 존재하는 전이학습 모델들만 27개가 존재한다. 우리는 먼저 모델들의 성능을 비교할 수 있는 간단한 dataset을 만들어 시험해보기로 하였다. 

우선은 다른 Positive, Neutral에 해당하는 데이터를 각각 2,000장씩 모아 dataset을 구성하였다. 그리고 keras API에 들어 있는 모델을 모두 사용하여 데이터의 감정을 분류하는 실험을 진행했다. 결과적으로 0.76~1.00에 해당하는 정확도를 낼 수 있었다. 

우리는 그 중에서 가장 높은 정확도를 보인 모델은 `DenseNet`, `MoblieNet`, `Xception`이었다. 이 모델들을 대상으로 결과를 비교하여 분류 모델로 활용하기로 하였다. 



### 1.2  모델 시험하기

|   Model   | Accuracy | Loss |
| :-------: | :------: | :--: |
| DenseNet  |          |      |
| Xception  |          |      |
| MobileNet |          |      |
|   VGG16   |          |      |
|    ...    |          |      |



### 1.3 웹페이지 모델 적용, 개선하기

하지만 웹페이지에 모델을 적용시키는 데 문제가 발생하였다. `loading`에 40초~1분 이상의 긴 시간이 필요했던 것이다. 우리가 시험해본 모델들은 모두 CNN을 기반으로 하고 있었으며, 그에 따라 용량이 큰 편이었기에 자연스러운 일이라고 할 수 있었다. 하지만 웹 서비스 개발에 있어서는 반드시 개선해야 할 점이었다. 

다행히 `MobileNet`의 경우, `h5`파일의 용량이 다른 모델의 절반임에도 정확도에 있어 다른 후보 모델과 큰 차이를 보이지 않았기에 `loading` 시간을 절반 이상으로 줄일 수 있었다. 

default graph 내용 추가



#### 1.3.1 데이터 추가 전처리

![데이터 추가](https://user-images.githubusercontent.com/58945760/89427140-e026b500-d775-11ea-9a15-8f4246caa091.PNG)



### 1.4 다른 모델과의 비교 및 결론



## 2. 최종 CNN 모델





데이터의 한계를 느낌(전처리 링크 첨부)

최종 모델과 정확도, LOSS



