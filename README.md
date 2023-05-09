# time-series-da

Data Analysis for Time Series Analysis

- [ ] LSTM
- [ ] CNN
- [ ] Prophet
- [ ] GRU
- [ ] CNN + LSTM

## Historical 데이터분석 + RealTime 데이터분석

> 기존 데이터를 불러와 분석결과를 표시하는 것과 실시간 데이터를 불러와 분석하는 방법 제시.

이를 구현하기 위해, 코인 별(위 경우, 비트코인)로 오로지 하나의 data만을 가지고 있는 것이 좋다. 데이터가 추가되는 경우 `append`한다.

## Conv1D

### loss and val_loss

- loss: training data에 대한 오차
- val_loss: validation data에 대한 오차

모델 학습이 잘 이루어졌다면, loss와 val*loss가 모두 낮아지는 경향을 보인다. 그러나 모델이 overfitting 되었다면 loss는 계속 감소하지만 val_loss는 증가할 수도 있다. 이는 모델이 training data에만 과적합되어 \_unseen*데이터에 대한 일반화 성능이 떨어질 가능성이 크기 때문에, 모델 구조나 학습 방법을 조정해야 한다.

![overfitting.png](./assets/overfitting.png)

이와 같은 과적합은 모델을 구성하면서 학습데이터에 대해 과도하게 최적화되어 있어 다른 데이터에 대한 일반화 성능이 떨어지기 때문이다.

### Optimizer

1. `adam`
2. `RMSprop`(Root Mean Sqaure Propagation)

## Issues

- [ ] API
      CNN-LSTM(kaggle버전)에서 사용하는 poloniex의 api는 `{period}` key(GET)로 불러올 수 있는 기간을 제한하고 있다. 더불어, 유일하게 제공하는 시계열 값인 timestamp가 unix timestamp이다.

이를 해결하기 위해 bitstamp에서 제공하는 1시간 단위의 dataset(`.csv`)을 이용한다.

단, 여전히 api로 실시간 데이터를 불러와 json을 csv로 저장하거나, 기존 데이터에 append할 수 있도록 준비하는 것은 중요하다.

- [ ] unix timestamps

  - 장점: 데이터 타입을 string이 아닌 long으로 받을 수 있다.
  - 단점: 인코딩 과정 필요(pd.to_datetime(..., unit='s')를 사용할 수 없는 경우 format으로 해결해야 한다.)

- [ ] Dataset
      data의 인덱스를 아래와 같이 고정.

| Key       | Desc.      |
| :-------- | :--------- |
| timestamp | 날짜(시간) |
| open      | 시가       |
| close     | 종가       |
| high      | 고가       |
| low       | 저가       |
| vol       | 볼륨       |
