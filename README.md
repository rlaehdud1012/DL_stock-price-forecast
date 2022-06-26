# DL_stock-price-forecast

1. Data

- yahoo finance
- 최근 10년 삼성전자 data
- High : 고가(가장 높은 가격으로 거래된 금액)
- Low : 저가(가장 낮은 가격으로 거래된 금액)
- Open : 시가(가장 처음 거래된 금액)
- Close : 종가(가장 마지막에 거래된 금액)
- Volume : 거래량
- Adj Close : 조정된 종가 금액

2. DATA 전처리 및 선택
- NULL 값 제거(Dropna 함수를 사용)
- Close(종가)를 예측하는 프로그램을 만들기 위해서 필요없는 Adj Close를 제거
- 종속변수(Y)를 Close로, 독립변수(x)는 High, Low, Open, Volume 

3. Data 정규화
- MinMaxScaler

4. Window Size 설정
- Window Size : 얼마동안(기간)의 주가 데이터에 기반하여 다음날 종가를 예측할 것인가를 정하는 Parameter
- Window Size = 50 으로 설정하여 50개 데이터를 통해서 다음 날 종가를 예측

5. LSTM 모델 구축하기
- LSTM : 장단기 메모리(Long Short-Term Memory;LSTM)이라고 불리며, RNN의 장기 의존성 문제 또는 현재 결과와 관련된 과거 정보를 기억하는 문제를 해결한다.
- 활성화 함수와 손실함수 설정
  * RELU : 대부분 일반적으로 사용되는 함수이며, 단순성 때문에 계산적으로 효율이 좋다
  * Softmax : Categorical_crossentropy 또는 mean_squared_error 손실함수에서 좋은 활성화 함수이다.
  * Sigmoid : Binary_crossentropy 손실 함수는 일반적으로 sigmoid 활성화 레이어 이후에 사용된다.
  * Tanh : Mean_squared_error는 tanh 출력에 대한 옵션이다.
  * Leaner : 항등함수이다.
  -> 변수 값이 전부 연속형 변수이기 때문에 MSE를 통해서 좋은 모델인지 확인할 수 있기 때문에 tanh를 활성화함수로 손실함수를 mse로 선택하였습니다.
- 정규화
 * Dropout : 일반적인 정규화 레이어이고, 다음 레이어에 참여하는 유닛의 일부를 랜덤하게 제거한다.

6. 결과 추출
- Layers : 128-128-128 / 256-256-256 / 512-512-512
- Regularizer : Dropout 0.2
- Optimizer : SGD / Adam / RMSprop
- Activation : Tanh
- Loss : MSE
- Train MSE와 Test MSE 값이 가장 작을 때의 모수를 최적화된 모수로 선정하였습니다.

7. 느낀점
- 노트북으로 진행했기에 시간이 너무 많이 걸렸고, 초기에 Keras 설정할 때 상당히 어려웠었다.
- 딥러닝을 처음 진행하는데, 모수에 대한 이해가 부족해서 높은 정확도를 추출하지 못해서 아쉬웠다.
