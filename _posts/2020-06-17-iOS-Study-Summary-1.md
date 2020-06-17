---
layout: post
title:  "내비게이션 아이템, 바 버튼 아이템, 내비게이션 바 관련 TIL(UINavigationItem, UIBarButtonItem, UINavigationBar TIL)"
date:   2020-06-17
categories: iOS, Swift
---

이 포스트는 iOS 관련한 공부 내용을 정리한 포스트 입니다.

- - -
- - -
### 예제 코드

- [Table-CellHeight](https://github.com/VincentGeranium/MyMovieChart/tree/master/Table-CellHeight)

- - -
- - -

### 시점이 다름으로 인한 UIBarButtonItem의 Action이 동작 불능 상태.

- 아래의 그림과 같이 내비게이션 바 위에 "+" 버튼을 올려서 버튼을 누르면 내가 작성한 test 함수가 작동하여 콘솔에 "test"가 프린트되길 바랐다.

    <img width="820" alt="iosSummary-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/iosSummary-1.png?raw=true" title="iosSummary-1">
    
    <img width="820" alt="iosSummary-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/iosSummary-2.png?raw=true" title="iosSummary-2">
    
- 그래서 코드를 만들어 본 결과 "+" 버튼은 시뮬레이터에서 보면 내비게이션 바 위에 잘 올라와 있는데 버튼을 눌러도 위의 그림의 콘솔에서 보이다시피 아무것도 프린트되지 않았다.

    <img width="820" alt="iosSummary-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/iosSummary-3.png?raw=true" title="iosSummary-3">
    
- 그래서 위와 같이 lazy 키워드를 사용하니 제대로 동작하였다.

    <img width="820" alt="iosSummary-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/iosSummary-4.png?raw=true" title="iosSummary-4">
    
- 나는 위의 그림과 같이 뷰들을 쌓아 올렸는데 아마 시점의 문제였던것 같다.

- - -
- - -