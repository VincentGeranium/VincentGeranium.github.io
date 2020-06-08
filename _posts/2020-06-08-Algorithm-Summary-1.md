---
layout: post
title:  "알고리즘 풀이 : 프로그래머스 알고리즘 문제(서울에서 김서방 찾기)"
date:   2020-06-08
categories: iOS, Swift
---

이 포스트는 알고리즘 문제를 풀고 공부하고 정리한 내용 입니다.

- - -
- - -

### 예제 코드

- [서울에서 김서방 찾기 문제 코드](https://github.com/VincentGeranium/Algorithm-Study/tree/master/Algorithm-Practice/2020-06-07-Algorithm-Practice-1.playground)

- - -
- - -

### 서울에서 김서방 찾기 문제 풀이와 배운점.

<img width="1058" alt="200608-Algorithm-Image-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/200608-Algorithm-Image-1.png?raw=true" title="200608-Algorithm-Image-1">
<img width="1058" alt="200608-Algorithm-Image-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/200608-Algorithm-Image-2.png?raw=true" title="200608-Algorithm-Image-2">

#### firstIndex(of:)

<img width="1058" alt="firstIndexQuickHelpImage" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/firstIndexQuickHelpImage.png?raw=true" title="firstIndexQuickHelpImage">

- firstIndex(of:) 메소드는 collection 안에 있는 특정한 값의 위치를 가져올 수 있다.

- 위의 그림에서 "i"는 "Maxime"의 위치인 3을 가져오고, students[i]에 "Max"를 넣어줌으로서 students의 "Maxime" 의 위치에 "Max"가 들어가게 된다.

- 전달인자로 들어온 값의 위치를 찾으면 그 위치인 값 (Int)를 반환하고 없을 경우에는 nil을 반환한다.

- - -
- - -