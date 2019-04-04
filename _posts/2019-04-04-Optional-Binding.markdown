---
layout: post
title:  "옵셔널 바인딩"
date:   2019-04-04
categories: Swift
---

# Optional Binding

---
  
- 옵셔널 바인딩은 주로 if let (또는 if var) 구문과 함께 사용한다.  
    - **"먼저 체크해 준다(nil인지, 값이 있는지)"** 라고 생각하면 편하다
- nil인지 아니면 값이 있는지, 앞에 말한 경우에 따라 결과를 달리하고 싶을때 **옵셔널 바인딩** 사용하여 검사한다
- **if let(또는 if var)구문으로 옵셔널 바인딩을 실행하였을때, "nil이 들어있으면 if 구문이 실행되지 않는다"**
    - 이유는 값이 있을때만 바인딩 되기 때문이다
    - 그래서 if let 또는 if var 구문을 통해 nil일 경우와 아닌 경우를 안전하게 대비 할 수 있다

---

[예시 코드 및 설명 주석 playground](https://github.com/VincentGeranium/Swift-Study/tree/master/OptionalBindingExample.playground)
