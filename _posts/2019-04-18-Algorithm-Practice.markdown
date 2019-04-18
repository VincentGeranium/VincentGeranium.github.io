---
layout: post
title:  "Algorithm Practice - 190418"
date:   2019-04-18
categories: Algorithm
---

# 190418-Algorithm-Practice

---

### 프로그래머스 알고리즘 연습

### 두 정수 사이의 합

---

![190418-Algorithm-Practice-img](https://user-images.githubusercontent.com/42841888/56364599-e4019180-6229-11e9-98f5-b90314644709.png)

---

## 나의 풀이 설명

처음에 각각의 가장 큰 값과 가장 작은 값을 구분하여 따로 maxValue와 minValue로 나누어 저장해야겠다는 생각에 if 문으로 maxValue와 minValue로 나눌수 있는 조건을 써서 나누어 변수에 저장 할 수 있도록 했다.

그 이후에 작은 값(minValue)부터 큰 값(maxValue) 까지의 숫자를 더해줘야 하니
반복문을 써야겠다는 생각에 for문을 만들자는 생각을 했다.

그리고 나서 for문을 몇번 돌릴지를 생각해야 하는데, 
예를들어 minValue가 3, maxValue가 5 이면 3+4+5 = 12 
즉, 3 ~ 5 까지 3번을 돌려야 했고
minValue가 3, maxValue가 7 이면 3+4+5+6+7 = 25
즉, 3 ~ 7 까지 5번을 돌려야 했다

그런데 위와 같은 관점으로 보면 생각이 더 꼬였다.

그래서 아에 쉽게 생각하자는 생각에 고민을 하니 그냥 minValue ~ maxValue를
for ~ in ~에서 in 뒤에 넣어주면 되겠네? 라는 생각이 들었다

그리고 또 중요한 점이 있는데 1부터 더하는것이 아니고 받아온 파라미터 값 중 작은 값(minValue) 부터 큰 값(maxValue) 을 차례로 더해야 한다는 점도 있어서

다음과 같이 for 문을 만들었다.

```
for i in (minValue...maxValue)
```

그리고 나서 따로 임시 저장소(temp)를 만들어 그 안에 for 문을 돌면서 minValue 부터 maxValue 사이의 숫자를 계속 더해주는 식인

```
temp += i
```

를 만들었다

위의 코드는 예를들어 minValue가 3 maxValue가 5이면 for 문이 minValue와 maxValue 사이의 범위만큼 돌면서 i에 3,4,5가 각각 들어간다

그래서 

첫 Loop에서는 temp가 0이므로, temp = 0 + 3, 그래서 temp에는 3이 저장되고 다음 Loop로 넘어가게 되고

두 번째 Loop에서는 temp가 3이므로, temp = 3 + 4, 그래서 temp에는 7이 저장되고 다음 Loop로 넘어가게 되고

마지막 Loop에서는 temp가 7이므로, temp = 7 + 5, 그래서 temp에는 12가 저장이 되고

임시 저장소(temp)에 저장된 마지막 결과값인 12를 answer에 저장하여 최종적으로

return answer 로 반환해준다

오늘은 여기까지~
