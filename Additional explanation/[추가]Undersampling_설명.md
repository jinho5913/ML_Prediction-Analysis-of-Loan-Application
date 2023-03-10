### Under Sampling

Loan 데이터의 경우 불균형이 매우 심하기 때문에 해당 불균형을 일정 수준 이상 해소하기 위해 Undersampling 과정을 거쳐야 하는 필요성이 있음 (모델 성능 비교하는 차트나 자료 넣으면 좋을듯)

Loan 데이터의 특성은 다음과 같다

- Loan 데이터 구성의 경우 유저가 대출을 조회한 하나의 신청서에 대해 여러 조회 결과가 나오며 그 상품 중 대출 신청하거나 모두 신청하지 않을 수 있음
- 모든 신청서가 동일한 대출 상품을 조회하는 것이 아니라 신청서 별 대출 조회 상품이 상이함
- 하나의 유저에서 발생하는 각 신청서마다 다른 대출 상품을 조회할 수 있음

따라서 랜덤하게 Undersampling을 진행하면 다음과 같은 문제가 발생할 수 있다.

- 한 유저의 0으로 Labelling 된 샘플 데이터는 모두 없어지지만, 다른 한 유저의 0으로 Labelling된 샘플 데이터는 모두 남아있을 수 있음
- 각 신청서의 대출 신청 여부는 유저의 정보에도 연관이 있기 때문에 유저의 정보와 추천된 대출 상품 정보 간의 연결된 정보가 랜덤하게 삭제되어 모델링 시 이러한 패턴을 파악할 수 없음

이러한 문제는 샘플링 시 데이터의 편향을 야기할 수 있으며 이러한 편향은 실제 모델의 과적합 발생에 영향을 줄 수 있으며 Robust한 모델 설계에 큰 걸림돌이 될 수 있다.

따라서 랜덤하게 Undersampling 하는 것이 아닌, 각 유저들의 데이터 수를 파악하여 유저들의 샘플 데이터 수를 고려하여 언더 샘플링을 진행하여야 한다는 필요성이 있어 다음과 같은 방법으로 Undersampling을 진행한다.

1. 각 유저마다 대출 조회를 한 신청서의 수가 다르기 때문에 우선적으로 각 유저 별 대출 조회 신청서의 수를 구한다
2. 이후 대출 조회를 한 신청서 중 0으로 Labelling 되어있는 데이터의 개수를 각 유저별로 파악한다.
3. 해당 유저의 0으로 labelling 된 신청서의 개수에 따라 5개 이상이면 85%, 2~4개면 50%, 1개이면 제거를 안하는 방식으로 모든 유저의 데이터 개수를 고려하여 언더샘플링 진행

해당 과정을 거쳐 나온 샘플 인덱스를 drop 하여 언더샘플링을 진행하였으며, 해당 과정을 통해 랜덤 언더샘플링을 통해 유저별 데이터 샘플의 쏠림 현상을 방지할 수 있음

결과적으로 undersampling을 통해  loan_result 에서 유저의 개인적 특성과 대출 신청 간의 연관성이 없어지는 문제를 최소화 할 수 있다.

