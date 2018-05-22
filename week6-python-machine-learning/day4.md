# 4일차 


-----------------------


#### **1. 차원 축소 기법**

피처 선택을 통해 데이터의 차원을 축소한 방법이 있었고,
이번에는 피처 추출을 통해 원래보다 낮은 차원의 새로운 부분공간으로 변환시켜 데이터를 요약하는
방법을 알아보겠다.

> **1.1 주성분 분석을 활용한 비지도적 차원 축소 기법**

```
여러 변수들의 변량을 주성분 분석(Principal Component)라고 불리는,
서로 상관성이 높은 여러 변수들의 선형조합으로 만든 새로운 변수들로 요약, 축약하는 기법.
비정규화된 모델에서 흔히 야기되는 일명 '차원의 저주' 문제를 해결하도록 도와주기도 한다.

우리는 회귀분석이나 의사결정트리등의 모델을 만들 때, 다중 공선성의 문제가 발생하는 것을 
쉽게 볼 수 있다. 이런 경우를 해결하는 것이 바로 상관도가 높은 변수들을 데이터를 대표하는 주성분 혹은
요인으로 축소하여 모형개발에 이용하는 것이다.

주성분 분석은 고차원 데이터에서 최대 분산의 방향을 찾아, 
새로운 부분 공간에 원래보다 작은 차원으로 투영하는 것인데, 
이 때 PCA는 데이터 각각에 대한 성분을 분석하는 것이 아니라, 
여러 데이터들이 모여 하나의 분포를 이룰 때 이 분포의 주 성분을 분석해 주는 방법이다.

여기서 주성분이라 함은 그 방향으로 데이터들의 분산이 가장 큰 방향벡터를 의미한다.

전체적인 과정은 다음과 같다.
d차원의 데이터간의 연관성을 찾기 위해 데이터를 먼저 표준화를 시킨다.
피처 상호간의 각각의 공분산을 구하기 위해 공분산 행렬을 만든다.
그리고 공분산행렬을 아이겐벨류(고유값)와 아이겐벡터(고유벡터)로 분해한다.
공분산행렬을 통해 그 두 가지(고유값, 벡터)를 유도하는 것이 가능한데, 이를 Eigendecomposition이라 한다.
고유값과 고유벡터의 쌍은 최대 d개가 나올 수 있다.

여기서 피처를 대표한다고 할 만큼의 큰 고유값과 그 쌍이 k개 존재한다면, 
데이터의 차원을 k개로 축소하는 것이다. 이 때, k개의 벡터는 새로운 데이터 차원의 basis가 된다.
```

>> 공분산이란
```
일반적인 분산은 모집단에서부터 추출한 표본 데이터들의 편차의 제곱의 산술적 평균을 의미하는 것,
즉 평균으로부터 퍼진 정도를 의미한다.

반면 확률론과 통계학에서, 공분산은 2개의 확률변수의 상관정도를 나타내는 값이다.
x와 y의 공분산은 x, y의 흩어진 정도가 얼마나 서로 상관관계를 가지고 흩어졌는지를 나타낸다.

만약 2개의 변수중 하나의 값이 상승하는 경향을 보일 때, 다른 값도 상승하는 경향의 상관관계에 있다면, 
공분산의 값은 양수가 될 것이다. 
반대로 2개의 변수중 하나의 값이 상승하는 경향을 보일 때, 다른 값이 하강하는 경향을 보인다면 
공분산의 값은 음수가 된다. 이렇게 공분산은 상관관계의 상승 혹은 하강하는 경향을 이해할 수 있으나 
2개 변수의 측정 단위의 크기에 따라 값이 달라지므로 상관분석을 통해 정도를 파악하기에는 부적절하다. 
이것을 보완하기 위해 상관계수라는 것을 사용하는데, 확률변수의 절대적 크기에 영향을 받지 않도록 하는 것.
```

![](https://raw.github.com/yoonkt200/DataScience/master/week6_PythonMachineLearning/week6_images/1.png)

>> 공분산 행렬

```
분산-공분산 행렬은 여러 변수와 관련된 분산과 공분산을 포함하는 정방형 행렬이다. 
(정방형 행렬은 행과 열의 개수가 동일한 행렬을 의미한다.)
행렬의 대각선 원소는 각 변수의 분산을 포함하며, 대각선 이외의 원소는 가능한 모든 변수 쌍 간의 공분산을 포함한다.
```

![](https://raw.github.com/yoonkt200/DataScience/master/week6_PythonMachineLearning/week6_images/2.png)

>> 고유값(eigenvalue)과 고유벡터(eigenvector)

```
행렬 A를 선형변환으로 봤을 때, 선형변환 A에 의한 변환 결과가 자기 자신의 상수배가 되는 0이 아닌 벡터를 
고유벡터(eigenvector)라 하고 이 상수배 값을 고유값(eigenvalue)라 한다.

자기 자신에 A라는 선형변환을 했을 때, 원래의 자기 자신의 고유한 특징(상수 λ 곱하기 자신은 자신)을
유지하는 벡터를 고유벡터라고 하는 것이다.

즉, nxn 정방행렬(고유값, 고유벡터는 정방행렬에 대해서만 정의된다) A에 대해 Av = λv를 만족하는 
0이 아닌 열벡터 v를 고유벡터, 상수 λ를 고유값이라 정의한다.

좀더 정확한 용어로는 λ는 '행렬 A의 고유값', v는 '행렬 A의 λ에 대한 고유벡터'이다.

- 출처 : http://darkpgmr.tistory.com/105

아래의 이미지가 이 내용에 대한 수식을 나타낸 것이다. A행렬은 공분산 행렬이 될 것이다.
더 정확히는, λ는 하나의 값이 아니라, λ1, λ2... λn 까지 구할 수 있다. 수식에서는
마치 λ가 하나인 것 처럼 보일 수 있지만, λ는 원래의 차원 개수만큼 생성된다.
v1, v2, ... vn 으로 되어있는 고유벡터 역시 (v1, v2, ...vn)의 묶음이 n개 생성되는 것이다.
```

![](https://raw.github.com/yoonkt200/DataScience/master/week6_PythonMachineLearning/week6_images/3.png)

```
PCA에 한정하여 고유값과 고유벡터를 살펴보면, 공분산 행렬 A를 알면 두 결과값을 얻을 수 있다는 것을 알수있다.

기하학적 의미를 아는 것 역시 중요하다.
고유값과 고유벡터의 기하학적 의미는, 고유벡터는 선형변환 A를 하여도 방향이 보존되며 크기만 변하는 벡터라는 것이고
고유값은 그 고유벡터의 변하는 크기를 나타내는 상수라고 할 수 있다.

이렇게 고유값 및 고유벡터에 대한 수학적인 내용이나 기하학적 의미를 대략적으로 파악하는 것도 꽤나 중요한 일이지만,
더 깊은 내용을 제대로 알기 위해서는 수학적인 내공이 필요한 것 같다.
```

>> 행렬의 mapping의 의미

```
행렬이란 선형변환이다. 선형 변환은 하나의 벡터 공간을 선형적으로 다른 벡터 공간으로 맵핑하는 기능이 있다.
선형대수학에서의 행렬을 이용한 rotation, shift, scale을 생각해보자. 
원래의 성질을 어느정도 유지하면서 새로운 선형 공간으로 벡터들이 이동하거나 변환하여 맵핑된다.
차원 축소는 바로 행렬의 이러한 성질 덕분에 가능한 것이다. 다음의 이미지들은 행렬에 의한 벡터 맵핑의 예시이다.
```

![](https://raw.github.com/yoonkt200/DataScience/master/week6_PythonMachineLearning/week6_images/4.png)

![](https://raw.github.com/yoonkt200/DataScience/master/week6_PythonMachineLearning/week6_images/5.png)

>> 다시 PCA

```
여기까지 정리가 되었다면 이제 공분산 행렬은 무엇인지, 고유벡터와 고유값의 의미가 무엇인지, 
왜 이런 친구들을 행렬로 구태여 사용하는 지 알 수 있다.
이제는 정리한 개념들을 통합해서, 데이터 축소에 도대체 어떻게 사용되는 건지를 정리할 차례다.

결국 PCA란 입력 데이터들의 관계를 보기 위해 만든 공분산 행렬을 분해한 두 가지 성분을 이용한 것이다.
그 두 가지 성분이란 고유벡터와 고유값인데, 고유벡터는 데이터의 분산이 큰 방향을 나타내는 벡터,
즉 원 데이터의 경향성의 방향 따위를 나타내는 개념이다. 고유값은 그 분산의 크기를 나타내는 것이다.
따라서 고유값이 클수록, 데이터의 경향을 강하게 대표한다고 할 수 있다. 그래서 고유값이 높을수록 좋은 것이다.

이는 다시 말하면 PCA도 퍼셉트론과 회귀분석에서와 마찬가지로, 데이터에서 의미있는 '선' 혹은 '축'을
찾는 과정이라고 할 수 있다. 그리고 그 각각의 축은 하나의 주성분을 대표한다.
기하학적으로는 각각의 고유벡터들은 서로 수직이다. 즉 새로운 basis를 만들어낸다고 생각할 수 있다.

데이터에는 차원의 숫자 만큼의 주성분이 달리게 되는데, PCA는 여기서 가장 중요한 주성분만을 분석하고
우선순위를 매기자는 것이다.

그렇다면 실제적으로 어떻게 데이터를 축소한다는 것인가?
feature selection의 경우, input feature 자체를 제외하는 것이지만 
PCA같은 feature extract는 다르다. 데이터 자체에 칼을 대는 것이 아니라,
특별한 변환 규칙을 통해 새로운 데이터를 생성하는 개념에 더 가깝다고 볼 수 있다.

다음과 같은 예를 들어보자.

① 빙판길 미끄러짐 사고 
② 수도관 동파 
③ 제설 차량 이용으로 인한 소비 금액 
④ 폭설로 인한 휴교 횟수 
⑤ 열사병 환자의 수

다음과 같은 5개의 차원의 데이터가 있다고 하자. 
하지만 데이터를 잘 살펴보면 모두 온도와 관계된 데이터라는 것을 알 수 있다. 
이 다섯개의 데이터는 아마 축소가 가능할 것이다.

만약 PCA를 통해서 한다면, 가장 강한 에이겐 벨류를 가지는 벡터를 통해 입력 데이터를 하나의 차원으로
변환시키는 과정을 거치는 것이다. 

d차원의 데이터가 있을 때, 가장 큰 k개의 고유값에 대한 k개의 벡터를 선택하고,
k개의 고유벡터로부터 투영행렬 W를 만든다. 이 W는 d차원의 입력데이터를 k차원의 새로운 피처 X로 변환시킨다.

이것이 PCA의 총체적인 개념이다. 구체적인 구현은 단순히 수학을 코딩으로 옮기는 문제이다.

얼마만큼의 차원으로까지 축소시키냐의 문제는, 
에이겐벨류의 최대값이 작아지는 순간까지 점차적으로 하는 방법 등을 생각해 볼 수 있겠지만, 
철저히 실전에서의 감각과 '해봄'에 의지하는 것 같다.
```

>> Python에서 PCA 구현하기

```
먼저 주성분을 추출하는 과정까지 진행해 본다. 과정은 다음과 같다.
- 먼저 와인데이터를 분리하여 전처리한 뒤, 피처간의 공분산 행렬을 구한다.
- 그리고 Numpy의 linalg.eig 함수를 이용하여 에이겐 벨류와 벡터를 추출한다.
- 추출한 주성분을 아이겐벨류의 설명 분산 비율을 통하여 확인한다.
```

```python
### data 불러오기
import pandas as pd

df_wine = pd.read_csv('https://archive.ics.uci.edu/ml/machine-learning-databases/wine/wine.data', header=None)

df_wine.columns = ['Class label', 'Alcohol', 'Malic acid', 'Ash', 
'Alcalinity of ash', 'Magnesium', 'Total phenols', 
'Flavanoids', 'Nonflavanoid phenols', 'Proanthocyanins', 
'Color intensity', 'Hue', 'OD280/OD315 of diluted wines', 'Proline']

df_wine.head()


### 데이터 전처리 - 데이터셋 분리
from sklearn.cross_validation import train_test_split

X, y = df_wine.iloc[:, 1:].values, df_wine.iloc[:, 0].values
	
X_train, X_test, y_train, y_test = \
        train_test_split(X, y, test_size=0.3, random_state=0)
        
        
### 데이터 전처리 - 데이터 표준화 작업
from sklearn.preprocessing import StandardScaler

sc = StandardScaler()
X_train_std = sc.fit_transform(X_train)
X_test_std = sc.transform(X_test)


### 공분산 행렬을 이용한 Eigendecomposition
import numpy as np

cov_mat = np.cov(X_train_std.T) # 공분산 행렬을 생성해주는 함수
# T는 Matrix의 T를 의미. 함수에 맞는 파라미터로 쓰기 위해 행렬을 돌려줌

eigen_vals, eigen_vecs = np.linalg.eig(cov_mat)

print('\nEigenvalues \n%s' % eigen_vals)


### 에이겐벨류의 설명 분산 비율
tot = sum(eigen_vals)
var_exp = [(i / tot) for i in sorted(eigen_vals, reverse=True)]
# 에이겐벨류 / 에이겐벨류의 합 을 각각 구한다. 나온 각각의 값은 아이겐벨류의 설명 분산 비율이다.
# 즉, 어떤 에이겐벨류가 가장 설명력이 높은지를 비율로 나타내기 위한 것이다.

cum_var_exp = np.cumsum(var_exp) # 누적 합을 계산해주는 함수. -> 누적 백분위로 표현


### 에이겐벨류의 영향력을 그래프로 시각화
import matplotlib.pyplot as plt
%matplotlib inline

plt.bar(range(1, 14), var_exp, alpha=0.5, align='center',
        label='individual explained variance')
plt.step(range(1, 14), cum_var_exp, where='mid',
         label='cumulative explained variance')
plt.ylabel('Explained variance ratio')
plt.xlabel('Principal components')
plt.legend(loc='best')
plt.tight_layout()
# plt.savefig('./figures/pca1.png', dpi=300)
plt.show()
```

```
다음으로 와인 데이터를 새로운 주성분 축으로 변환하는 과정, 즉 피처변환을 진행해본다.
```

```python
### 에이겐 쌍을 이용하여 투영행렬 생성
eigen_pairs = [(np.abs(eigen_vals[i]), eigen_vecs[:,i]) for i in range(len(eigen_vals))]
# 에이겐 쌍 생성 -> 투플 자료형

eigen_pairs.sort(reverse=True) # 내림차순으로 정렬

w = np.hstack((eigen_pairs[0][1][:, np.newaxis],
               eigen_pairs[1][1][:, np.newaxis]))
# 투영행렬 W : 변수를 2차원으로 축소시키는 투영행렬.
# eigen_pairs의 0,1 번째만 -> 2개의 에이겐 쌍으로만 차원축소를 하겠다는 것.
# hstack -> 행의 수가 같은 두 개 이상의 배열을 옆으로 연결하여, 열의 수가 늘어난 np배열을 만든다.
# 1차원 배열끼리는 hstack 되지 않으므로 [:, np.newaxis]을 추가함.

print('Matrix W:\n', w)


### 투영행렬로 피처 압축
X_train_std[0].dot(w) # X_train_std[0] 행렬과 W 행렬의 곱(내적연산)

X_train_pca = X_train_std.dot(w) # 피처를 투영행렬에 곱한 값 -> 피처 축소된 결과


### 변환된 데이터를 그래프로 시각화
colors = ['r', 'b', 'g']
markers = ['s', 'x', 'o']

for l, c, m in zip(np.unique(y_train), colors, markers):
    plt.scatter(X_train_pca[y_train==l, 0], 
                X_train_pca[y_train==l, 1], 
                c=c, label=l, marker=m)

plt.xlabel('PC 1')
plt.ylabel('PC 2')
plt.legend(loc='lower left')
plt.tight_layout()
# plt.savefig('./figures/pca2.png', dpi=300)
plt.show()
```

>> sklearn으로 주성분 분석

```
위에서 구현한 내용을, sklearn을 통하여 모듈로 간단하게 사용할 수 있다.
```

```python
from sklearn.decomposition import PCA

pca = PCA() 
# pca = PCA(n_components=2) 라고 하면, 2개의 에이겐 쌍만 쓴다는 것.
# n_components 는 none이 디폴트값.

X_train_pca = pca.fit_transform(X_train_std)
pca.explained_variance_ratio_ # pca객체의 기능으로, 에이젠벨류의 값을 소팅해서 보여줌.

from sklearn.linear_model import LogisticRegression

lr = LogisticRegression()
lr = lr.fit(X_train_pca, y_train) # 차원이 축소된 데이터를 로지스틱 회귀 모델로 학습
```

> **1.2 선형 판별 분석을 활용한 지도적 데이터 압축**

```
선형 판별 분석(Linear Discriminant Analysis, LDA)은 PCA와 마찬가지의 피처 압축 기법 중 하나이다.
전체적인 개념은 상당히 유사하지만, LDA는 PCA와 달리 최대분산의 수직을 찾는 것이 아니라
지도적 방식으로 데이터의 분포를 학습하여 분리를 최적화하는 피처 부분공간을 찾은 뒤, 
학습된 결정 경계에 따라 데이터를 분류하는 것이 목표이다.

즉, PCA가 데이터의 전체적인 분포를 참고하여 새로운 basis를 설정하고, 그 축에 맞게 데이터를
새롭게 projection 하는 것이 목표라면, LDA는 지도적인 방법으로 basis를 찾아서
그 축을 분리에 이용한 뒤, 최적의 분리를 완성한 뒤 projection을 하는 것이 목표이다.
지도적인 방법으로 basis를 찾는다는 것은, 통계적으로 지도적인 방법으로 두개의 이산행렬을 구한다는 것이다.
두개의 이산행렬에 대한 설명은 밑에서 설명할 것이다.

내용만 봐서는 LDA는 PCA의 업그레이드 버전으로 보인다. 게다가 지도학습!
당연하게도 일반적인 상황에서는 PCA보다 성능이 좋은 것으로 알려져 있다. (물론 PCA가 더 좋은 경우도 꽤 있단다.)

LDA가 잘 작동하기 위해서는 다음과 같은 조건들이 필요하다(반드시 필수는 아니다. 사실 다 성립하기는 불가능.)

1. 데이터가 정규 분포한다.
2. 각각의 분류들은 동일한 공분산 행렬을 갖는다.
3. 피처들은 통계적으로 상호 독립적이다.

그리고 전체적인 개념 및 과정을 한번 훑어보자면,

- 표준화된 d차원의 데이터가 있다.
- 각각의 레이블에 대한 d차원의 평균 벡터를 구한다
- 분류간 이산행렬과 분류 내 이산행렬을 만든다. 
(분류간은 두 범주의 평균이 멀도록, 분류내는 분산이 작도록 하는 이산행렬.)
- 이산행렬을 이용하여 아이겐벨류와 아이겐벡터를 구한다.
- 변환행렬을 구하여 차원축소를 진행한다.
```

![](https://raw.github.com/yoonkt200/DataScience/master/week6_PythonMachineLearning/week6_images/9.png)

```
위 그림을 보면, 왼쪽은 데이터를 변환행렬에 의해서 새롭게 1차원으로 투영했을 때, 부분적으로 겹치거나
오분류가 일어난 것을 볼 수 있다. 반면 오른쪽은 새롭게 1차원으로 투영했을 때, 잘 분류된 모습이다.
두 그래프의 차이는, 초록색 구분선으로 설명이 가능하다. 오른쪽의 경우는 두 분류(레이블)간의 mean의 차이가 크고
분류 내의 분산(선형적 의미 : 새로운 축으로 투영했을 때 분류의 x축 범위가 좁은것 과 넓은 것)이 작다.
왼쪽 그래프는 두 분류간의 평균은 커보이지만, 분산 역시 크기 때문에 투영이 잘 이루어졌다고 볼 수 없다.
분류내의 이산행렬을 구한다는 것은 레이블을 알고 있어야 가능한 것이기 때문에 LDA가 지도적 방식인 것이다.
PCA와 다른점은 바로 이렇게 지도적으로 분류간 이산행렬, 분류내 이산행렬을 구한다는 점이다. 

PCA의 경우는 변수간의 공분산 행렬을 이용하여 데이터를 대표하는 에이겐 쌍을 추출했다면
LDA의 기본적인 방법은 class들의 mean 값들의 차이는 최대화하는 행렬 A, 
class내의 variance는 최소화하는 행렬 B를 찾아내서 B의 역행렬 X A행렬에다가 eigendicomposition을 통해 
class 간의 mean은 최대화하고 class 내의 variance는 최소화하는 에이겐 쌍을 추출한다.
(사실 LDA에서의 B행렬은 공분산 행렬과 비슷한 것이다.)

조금 더 구체적인 설명과, 지도학습과 행렬들에 이용되는 수식은 다음을 참고하자.
https://ratsgo.github.io/machine%20learning/2017/03/21/LDA/
```

>> sklearn에 구현된 LDA

```
직접 LDA로 차원축소를 구현하는 과정은 PCA와 거의 유사(이산행렬 부분만 추가되어 구현하면 됨 : 
PCA에서 공분산 행렬을 구하는 것 까지의 단계를, 이산행렬들을 구하는 과정으로 대체하면 그 이후 구현은 동일.)
하기 때문에 생략하고, 모듈로 미리 구현된 LDA를 사용하는 코드를 실행해보자. 콘텐츠는 다음과 같다.
```

```python
# from sklearn.lda import LDA 가 Deprecation되었기 때문에 바꿔줌.
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis as LDA
lda = LDA(n_components=2) # 2개의 에이겐 쌍을 선택
X_train_lda = lda.fit_transform(X_train_std, y_train) # 축소된 훈련, 테스트 데이터 생성
X_test_lda = lda.fit_transform(X_test_std, y_test)

from sklearn.linear_model import LogisticRegression # 로지스틱 분류로 성능 테스트
lr = LogisticRegression()
lr = lr.fit(X_train_lda, y_train)

lr.predict_proba(X_test_lda[0,:]) #해당 분류에 속할 확률값으로 결과 도출
y_pred_lr=lr.predict(X_test_lda) #예측한 분류값을 보고싶을 때

from sklearn.metrics import accuracy_score
print('Accuracy: %.2f' % accuracy_score(y_test, y_pred_lr))
# 무려 100%의 정확도..
```

> **1.3 비선형 매핑을 위한 커널 주성분 분석의 사용**

```
회귀분석과 대부분의 분류 알고리즘에서는 데이터를 선형분리 가능하다는 가정이 필요했다.
심지어 인공신경망의 기초격인 퍼셉트론에서조차 선형분리 가능을 전제로 알고리즘이 동작했다.
이러한 문제점들을 PCA, LDA같은 차원 축소 기법으로 해결했으나
데이터의 모양이 정말로, 완전히, 앱솔루틀리 하게 비선형인 경우는 문제가 달라진다.

PCA, LDA 같은 알고리즘은 차원축소를 위한 선형 변환 기법을 이용하기 때문에,
선형으로 분리 불가능한 데이터에 대해서는 적당하지 않다. 

이런 문제를 극복하기 위해 커널 PCA를 사용할 수 있다.

SVM에서의 커널 기법을 떠올려보자. 원래의 d차원 데이터를 k차원으로 (더 큰 차원으로)
매핑하는 하나의 함수를 생각할 수 있다. 이 때, 커널을 활용하여 데이터를 고차원으로 변환하는
비선형 매핑을 수행한 뒤, 일반적인 PCA를 통해 데이터들이 선형 분리가 가능한 저차원 공간으로
다시 투영하는 아이디어를 생각해보자. 이 아이디어가 커널 PCA의 기본적인 생각이다.

하지만 이런 방법은 굉장히 비효율적이다. 

이 문제를 효율적으로 해결하기에 앞서 잠시 앞으로 돌아가 볼 필요가 있다.
우리는 앞서 PCA에서 피처간의 관계를 공분산 행렬로 표현하였다. 
공분산은 피처간의 내적을 통해 표현이 되기도 한다. 
즉, 두 피처간의 벡터의 내적이란 두 데이터의 유사도를 의미하기도 한다는 것이다.

그렇다면 두 벡터 사이를 내적하는 부분의 함수를, 데이터를 고차원으로 mapping하는 커널 함수로
대체하는 것은 어떨까? 아마도 두 데이터의 상관관계를 우리가 정한 kernel function으로써 
나타내는 것이 가능해질 것이고, 유사도라는 개념을 더욱 범용적이고 고차원적인 방법으로 사용이 가능해진다.


벡터의 내적을 이용하여 상관관계를 구하게 되면, 그 관계의 모양은 linear한 선형적 의미를 가진다.
하지만 커널을 사용한다면, 그 커널과 맞는 선형적 의미를 가지게 된다. 당연히 가우시안 커널을 사용한다면
방사형의 관계를 가지게 될 것이다.

다시 kernel PCA로 돌아와보자. PCA는 주어진 데이터셋을 linear 벡터 형식의 주성분 분석을 통해
새로운 basis에 projection 시키는 과정이라고 할 수 있다. 
하지만 만약 여기서 데이터의 주성분 분석이 kernel의 형태라면, 
기존의 linear projection이 nonlinear한 projection으로 바뀌게 될 것이다.
그 결과, 우리가 분류하고자 하는 데이터셋은 커널의 성질을 띤 채로 non-linear하게 구분이 된다.

```

>> python에 구현되어있는 kernel PCA

```python
from sklearn.decomposition import KernelPCA

X, y = make_moons(n_samples=100, random_state=123)
scikit_kpca = KernelPCA(n_components=2, kernel='rbf', gamma=15)
X_skernpca = scikit_kpca.fit_transform(X)

plt.scatter(X_skernpca[y==0, 0], X_skernpca[y==0, 1], 
            color='red', marker='^', alpha=0.5)
plt.scatter(X_skernpca[y==1, 0], X_skernpca[y==1, 1], 
            color='blue', marker='o', alpha=0.5)

plt.xlabel('PC1')
plt.ylabel('PC2')
plt.tight_layout()
# plt.savefig('./figures/scikit_kpca.png', dpi=300)
plt.show()
```

-----------------------


#### **2. 모델 평가**

```
머신러닝 모델을 학습하는 데 있어서 중요한 점 중 하나는, 새로운 데이터셋에 대한 반응하는 모델의 성능을 추정하는 것이다.
만약 새로운 데이터셋이 들어왔을 때 학습된 모델이 얼마나 예측이나 분류를 잘 수행하는지에 대한 예상이 필요하다.
우리가 학습한 모델이 새로운 데이터에 대한 결과의 예상이라면 우리는 그 모델이 얼마나 잘 예상할지에 대한 예상이 필요하다.

정확한 용어로 얘기하자면, 모델의 일반화 오차에 대해 신뢰할만한 추정치를 구할 수 있게 해주는 방법이 필요하다는 것이다.

그 방법으로는 일반적으로 크게 두가지, 홀드아웃(holdout) 교차검증과 k-fold 교차검증의 방법이 있다.
```

> **2.1 홀드아웃 교차검증 방법**

```
가장 보편적인 모델의 성능 테스트 방법은, 원 데이터를 훈련데이터와 테스트데이터 두개로 나누는 것이다.
훈련데이터로 모델을 학습하고, 테스트 데이터로 모델의 성능을 증가시키는 선택을 반복하게 된다.
하지만 모델을 선택하는 동안 동일한 테스트 데이터를 계속 재사용한다면, 이 테스트 데이터는 테스트데이터로써의
효용가치가 떨어지고, 훈련데이터화 될 것이다. 결국 데이터는 오버피팅 된다.

하지만 홀드아웃 메서드를 사용하면 데이터를 세 부분으로 나누게 된다.
처음의 모델 학습에서 분리된 훈련 데이터와 테스트 데이터, 즉 ((훈련데이터, 검증데이터), 테스트데이터) 세 개로 나뉜다.
여기서의 훈련 데이터는 말 그대로 훈련 데이터이고, 검증 데이터에 대한 성능을 높이는 작업을 학습에서 진행한다.
그리고 테스트 데이터를 이용하여 최종 성능을 추정하게 된다.

홀드아웃 교차검증의 단점은, 데이터를 위와 같이 나눈 방식 자체가 성능 추정에 민감한 영향을 미친다는 것이다.
만약 데이터셋 전체가 개수가 크지 않다면, 이러한 분할은 치명적일 수 있다.
즉 홀드아웃 셋을 만들어 내는 것 자체에 대단한 신경을 써야한다는 것이다.
```

> **2.2 k-fold 교차검증 방법**

```
k-fold 교차검증은 조금 더 강인한 성능추정 기법이다.
분류기 성능 측정의 통계적 신뢰도를 높이기 위해서, resampling 방법을 사용한다.

먼저 데이터를 k개의 데이터로 등분한다. 분리된 k개의 subset중에 k-1개를 훈련 데이터로 사용하고
(샘플링의 방법은 simple random, systematic, stratified, First N, cluster등이 있음.)
1개의 subset을 테스트 데이터로 사용한다. 여기서 비복원 추출의 개념으로, 한번 테스트로 선택된 subset 데이터는
다시 선택되지 않는다. 물론 k-fold와 홀드아웃 교차검증을 섞어서 사용할 수도 있다.
그리고 당연하게도, k등분 된 k-fold 검정에서의 iterate 횟수는 k번이다. (비복원으로 모든 경우의 수를 하는 갯수)

k-fold의 장점은 모든 데이터를 training과 test에 쓸 수 있다는 점이다. 또한 오버피팅의 염려도 크지 않다.
하지만 시간이 다소 오래걸린다는 단점이 존재한다.
k=n 으로 설정하여 1개의 샘플을 테스트셋으로 두어 샘플의 숫자만큼 반복측정을 하는,
leave-one-out(혹은 jackknife 기법)기법과 같은 극단적인 방법으로 실행할 때는 더더욱 그렇다.

보통 k-fold는 일반화 성능을 만족시키는 최적의 하이퍼 파라미터를 구하기 위한 모델 튜닝에 사용된다는 것이 가장 중요하다.

위에서 잠시 언급한 층화 추출(stratified) 등으로 k-fold를 샘플링하게 되면 이 알고리즘은 조금 더 개선이 가능하다.
그것을 층화 k-fold 교차검증(Stratified K-fold Cross Validation)이라고 한다.
```

![](https://raw.github.com/yoonkt200/DataScience/master/week6_PythonMachineLearning/week6_images/14.png)

>> k-fold 교차검증을 파이썬에서 사용하기

```python
from sklearn.cross_validation import cross_val_score

scores = cross_val_score(estimator=pipe_lr, 
                         X=X_train, 
                         y=y_train, 
                         cv=10,
                         n_jobs=1)
print('CV accuracy scores: %s' % scores)
print('CV accuracy: %.3f +/- %.3f' % (np.mean(scores), np.std(scores)))
```


-----------------------


#### **3. 학습, 검증곡선과 편향-분산 트레이드오프**

>> 편향-분산 트레이드오프 (Bias-Variance Tradeoff)

![](https://raw.github.com/yoonkt200/DataScience/master/week6_PythonMachineLearning/week6_images/16.png)

```
머신 러닝에서의 error는 크게 두 분류로 나뉜다.
bias(편향), 그리고 variance(분산)이다.

bias는 흔히 생각할 수 있는 error로, 선형 회귀같은 문제에서의 SSE를 떠올리면 쉽다.
모델이 학습데이터를 충분히 설명할 수 없는 상황에서 커지는 에러이다. 
이 상황을 흔히 underfitting이라고 한다.

variance는 그 반대로 모델이 학습데이터를 과도하게 잘 설명하는 상황이다.
모집단을 추정하고자 표본집단을 이용하여 모델을 만들어놨더니, 표본집단만을 거창하게 잘 설명하는 모델이 된 것이다.
머신러닝을 공부하는 사람이라면 한 번 쯤 들어본, overfitting의 상황이다.

variance에 대해 수학적으로 조금 더 직관적으로 얘기하자면, 
Training Score와 Cross Validation의 차이가 심해지는 상황이 variance가 증가하는 상황이다.
아래의 그림을 보면 매우 쉽게 알 수 있다. 
빨간 곡선은 cross validation error이고, training error가 녹색 곡선이다.
학습이 진행됨에 따라 오버피팅이 되기 때문에 트레이닝 스코어는 계속해서 증가하는 경향을 보이지만,
교차검증값은 점점 악화된다. 모델이 일반화 성능을 잘 보여주는 영역에서 벗어나고 있는 상황이다.
(참고 - 트레이닝 스코어 : 학습데이터로 모델을 테스트했을때의 스코어, 
교차검증 스코어 : 모델의 일반적 성능을 추정하기 위해, 테스트셋을 resampling 하는 등의 모델 일반화 검증을 하는 방법에 대한 스코어)
```

![](https://raw.github.com/yoonkt200/DataScience/master/week6_PythonMachineLearning/week6_images/15.png)

```
일반적인 머신러닝에서는 편향-분산의 관계는 편향이 올라가면 분산은 내려가고, 
분산이 올라가면 편향이 내려가는 시소 관계에 놓여있다. 이를 편향-분산 트레이드오프라 한다.

흔히 머신러닝에 있어서 중요한 것으로, 비용함수를 최적화 하거나 차원을 축소한다거나 하는 이야기를 하기 쉽다.
하지만 편향-분산 트레이드오프를 잘 맞춰주는 것이 훨씬, 머신러닝의 정말 기본중의 기본이라고 할 수 있겠다.

편향-분산 트레이드오프를 잘 맞춰주기 위해서는 그리드검색등을 이용한 파라미터 튜닝의 좋은 기법등이 있을 수 있겠으나,
역시 기본이 되면서 사람에게 설득력을 갖는 것은 눈으로 보여지는 것이다.
학습곡선과 검증곡선을 이용하여 바이어스와 분산 문제를 진단하는 것이 여전히 좋은 방법이다.
sklearn에서는 learning-curve를 아주 쉽게 그려주는 모듈을 제공한다.

이것을 이용하는 것이 전자보다 더 의미가 있다.
그리드 검색의 하이퍼 파라미터 튜닝, 중첩 교차검증 등의 고급 기법은 학습곡선과 검증곡선을 토대로,
이 문제를 사람의 직관으로 판단하는 요인을 코드로 구현한 것에 지나지 않기 때문이다.

아래의 예제는 학습곡선과 검증곡선으로 편향-분산 트레이드 오프 상황을 핸들링하는 상황을 재현한 것이다.

더욱 고급기법의 경우는 오히려 코드로는 훨씬 쉽다.
GridSearchCV등의 클래스에 매우 직관적이면서 쉽게 정리가 되어있기 때문에 sklearn의 튜토리얼을 
한 번 쯤 따라해보는 것만으로도 충분하다.
```

```python
%matplotlib inline
import matplotlib.pyplot as plt
from sklearn.learning_curve import learning_curve

pipe_lr = Pipeline([('scl', StandardScaler()),
            ('clf', LogisticRegression(penalty='l2', random_state=0))])

train_sizes, train_scores, test_scores =\
                learning_curve(estimator=pipe_lr, 
                X=X_train, 
                y=y_train, 
                train_sizes=np.linspace(0.1, 1.0, 10), 
                cv=10,
                n_jobs=1)

train_mean = np.mean(train_scores, axis=1)
train_std = np.std(train_scores, axis=1)
test_mean = np.mean(test_scores, axis=1)
test_std = np.std(test_scores, axis=1)

plt.plot(train_sizes, train_mean, 
         color='blue', marker='o', 
         markersize=5, label='training accuracy')

plt.fill_between(train_sizes, 
                 train_mean + train_std,
                 train_mean - train_std, 
                 alpha=0.15, color='blue')

plt.plot(train_sizes, test_mean, 
         color='green', linestyle='--', 
         marker='s', markersize=5, 
         label='validation accuracy')

plt.fill_between(train_sizes, 
                 test_mean + test_std,
                 test_mean - test_std, 
                 alpha=0.15, color='green')

plt.grid()
plt.xlabel('Number of training samples')
plt.ylabel('Accuracy')
plt.legend(loc='lower right')
plt.ylim([0.8, 1.0])
plt.tight_layout()
# plt.savefig('./figures/learning_curve.png', dpi=300)
plt.show()
```

![](https://raw.github.com/yoonkt200/DataScience/master/week6_PythonMachineLearning/week6_images/17.png)