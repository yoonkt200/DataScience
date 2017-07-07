# 4일차 


#### **1. 독립, 연관성 검정**

> **1.1 카이제곱 검정**

```

- 관찰된 빈도가 기대되는 빈도와 다른지의 여부를 검증하는 방법.

- z, t검정은 평균값에 대한 가설 검정에 사용되는 반면, 카이제곱은 확률에 대한 가설 검정이다.

- 카이제곱은 표본이 적거나, 오버피팅 되어있다면 검정결과가 매우 부정확할 수 있다.

- 이 경우 주로 fisher test를 사용함.

```

-----------------------


# 5일차 


#### **1. 분산분석**

> **1.1 집단 차이 검증**

```
집단간의 평균 차이를 검증하는 방법으로 t-검정이 있다. t-검정은 주로 두 집단을 비교할 때 사용한다. 물론 여러 집단간의 차이 검정에도 t-test가 쓰일 수는 있지만, 1종 오류가 커진다는 문제가 발생한다. 세 집단 이상 평균 비교에 대한 오류의 증가 관계는 다소 어려운 내용이므로, 데이터 분석만을 위해서는 알 필요는 없다.

어찌되었든 이러한 여러 집단간의 차이검증을 t-test로 하는 것에 의한 문제점을 해결하기 위해 해야되는 것이 분산분석이다. 

분산분석은 회귀분석의 한 형태라고 할 수 있는데, 집단 간 분산을 비교과정에 이용하는 것이 핵심 아이디어이다. 집단 간 분산이란, 각 케이스의 관찰값과 전체 평균 간 차이인 편차를 제곱하여 합산한 뒤, 각 케이스의 자유도로 나누게 되면(표본크기)분산의 비를 알 수 있다는 것이다. 이러한 분산의 비를 이용해서 집단간의 차이가 있는지 아닌지를 판단하는 게 분산분석의 핵심이다.

간단히 말해서, 각 집단의 평균치가 전체 평균으로부터 얼마나 이탈해있는지를 집단 간 분산을 통해 나타내는 것이다.
```