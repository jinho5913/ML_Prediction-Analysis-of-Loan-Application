# BigContest Competition

### 앱 사용성 데이터를 통한 대출신청 예측분석  
#### < 1. Data Preprocessing & Feature Engineering >
* Data Preprocessing
  * 이상치 처리, Data Leakage가 발생하지 않도록 전처리 진행  
* Feature Engineering
  * user별 파생변수 생성
    * 유저 타입 등

  * item별 파생변수 생성  
    * 상품매력도, 상품코드 등

  * log 데이터로 파생변수 생성
    * 시간 순으로 정렬된 sequence data이기 때문에 시계열 정보가 담긴 feature 생성
    * `GRU`를 사용하여 대출 조회(target)까지 도달한 log인지 판단하는 __이진분류 모델 생성__ (정확도 : 92.89%)
    * Linear layer를 추가하여 각 시퀀스당 10차원의 embedding vector 추출 -> feature로 사용

  * 그 외
    * 연이자부담지수, 증감율 등

#### < 2. Modeling >
* DNN, RandomForest, LGBM, CatBoost 모델 사용하여 예측 모델 개발
* 분류된 예측값을 기준으로 K-Means로 고객 군집화 진행

#### < 3. EDA >
* 분류된 군집별로 각각 EDA 진행

< 예시 >

<img width="613" alt="image" src="https://user-images.githubusercontent.com/87609200/215314811-11c3bbfa-cc52-406e-9bbb-399d91f226eb.png">

<img width="1087" alt="image" src="https://user-images.githubusercontent.com/87609200/215314829-55284ebb-a82b-4e30-af02-561f36b7cafe.png">


