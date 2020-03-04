---
layout: post
title:  "DispatchQueue를 활용한 비동기 프로그래밍 Summary"
date:   2020-03-04
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다.

[edwith iOS 프로그래밍 - DispatchQueue를 활용한 비동기 프로그래밍](https://www.edwith.org/boostcourse-ios/lecture/16918/)

- - -

### Async Programming used by DispatchQueue

![AsyncProgrammingUsedbyDispatchQueueImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AsyncProgrammingUsedbyDispatchQueueImage-1.png?raw=true)

- 위의 그림에서 보면 `let dataTask: URLSessionDataTask`의 클로저는 백그라운드에서 동작할 클로저이다

- `self.mainTableView.reloadData()`는 메인 스레드에서 동작해야하는 메소드이기 때문에 그냥 아무런 처리 없이 `dataTask`의 클로저 내부에 넣어주면 앱이 꺼지고 `error`가 생긴다

- `self.mainTableView.reloadData()`는 메인 스레드에서 동작해야하는 메소드이니까 `dataTask`의 클로저 내부에 `DispatchQueue.main.async`를 이용하여 비동기적으로 메인 스레드에서 처리 할 수 있도록 한다.
    
![AsyncProgrammingUsedbyDispatchQueueImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AsyncProgrammingUsedbyDispatchQueueImage-2.png?raw=true)

- 위의 그림에서 보면 `let imageURL: Data = try? Data(contentsOf: imageURL)`은 동기 메서드이기 때문에 이미지가 다운로드가 다 되기 전까지는 화면이 멈추게 된다.

- 그래서 화면 멈춤을 해결하기 위해서는 이미지를 다운로드 받는 부분을 백그라운드에서 실행하고 이미지를 뷰 안에 셋팅해주는 코드는 메인에서 실행해줘야 한다

- 백그라운드에서 실행될 코드를 `DispatchQueue.global().async`, 기본적으로 제공되는 백그라운드 큐 안에 넣어준다

- 백그라운드에서 실행될 코드를 다 작성하였다면 이제는 메인 스레드에서 실행될 코드를 `DispatchQueue.main.async`를 이용하여 메인 스레드에서 처리 할 수 있도록 한다.

- 또한 백그라운드에서 이미지를 다운받는 동안 사용자가 화면을 움직일 가능성이 있다, `사용자가 화면을 움직인다.`라는 말의 의미는 `셀의 인덱스가 바뀌어 버린다`라는 말이다.

- `그래서 셀이 지금 데이터를 셋팅해 주고있는 현재의 인덱스와 이미지가 다운로드가 끝났을 때의 인덱스가 상의할 수 있기 때문에 그것을 서로 일치하는 상황에서만 이미지를 셋팅해줘야 한다는 말이다`

![matchIndexImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/matchIndexImage-1.png?raw=true)

- 위의 그림과 같이 셀의 인덱스를 맞추어 줄 수 있는 코드를 작성해야 한다.

![matchIndexImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/matchIndexImage-2.png?raw=true)

- 그리고 나서 이 셀이 다음에 재사용되기 전에 셀의 이미지 뷰의 이미지는 없애 줘야하므로 위와 같은 코드를 만들어야 한다.

    - 이 이미지를 가져오기 전에 다른 이미지가 표현이 안되고 있는 상태로 비워줘야하기 때문이다.
    
- - -
### Code

[Vincent Code](https://github.com/VincentGeranium/edwithStudy-project-6/tree/master/Leacture-4-3)