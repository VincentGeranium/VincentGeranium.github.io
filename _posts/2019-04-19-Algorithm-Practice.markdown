---
layout: post
title:  "Algorithm Practice - 190419"
date:   2019-04-19
categories: Algorithm
---

# 190419-Algorithm-Practice

---

## 프로그래머스 알고리즘 연습

## 문자열 내 p와 y의 개수

![algorithmImg](https://user-images.githubusercontent.com/42841888/56426727-41621500-62f4-11e9-987c-97a5d0e18356.png)

---

## 나의 풀이

처음에 든 생각은 문자열이니까 for 문을 돌려서 하나씩 빼야겠다는 생각이 들었다

그래서 먼저

```
for i in paramString {}
```

for 문을 만들었는데, 이때부터 조금 생각을 했다.

문자열이 1개씩 개별로 나와 i에 들어가는데, 이 i를 어떻게 할까?? 하고 생각을 해보니

처음에는 튜플에 넣을 생각을 했는데 튜플은 처음부터 튜플에 들어갈아이템의 갯수만큼 타입을 명시해서 초기화를 해주었어야 했다.

만약에, 몇 글자 일지 모르는 상황에서는 튜플에 못넣겠다는 생각에 튜플은 생각에서 지웟다

그리고 나서 생각한것이 배열이였는데 그전에 Set도 생각했다

그런데 Set은 중복값을 허용하지 않아서, 배열에 i에 들어오는 각각의 값을 append하여야 겠다는 생각을 했다

그래서 전역변수로 빈 배열값을 만들엇는데, 그 배열값이 각각 p와 y를 따로 넣어주고 그 갯수를 세어 비교하면 되겠다는 생각에

```
var arrayTempStoredP = [""]
var arrayTempStoredY = [""]
```

위와 같이 p와 y 따로 담을 수 있는 빈 배열 2개를 전역변수로 선언하고 나서

for 문 안에 if문으로 각각의 배열에 p와 y가 대소문자 구분 없이 나눠서 각자에 맞는 배열에 넣어주기 위해 아래와 같은 if문을 만들었다

```
for i in paramString {
        if i == "p" || i == "P" {
            arrayTempStoredP.append(String(i))
        } else if i == "y" || i == "Y" {
            arrayTempStoredY.append(String(i))
        }
```

이제 각각의 배열의 갯수만 비교하여 같으면 true 다르면 false를 반환하면 되겠다는 생각에

if 조건문을 한번 더 사용하여 배열 arrayTempStoredP과 arrayTempStoredY의 count를 통하여

갯수의 비교를 했다.

그 코드가 바로 아래의 코드이다

```
 if arrayTempStoredY.count == arrayTempStoredP.count {
        return true
    } else {
        return false
    }
```

이렇게 해서 모든 코드가 완성이 되었다

오늘은 여기까지~

---

## 전체 코드

```
var arrayTempStoredP = [""]
var arrayTempStoredY = [""]

func answer(_ paramString:String) -> Bool
{
    for i in paramString {
        if i == "p" || i == "P" {
            arrayTempStoredP.append(String(i))
        } else if i == "y" || i == "Y" {
            arrayTempStoredY.append(String(i))
        }
    }
    
    if arrayTempStoredY.count == arrayTempStoredP.count {
        return true
    } else {
        return false
    }
}
```
