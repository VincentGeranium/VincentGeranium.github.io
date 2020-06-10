---
layout: post
title:  "알고리즘 풀이 : 백준 온라인 저지 알고리즘 문제(1000번, A + B), readLine()"
date:   2020-06-08
categories: iOS, Swift
---

이 포스트는 알고리즘 문제를 풀고 공부하고 정리한 내용 입니다.

- - -
- - -

### 예제 코드

- [백준 온라인 저지 알고리즘 문제(1000번, A + B) 코드](https://github.com/VincentGeranium/Algorithm-Study/tree/master/Algorithm-Practice/2020-06-09-Algorithm-Practice-1)

- - -
- - -

### 참고 자료

- [ZeddiOS](https://zeddios.tistory.com/68)

- - -
- - -

### 백준 온라인 저지 알고리즘 문제(1000번, A + B)

<img width="820" alt="baekjoon-1000" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/baekjoon-1000.png?raw=true" title="백준1000번문제스크린샷">

- A + B 문제에서 보면 입력을 첫째 줄에 A와 B가 주어진다고 나와있다.

    - 즉, 한 줄에 A와 B가 둘 다 입력 받는다는 말이다, 변수를 하나만 쓰고 입력을 받아야 한다.
    
        - 그렇다면 int는 사용하지 못한다. 그 이유는 입력이 스페이스로 나눠져있기 때문이다.
        
- 해결방법은 String을 사용하여 A와 B 값을 받아와 전달인자로 받은 String 값 조건으로 나누는 메소드 components(separatedBy:)를 사용해 Array에 A와 B를 각각의 값으로 나누어 받아온 뒤 각각의 두 값을 더해주면 해결이 된다.

    - 그래서 components(separatedBy:) 메소드를 사용했다.
    
<img width="820" alt="componentsImg-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/componentsImg-1.png?raw=true" title="컴포넌트메소드정의이미지">    
    
- components(separatedBy:) 메소드는 전달인자로 받아온 값을 조건으로 하여 값을 나눈뒤 그 값을 한 Array에 담아 return하는 메소드이다.

- 나눠 받아온 Array return 값을 가져와 Array의 index를 이용하여 A와 B 값을 더해주면 된다.

### Swift에서 키보드 입력 받는 법 (User input) - readLine()

- Swift에서 키보드 입력 받는 가장 편한 함수 = readLine()

- readLine() 함수를 플레이그라운드에서 함수 사용은 가능하지만 키보드 입력을 받지는 못한다.

    - 플레이그라운드는 샌드박스이기 때문에 input이 없다.
    
        - "sandbox"란 외부로부터 들어온 프로그램이 보호된 영역에서 동작해 시스템이 부정하기 조작되는 것을 막는 보안 형태이다.

- 키보드 입력을 받을 수 있는 방법은 actual application을 이용하는 것이다.

    - actual application이란 아래의 그림과 같다
    
<img width="820" alt="commandLineToolImage" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/commandLineToolImage.png?raw=true" title="commandLineToolImage">

- 프로젝트를 command line tool 만들 때, 언어를 Swift로 선택해서 만들어야 한다.

#### Standard input in Swift - readLine()

- readline 은 한 줄을 읽어들이는 함수이다.

<img width="820" alt="readLineScreenShot-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/readLineScreenShot-1.png?raw=true" title="readLineScreenShot-1">

<img width="820" alt="readLineScreenShot-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/readLineScreenShot-2.png?raw=true" title="readLineScreenShot-2">

- 정수를 넣으면 Optional("정수"), 문자를 넣으면 Optional("문자")가 나온다.

<img width="820" alt="readLineScreenShot-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/readLineScreenShot-3.png?raw=true" title="readLineScreenShot-3">

- readLine의 return 값이 Optional 로 나오는 이유는 위의 그림에서 보면 readLine()의 return 값이 "String?" 이기 때문이다.

- - -
- - -