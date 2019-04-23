---
layout: post
title:  "Algorithm Practice - 190423"
date:   2019-04-23
categories: Algorithm, iOS, Swift
---

# 190423-Algorithm-Practice

---

## 프로그래머스 알고리즘 연습

## 가운데 글자 가져오기

![algorithmImg](https://user-images.githubusercontent.com/42841888/56545602-0a6d5700-65b3-11e9-8fa4-9d534e1b4f2b.png)


---

## 나의 풀이

가운데 글자를 가져오는 알고리즘을 만들어보는데 처음 이 문제를 접하자 마자 생각이 든 것은

for 반복문으로 문자열을 하나씩 빼서 그 문자열의 갯수를 셀 수 있게 해야겠다는 생각을 했다

그래서 일단 아래와 같은 for 반복문을 만들었다

```
func solution(_ s:String) -> String {
    for i in s {}
```

그럼 이 for 반복문으로 문자열의 갯수를 셀 수 있게 만들어야 하는데 문자열의 갯수를 어떻게

카운트 할까?? 하는 생각에 카운트를 사용 할 수 있는 배열에 차곡 차곡 쌓아서 갯수를 세면 되겠다는 생각을 했다

그래서 아래와 같은 코드를 만들었다

먼저 for 반복문으로 인자값으로 받는 문자열을 하나씩 빼서 i 에 넣고 그 i는 Character 타입이므로 String 타입으로 형 변환 하여 빈 배열에 넣어주는 코드를 만들었다

```
var countArr: Array<String> = []

func solution(_ s:String) -> String {
    for i in s {
        countArr.append(String(i))}
```

이렇게 되면 이제 for 문을 통해 문자열이 들어오고 그 문자열의 갯수만큼 for 반복문이 돌면서

빈 배열에 문자열이 하나씩 쌓이게 된다

그럼 이 하나씩 쌓여간 배열을 어떻게 하면 될지 생각을 햇다

일단 문자열의 길이를 배열의 카운트로 측정 할 수 있으니 문자열의 짝수와 홀수로 나눠 각기 다른

논리구조로 만들어 줘야겠다는 생각을 했다

그래서 먼저 if 문으로 홀수와 짝수를 나눌 수 있는 구조를 만들었다

```
func solution(_ s:String) -> String {
    for i in s {
        countArr.append(String(i))
        if countArr.count % 2 == 0 {
            
        } else {
          
        }
    }
}
```

이렇게 홀수와 짝수를 나누는 논리 제어문을 만들었으니 각각의 조건에 맞는 패턴을 정해줘야 한다고 생각했다

그런데 여기서 문제가 생겼다

처음 내가 생각한것은 가운데 글자를 뽑아 와야 하니 만약 문자열이 짝수면 배열의 카운트의 값을 반을 나눠 나온 몫, 

그 몫과 그 몫 + 1의 값을 각각 뽑아야 하는 글자 1, 글자 2 로 하여 뽑으면 되겠다는 생각을 했다

```
"abcd" => 반으로 나누면 2
첫 글자  =  배열의 index 2번째를 뽑아오자
두번째 글자 = 배열의 index 2 + 1 번째를 뽑아오자

그러면 bc 가 나오겠지?
```

위와 같은 생각으로 코드를 만들었더니 **Fatal error: Array index out of range**

에러가 계속 났다.

배열 인덱스가 범위를 벗어난다는 뜻이 뭘까 하고 생각해보니

**배열의 .count 한 값과 배열의 index 값은 다르다는 것을 알았다**

예를들어

```
let testArr = ["a","b","c","d"]
testArr.count
```

이 카운트 값은 배열의 요소의 갯수 값 즉, 4가 나오고

```
let testArr = ["a","b","c","d"]
testArr.startIndex
```

배열의 인덱스 값은 0부터 시작하여 이 testArr의 마지막 인덱스 값은 3이 되어

배열의 요소 갯수 값과 인덱스 값에는 차이가 있어서 논리 구조를 다시 짜야한다는 생각이 들었다

그럼 배열의 카운트 값의 연산을 이용해 배열의 인덱스 값을 뽑아 내야 하므로

배열의 인덱스 값에 맞게 배열의 카운트 값 연산 식을 다시 짜야 한다

그럼 생각을 해보면 배열의 카운트 값은 배열의 인덱스 값보다 1이 크므로

배열의 카운트 값의 -1 씩을 해주면 내가 원하는 인덱스 값의 배열 내의 요소를 뽑아 낼 수 있는 것이다

그럼 위의 내용을 토대로 생각을 해보면

예를들어 배열내의 카운트 수가 짝수 즉, 문자열이 짝수의 길이이면

문자열의 중간 문자를 뽑아야 하므로 두개의 문자를 뽑아야 한다

그렇다면 뽑아야 하는 첫번째 문자는 배열의 카운트의 / 2를 한 값에 -1 를 하면 뽑혀나온다

```
첫번째 문자 뽑기

"asdf"

4 / 2 = 2 -> "d"
(4 / 2) - 1 = 1 -> "s"
```

그럼 두번째 문자는 위의 수식에 +1을 하면 바로 뒤의 문자를 뽑을 수 있다

```
"asdf"

4 / 2 = 2 -> "d"
(4 / 2) - 1 = 1 -> "s"

두번째 문자 뽑기

1 + 1 = 2-> "d"
```

이렇게 배열의 카운트가 짝수 즉, 문자열의 길이가 짝수인 것의 중간 값을 빼오는 수식을 만들었다

그렇다면 이제 홀수 부분을 만들어야 하는데 배열의 카운트가 홀수 즉, 문자열의 길이가 홀수이면

그냥 그 배열의 카운트의 중간값을 빼오면 문자열의 중간값이 된다

```
"asd"

index => 0: a, 1: s, 2: d

3 / 2 = 1 -> 중간 문자 s
```

위의 내용을 종합적으로 만들면 전체의 로직이 완성된다

```
for i in s {
        countArr.append(String(i))
        if countArr.count % 2 == 0 {
            first = (countArr.count / 2) - 1
            second = (first) + 1
            returnValue = countArr[first] + countArr[second]
        } else {
            first = countArr.count / 2
            returnValue = countArr[first]
        }
```

---

## 깃헙 내에 있는 코드 링크

[github](https://github.com/VincentGeranium/Algorithm-Study/tree/master/Algorithm-Practice/190423-Algorithm-Practice.playground)

---

## 전체 코드

```
var countArr: Array<String> = []
var first: Int = 0
var second: Int = 0
var returnValue: String = " "

func solution(_ s:String) -> String {
    for i in s {
        countArr.append(String(i))
        if countArr.count % 2 == 0 {
            first = (countArr.count / 2) - 1
            second = (first) + 1
            returnValue = countArr[first] + countArr[second]
        } else {
            first = countArr.count / 2
            returnValue = countArr[first]
        }
    }

    return returnValue
}

solution("abde") // "bd"
```