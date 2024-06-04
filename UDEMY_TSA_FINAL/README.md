# Python for Time Series Data Analysis - Jose Portilla, Pierian Training

## 목차

- [Section 10 - Prophet](#section-10---prophet)


# [Section 10 - Prophet](#목차)

`Prophet`은 페이스북의 시계열 예측 모델이다.

> Forecasting at Scale by Sean Taylor, Benjamin Letham
> Prophet 모델 논문

Prophet 예측 프로시저는 4가지 주요 컴포넌트를 가진 가법 회귀 모형이다.

일반화 가법 모델(Generalized Additive Models)

$$ y_i = \beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \cdots + \beta_p x_{ip} + \epsilon_i $$ 

-
-
-
-

1. piecewise linear (구분적 선형) 또는 logistic growth curve trend (로지스틱 성장 곡선)

프로시저가 데이터로부터 변경점을 선택하여 추세 변화를 자동으로 감지합니다.

2. Fourier series (푸리에 급수)를 이용한 연 단위의 계절성 컴포넌트
3. 더미 변수를 이용하는 주 단위 계절성 컴포넌트
4. 사용자가 제공하는 주요 공휴일 목록

Prophet 모델의 장점은 예측 결과를 만들기 위해 필요한 코드가 많지 않다는 점입니다.

## 실습

```py
import pandas as pd
# from fbprophet import Prophet # prophet v1.0 이전 이름
import prophet # python 3.7부터 사용
```

```
       date  beer
0  1/1/1992  1509
1  2/1/1992  1541
2  3/1/1992  1597
3  4/1/1992  1675
4  5/1/1992  1822
```

Prophet 예측 라이브러리가 작동하는 방식은 데이터셋의 열 부분이 
ds와 y로 분류되어 있어야 한다.

-> date 열이 ds가 되고, 예측하려는 데이터 레이블이 y이다.

