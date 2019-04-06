---
layout: post
title:  "Property Observer-didSet, willSet"
date:   2019-04-06
categories: Swift
---

# Property Observer

---

Property Observer의 didSet과 willSet에
대해 알아보자
didSet과 willSet의 역활은 값이 변경되기 직전과 직후를 감지하는 것이다
기본적인 구문은 다음과 같다

```
var someProperty: Int = 10 {
    didSet(oldValue) {
        //someProperty의 값이 변경된 직후 호출, oldValue는 변경 전 someProperty의 값
    }
    willSet(newValue) {
         //someProperty의 값이 변경되기 직전에 호출, newValue는 변경될 새로운 값
    }
}
```

프로퍼티 옵저버를 사용하려면 꼭 **초기화**가 되어 있어야 한다.
또한 **클래스 init()** 사용하여 값을 초기화 해주려고 할때는 didSet과 willSet은 호출 되지 않는다
즉, 초기화 이후부터 프로퍼티를 감시한다

프로퍼티 옵저버의 가장 빈번한 사용은 Model에서 갱신된 값을 View에 보여줄 때 이다
예를들어 View에 점수를 표시하는 Label을 만들어 점수가 바뀔때마다 업데이트 해주고 싶다고 하자
그럼 점수가 바뀔때마다를  프로퍼티 옵저버를 이용하여 점수의 변화를 감시하여 그에 알맞는 행동을 취해줄 수 있다
이 경우에는 점수를 저장하는 score라는 변수를 만들고 값을 바꾸어준느 코드를 작성해보자

```
score: Int = 85
scoreLabel.text = "score: \(score)"
```

위와 같은 코드를 작성해도 점수가 바뀔때마다 계속해서 값을 업데이트 해 줄 수 있다 그러나 여러곳에서 값이 바뀌는 것을 알아야 한다라고 가정하면 그 곳마다 위의 코드를 다시 다 써주어야하고 한곳이라도 위 코드가 빠지게되면 값이 업데이트 되지 않는다

그럴때 프로퍼티 옵저버를 사용하면 된다

```
var score:Int = 0{
    didSet {
         scoreLabel.text = "score: /(score)"
    }
}
```

이렇게 하면 값이 바뀔때마다 View의 값을 갱신 하는 작업을 따로 해줄 필요가 없다

프로퍼티 옵저버를 이용하면 현재 값과 바뀔 값을 비교하는 작업을 수행 할 수도 있다

```
var score: Int = 0 {
    didSet(oldValue) {
         print("현재 점수는 /(self.score) 이고, 이전 점수는 /(oldValue) 입니다")
    }
}
```

그렇다면 willSet으로도 바뀔 값을 미리 알아서 그에 따른 처리를 해 줄 수 있다

```
var score: Int = 0 {
    didSet(oldValue) {
         print("현재 점수는 /(self.score)이고, 이전 전수는 /(oldValue)입니다"
    }
    willSet(newValue) {
         print("현재 점수는 /(self.score)이고, 바뀔 점수는 /(newValue)입니다"
    }
}
```
