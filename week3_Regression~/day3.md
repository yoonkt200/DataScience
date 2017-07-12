# 3일차 


-----------------------


#### **1. 분류 알고리즘**


> **1.1 K-NN**

```
- 최근접 이웃을 찾아가는 분류 알고리즘.

- K는 최근접 이웃의 갯수를 말하는 것.

- 지도학습의 일종으로 레이블이 있는 데이터를 사용함.

- 예를 들어 K가 1이면, iterate 할 때, 그 데이터와 가장 가까운 Class를 자신의 Class로 하게 됨.\

- 2이면, 자신과 가장 가까운 2개의 데이터의 클래스를 참조하여 자신의 클래스를 결정

- 이웃을 찾을때는 여러가지 거리 측정 방법 중에 주로 유클리디안 거리를 사용함.

- feature들이 numerical할 때, 데이터를 표준화시켜주는 것이 좋음.

```

> **1.2 K-means**

```
- 주어진 데이터를 K개의 클러스터로 묶는 알고리즘.

- 비지도학습의 일종으로 레이블이 없는 데이터를 사용함.

- 데이터들의 각 클러스터와의 거리차이의 분산을 최소화하는 방식으로 iterating 한다.

- 알고리즘의 대략적인 방법은 다음과 같다.

##################################################################
1. 초기에 K개를 선택하여 각각이 cluster가 된다.

2. 모든 데이터들은 가장 가까운 클러스터에 할당함.

3. 거리 판단 기준 : (클러스터의 중심과의 거리 / 외곽과의 거리 / 반대 외곽과의 거리)등이 있음.

4. 클러스터에 데이터가 모두 편입되면 cluster의 중심을 재설정하고, 

5. 다시 모든 데이터를 새로 설정된 K개의 중심에 맞게 할당함. 이 작업을 반복.
##################################################################

- iterating할 때, 클러스터 중심이 재조정되는 과정에서 더이상 변화가 없다면 중지하게 된다.

- 프로그래머는 초기의 중심 갯수를 설정해야 하고, 어떤 데이터가 선택될지는 일반적으로 랜덤하다.

- k값을 실제 클러스터링의 개수와 비슷하게 설정해줘야 한다.

- 이상값에 굉장히 민감하고, 기초적인 알고리즘이기 때문에 문제점이 많다.

##################################################################
1. 초기 클러스터 지점과 수를 잘 설정해야 한다.

2. 이상값을 처리해야 한다.

3. 지역 최적값 때문에 이상한 수렴조건에 빠져 더이상 클러스터링을 진행하지 않을 수도 있다. 

-> initialization이 매우 중요

4. 데이터의 분포 모양이 구형이 아니다.
##################################################################

 - 등의 문제점들을 해결해야 한다.

 - K-means 아이디어에 기반한 많은 변형, 응용 알고리즘을 사용해야 각각의 문제점이 해결된다.
```

> **1.3 K-NN vs K-means**

```
분류(Classiication) - 이미 레이블이 있는 데이터를 기반으로, 새로운 데이터를 분류하는 것.

군집화(Clustering) - 레이블이 없는 데이터를 비슷한 군집으로 묶는 것.

- K-NN은 분류에 가까운 알고리즘이고, K-means는 군집화에 가까운 알고리즘이다.

- 가장 큰 차이는 레이블의 유무이다.
```

-----------------------


#### **2. 집단간 차이검정**

> **2.1 데이터 분석에서 사용하게 되는 가설, 통계량에 대한 기본 용어와 이론**
