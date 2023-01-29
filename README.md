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
* df

