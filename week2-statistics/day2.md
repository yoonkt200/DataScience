# 2일차 


-----------------------


#### **1. 비정형 데이터 처리**

- R 패키지 참고 : http://r4pda.co.kr/

```

텍스트와 음성, 이미지는 비정형 데이터라고 할 수 있다. 최근 머신러닝 분야에서 가장 활발하게

연구 및 개발이 이루어지고 있는 것들이 바로 이 비정형 데이터라고 할 수 있다. 

비정형 데이터를 이용하여 인사이트를 도출하는 것이 데이터 분석 / 머신 러닝 분야의 가장 큰 화두인듯 하다.

```

> **1.1 텍스트 처리** : KoNLP를 이용

- 텍스트마이닝 전처리 과정

```

텍스트를 분석에 용이한 형태로 전처리 하기 위해서는, 가장 먼저 사전작업이 필요하다.

여기서 사전은 Dictionary를 의미한다. R Studio에서는 사전을 메모리상에 올린 뒤,

MergeUserDic(discrete 되었다.) 으로 사전을 구성한다. 

다음으로 텍스트를 pre-processing 해야하는데, 주로 소문자 변환, 유사단어 통일, 공백 제거 등의 과정이다.

```

```R

# string to lower
txt0 = str_to_lower(txt)

# word unite
txt1 = gsub("빅데이타", "빅데이터", txt0)
txt1 = gsub("bigdata", "빅데이터", txt1)
txt1 = gsub("big data", "빅데이터", txt1)
txt1 = gsub("[[:digit:]]", "", txt1)
txt1 = gsub("[[A-z]]", "", txt1)
txt1 = gsub("[[:punct:]]", "", txt1)
# txt1 = gsub("[a(\\d)+]", "", txt1) -> regular expression
txt1 = gsub("  ", " ", txt1)
txt2 = txt1[str_length(txt1)>1] # remove empty line

```

텍스트 전처리를 마쳤으면,

extractNoun (한글 형태소 분석의 경우)을 통해 간단한 텍스트 분석을 시행해보고

table을 이용해 결과를 확인해본다.

```R
txt_e = extractNoun(txt2)
txt_t = table(unlist(txt_e))
```

-----------------------


#### **2. 베이즈 정리**

```

베이즈 정리란, 두 확률변수의 사전확률과 사후확률의 관계를 나타내는 정리이다.

기본 아이디어는 기존의 가설에 현재의 자료를 반영해서 더 새로운 것을 만들어낸다는 아이디어로,

기존의 통계학의 패러다임과는 약간 다른 유형이었다.

베이즈 정리는 통계학적으로 비판적인 시각을 받고 있었으나, 심리학, 신경과학, 인공지능 등의 분야에서

인간의 정보처리방식과 유사하다는 점에서 계속하여 발전되어 왔었다.

최근에는 컴퓨팅 환경이 좋아지면서 머신 러닝에 대한 흐름이 가속화됨에 따라 베이즈주의적으로 해석하는 기법이 많이 발전되었다.

이제 수학적인 측면에서 살펴보자면,

기본적 용어로 다음의 용어들이 있다.

- 1. 사후 확률 : 관측자가 이미 알고 있는 사건으로부터 나온 확률로, 베이즈 정리에서는 P(A1), P(A2)... 을 의미함

- 2. 우도 : 이미 알고 있는 사건이 발생했다는 조건 하게 다른 사건이 발생할 확률.  P(B|A1), P(B|A2)...을 의미함

- 3. 사전 확률 : 사전확률과 우도를 통해서 알게되는 조건부 확률. P(Ak|B)를 의미함.

최종적으로 베이즈 정리의 의미를 생각해보자면, 사후 확률을 알고싶은데 직접적인 확률을 구할 변수가 없는 상황에서 

사전확률과 우도를 이용하여 사후확률을 구할 수 있다는 것이 베이즈 정리의 핵심이다. 

이때 기준 자체를 바꿔서 재정의 하는 것이 가능하다는 게 중요한 개념이기도 하다.

최종적으로 정리하자면, 이전의 경험과 현재의 증거를 토대로 어떤 사건의 확률을 추론하는 알고리즘이다.

```

-----------------------


#### **3. 각종 데이터 import 방법**

```R

data1 = read.table('clipboard', header = T) # for window
data1 = read.table(pipe("pbpaste"), header = T) # for mac

data2 = read.csv("data1.csv")

str(data2)
names(data2) = c("x1", "x2") # set column names

# install.packages("xlsx")
dyn.load("/Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home/jre/lib/server/libjvm.dylib")
library(rJava)
library(xlsx)

data3 = read.xlsx("data1.xlsx", sheetIndex = 1, header = T)

```

-----------------------



#### **4. 이미지 데이터 import 방법**

```R

dyn.load("/Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home/jre/lib/server/libjvm.dylib") # for mac
library(rJava)
install.packages("readbitmap") # even jpg, png possible
library(readbitmap)

bmp1 = read.bitmap("7.bmp")
str(bmp1)
dim(bmp1)

jpg1 = read.bitmap("7.jpg")
str(jpg1)
dim(jpg1)

png1 = read.bitmap("7.png") # png is 4dim for transparency
dim(png1)

bmp_m = matrix(bmp1, nrow=1, byrow = T)
jpg_m = matrix(jpg1, nrow=1, byrow = T)
png_m = matrix(png1, nrow=1, byrow = T)

```
