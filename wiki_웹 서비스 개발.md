#  :wrench:웹 서비스 개발

> 이 문서에서는 데이터 전처리 과정부터 병행해왔던 구체적인 웹 서비스 구현 과정에 대하여 다룬다. 기본적인 화면 구성부터 구체적인 기능 구현에 대해 설명을 포함한다. 



## 0. 준비 과정

![KakaoTalk_20200619_124911264](https://user-images.githubusercontent.com/58945760/85095315-f7dcc500-b22b-11ea-9b78-946b8fc8dd29.png)

backend는 `django`를 통해 웹 서비스를 구현하였고,  코딩에 사용한 주요 `tool`은 `Atom`입니다. 



## 1. 기본 화면 구성

- [화면계획서]()
- 웹 시나리오 

![웹 흐름도](https://user-images.githubusercontent.com/58945760/89790495-f7dab080-db5c-11ea-85c4-dd8bb362853c.PNG)



## 2. 웹캠 접근 및 구현

> 노트북의 웹캠에 접근하여 사용자의 얼굴을 받아들이도록 한다. 



## 3. 이미지 전송

> 웹캠으로 받아들인 이미지를 다음 페이지로 저장, 전송한다. 



## 4. 감정분류 모델 적용

> 미리 만들어둔 모델을 프로젝트 내에서 적용하여 결과를 출력한다. 



## 5. Youtube playlist 재생

> 모델의 감정 분류 결과에 따라 playlist가 재생되도록 한다.



## 6.1. 음악 추천 기능 구현

> 미리 만들어둔 음악 추천 알고리즘을 적용한다. 

![필터링](https://user-images.githubusercontent.com/58945760/89897022-5d8c7280-dc19-11ea-8c75-779970ee6cd6.PNG)

### 6.1.1. 음악 추천 알고리즘 

> 해당 서비스에 적용된 추천 알고리즘은 협업 필터링과 콘텐츠 기반 필터링이 혼합된 형태이며, 자세한 설명은 [링크](https://github.com/MLFYM/RECODUO/blob/master/technical_blog/04_%EC%B6%94%EC%B2%9C%EC%8B%9C%EC%8A%A4%ED%85%9C/Recommender_System_For_Music.md#recommender-system-for-music)에 자세히 설명되어 있다. 추천 시스템에 대한 기본적인 내용은 [이 링크](https://github.com/MLFYM/RECODUO/blob/master/technical_blog/04_%EC%B6%94%EC%B2%9C%EC%8B%9C%EC%8A%A4%ED%85%9C/RecommendationSystem.md#recommender-system)를 참조한다. 



### 6.1.2 추천 음악 링크 추출

> 웹페이지에서 재생되는 Youtube 영상 링크는 Google 웹 크롤링을 통해 추출한다.  

크롤링할 사이트로 Google을 선택한 이유는 노래 제목+아티스트명으로 검색하였을 때 공식 영상에 가까운 동영상을 최상단에 보여주기에, 보다 높은 품질의 영상을 사용자에게 제공할 수 있기 때문이다.  



## 6.2. 선택지 기능 구현

> 재생된 default playlist의 음악이 사용자의 마음에 들지 않을 경우, 보다 사용자의 취향에 맞춘 음악을 들려주기 위해 질문 & 답변 set를 제공한다. 해당 답변에 따라 맞춤 playlist를 추천해 준다.

 감정별로 세 가지 질문 & 4~5지선다형 답변 세트가 있으며, 해당 질문과 답변들은 자료를 참고하여 결정하였다. 



## 7. 음악 재추천 loop 구현

> 추천받은 음악이 마음에 들어 또 다른 음악을 추천받고 싶을 때, 계속적으로 추천을 받을 수 있도록 한다. 

