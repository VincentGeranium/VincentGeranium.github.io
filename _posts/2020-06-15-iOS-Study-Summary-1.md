---
layout: post
title:  "테이블 뷰 TIL - 1 (TableView Study, Today I Learned - 1)"
date:   2020-06-15
categories: iOS, Swift
---

이 포스트는 iOS 관련한 공부 내용을 정리한 포스트 입니다.

- - -
- - -
### 예제 코드

- [MyMovieChart](https://github.com/VincentGeranium/MyMovieChart)

- - -
- - -

### 참고 자료

- [얄미대디님의 Blog](https://m.blog.naver.com/PostView.nhn?blogId=jdub7138&logNo=220963701224&proxyReferer=https:%2F%2Fwww.google.com%2F)

- [apple developer documentation - UITableViewCell](https://developer.apple.com/documentation/uikit/uitableviewcell)

- - -
- - -

### TableView Today I Learned

- '프로토타입 셀(Prototype Cell)'

    - 프로토타입 셀은 테이블 뷰의 셀을 원하는 대로 쉽게 디자인할 수 있도록 해주는 객체.
    
    - 프로토타입 셀은 버튼이나 텍스트 레이블과 달리 직접 데이터를 표시하거나 화면에 공간을 차지하지 않음.
    
    - 그저 테이블 뷰가 화면에 표현될 때 셀의 구성을 미리 보여주기 위한 가상의 틀.
    
- 프로토타입 셀 영역

    <img width="820" alt="prototypeCellImage" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/prototypeCellImage.png?raw=true" title="프로토타입셀이미지">
    
    - Cell Content : 셀에 표현될 콘텐츠
    
    - Accessory View : 콘텐츠의 부가 정보 여부를 암시
    
#### 데이터 소스 .

- 고정되지 않고 매번 갱신되는 내용 표현시 테이블 뷰 셀을 프로그래밍적으로 구성해 주어야 한다. 이를 위해서는 데이터 소스가 필요하다.
    
    - 테이블 뷰의 각 행마다 대응할 수 있도록 **배열 형태**이기만 하면 데이터 소스가 된다.
    
    - 데이터 소스를 테이블 뷰 각 행에 연결하는 과정을 **데이터 바인딩(Data Binding)**이라고 한다.
    
#### Value Object Pattern 

- 데이터 저장을 전담하는 클래스를 별도로 분리하는 설계 방식 (Value Object Pattern), 줄여서 VO.

    - 데이터 저장을 위한 클래스임을 쉽게 식별할 수 있게 하려고 클래스의 마지막에 VO라는 접미사를 붙인다.
    
    - 클래스 인스턴스 내부의 속성에 각각의 데이터들을 담은 다음, 전달할 때에는 클래스 인스턴스 전체를 전달하기 때문에 자연스레 클래스 내부의 변수에 저장된 값도 함께 전달된다.

    <img width="820" alt="VOpatternImage" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/VOpatternImage.png?raw=true" title="VO이미지">
        
#### lazy 키워드

- 배열 변수 list에는 lazy 키워드가 추가되어있다.

    <img width="820" alt="lazyKeywordImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/lazyKeywordImage-1.png?raw=true" title="lazyKeywordImage-1">
    
- 여기에는 두 가지 이유가 있다.

    - 1) 미리 생성해서 메모리를 낭비할 필요가 없기 때문.
    
        - lazy 키워드를 붙여서 변수를 정의하면 참조되는 시점에 맞추어 초기화되므로 메모리 낭비를 줄일 수 있다.
        
    - 2) lazy 키워드를 붙이지 않은 프로퍼티는 다른 프로퍼티를 참조할 수 없기 때문.
    
        - list 배열 변수를 초기화하는 데에는 dateSet 프로퍼티가 필요하다. 하지만 프로퍼티들이 초기화되는 순서는 개발자가 컨트롤할 수 있는 범위를 벗어나기 때문에 list 배열 변수의 클로저가 실행되는 시점에 dateSet 배열이 초기화되어 있다고 보장할 수 없다. **이 때문에 일반 저장 프로퍼티들끼리는 서로를 참조할 수 없다.**
        
        - 하지만 **lazy 키워드가 붙은 프로퍼티라면 다른 일반 프로퍼티들이 초기화된 후 맨 마지막에 초기화될 뿐만 아니라, 초기화되는 시점도 개발자가 통제할 수 있다.**
        
        - 따라서 **lazy 키워드가 붙은 프로퍼티의 초기화 클로저 구문 내에서는 다른 일반 프로퍼티를 참조하는 것도 가능하다.**
        
#### 테이블 뷰와 데티어 소스 연동

- 데이터 소스와 테이블 뷰를 연동하는 과정은 UITableViewDataSource라는 프로토콜에 의존하여 이루어진다.

    - 테이블 뷰 컨트롤러는 이 프로토콜을 참고하여 지정된 메소드를 호출함으로써 데이터 소스와 테이블 뷰를 연동한다.
    
- **테이블 뷰에 데이터 소스를 연동할 때 필요한 내용 두 가지.**

    - **1) 테이블이 몇 개의 행으로 구성되는가 ?**
    
    - **2) 각 행의 내용은 어떻게 구성되는가 ?**
    
#### 데이터 소스 연돌을 위한 핵심 메소드

- 테이블 뷰와 데이터 소스를 연동하는 데 필요한 기본 메소드는 아래와 같다.

    - **1) tableView(_:numberOfRowsInSection:)**
    
    - **2) tableView(_:cellForRowAt:)**
    
        - 이 메소드들은  iOS 시스템이 필요에 의해 호출하는 메소드들이다. 일종의 델리게이트 패턴을 따르고 있다.
        
        - 동작이나 이벤트에 관한 메소드가 아니므로 델리게이트라는 접미어를 붙이지는 않지만, 델리게이트 패턴과 동일한 방식으로 동작한다.
        
        - 시스템이 호출하는 **CallBack Function**로 생각하면 된다. 개발자가 알아서 적절한 시점에 호출하는 것이 아니라 작성해 두면 시스템이 알아서 호출하는 식. 일종의 지뢰 같은 방식으로 동작하는 함수.
        
#### tableView(_:numberOfRowsInSection:)

- **이 메소드는 테이블 뷰가 생성해야 할 행(row)의 개수를 반환한다.**

- 이 메소드는 iOS 시스템이 테이블 뷰를 구성하기 위해 먼저 호출하는 메소드이다.

    - 이 메소드는 개발자가 사용하기 위한 것이 아니라 시스템이 사용하기 위한 메소드이다.
    
    - **즉, 현재 몇개의 행이 구성되어 있는지를 개발자에게 알려주는 역활이 아니라 몇 개의 행을 생성해야 할지 개발자가 iOS 시스템에게 알려주기 위해 작성하는 메소드이다.**
    
- **이 메소드는 이미 만들어진 테이블 뷰의 행 개수를 결과값으로 반환하는 용도가 아니다. 이 메소드에 의해 테이블 뷰의 행 수가 결정되는 것이다.**

- 이 메소드를 이용해서 테이블 뷰가 생성할 행의 개수를 작성해 놓으면 iOS 시스템은 메소드를 호출한 다음, 반환된 값만큼 목록을 생성한다.

- **생성해야 할 행 수는 개발자가 임의로 지정해주기보다는 데이터 소스의 크기를 동적으로 반환하는 방식으로 처리하는 것이 바람직하다.**

    <img width="820" alt="numberOfRowsInSectionMethod-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/numberOfRowsInSectionMethod-1.png?raw=true" title="numberOfRowsInSectionMethod-1">

- **1) 첫 번째 인자값은 이 메소드를 호출한 테이블 뷰 객체에 대한 정보를 나타낸다.**

    - 하나의 뷰 컨트롤러 내에 두 개 이상의 테이블 뷰가 존재할 수 있다. 테이블 뷰가 여러 개일 때에도 모두 같은 메소드를 호출하는데 이때, 호출되는 메소드 입장에서는 어느 테이블 뷰에서 자신을 호출하는지를 알 필요가 있기 때문에, 이를 위해 첫 번째 인자값이 사용된다.
    
- **2) 두 번째 인자값은 섹션에 대한 정보이다.**

    - 테이블 뷰는 일종의 행 그룹의 개념인 섹션으로 이루어질 수 있고, 그 하위에 개별 생이 추가된다.
    
    - 섹션별로 행의 수를 다르게 구성할 수 있기 때문에 섹션에 따라 구분하여 행의 개수를 반환해야 할 때도 있다.
    
        - 따라서 섹션에 대한 정보도 함께 요구된다.

- **필요에 따라서는 테이블 뷰 정보와 섹션 정보를 바탕으로 반환값을 다르게 줄 수도 있다.**

    - 이 테이블 뷰의 섹션은 몇 개의 행을 가져야 하고, 저 테이블 뷰의 저 섹션은 몇 개의 행을 가져야 한다라는 식으로.
    
#### tableView(_:cellForRowAt:)

- **이 메소드는 각 행이 화면에 표현해야 할 내용을 구성하는 데에 사용된다.**

- **이 메소드가 반환하는 값은 전체 테이블 뷰의 목록이 아니라 하나하나의 개별적인 테이블 셀 객체이다.**

    - 이는 화면에 표현해야 할 목록의 수만큼 이 메소드가 반복적으로 호출된다는 것을 의미한다.
    
- 메소드 내에서 테이블 뷰 셀 객체를 구성한 다음 결과값으로 반환하면 시스템은 이 객체를 받아 테이블 뷰의 목록 각 행에 채워 넣는 방식이다.

- 개발자가 작성한 데이터 소스는 이 메소드 내부에서 활용되어 특정 행의 콘텐츠를 구성하는 데에 사용된다.

- iOS 시스템은 테이블 뷰를 구성하기 위해 먼저 **tableView(_:numberOfRowsInSection:)를 호출하여 몇 개의 행을 생성해야 하는지를 반환받고, 그 수만큼 tableView(_:cellForRowAt:) 메소드를 호출한다.**

    - tableView(_:cellForRowAt:) 메소드 매 호출 시마다 몇 번째 행에 대한 요청인지를 함께 전달하기 때문에 개발자는 이 값을 받아, 해당 행에 적절한 콘텐츠를 구현한 다음 이를 테이블 뷰 셀 객체의 형태로 리턴하면 된다.
    
    <img width="820" alt="cellForRowAtMethod-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/cellForRowAtMethod-1.png?raw=true" title="cellForRowAtMethod-1">
    
- iOS 시스템은 tableView(_:cellForRowAt:) 메소드의 두 개의 인자값을 사용하여 이 메소드를 호출한다.

    - **1) 구성할 테이블 뷰 객체에 대한 참조.**
    
    - **2) 구성할 행에 대한 참조 정보.**
    
- **하나의 뷰 컨트롤러 안에 두 개 이상 테이블 뷰가 사용될 경우, 첫 번재 인자값으로 전달된 tableView 매개변수를 사용하면 어느 테이블 뷰에 대한 요청인지 구분 가능하다.**

    - 단순히 구분 용도만이 아니라 테이블 뷰 자체에 대한 참조가 필요할 때에도 사용할 수 있다.
    
- **첫 번째 매개변수를 통해 테이블 뷰가 특정되면, 두 번째 매개변수인 indexPath를 통해 몇 번째 행을 구성하기 위한 호출인지를 구분할 수 있다.**

    - **IndexPath 객체 타입으로 정의된 이 매개변수는 선택된 행에 대한 관련 속성들을 모두 제공한다.**
    
        - **그 중에서도 .row는 가장 많이 사용되는 속성으로, 행의 번호를 알려주는 역활을 한다.**
        
        - 0부터 시작하는 이 행 번호는 배열로 이루어진 데이터 소스의 아이템 인덱스와 대부분의 경우 일치하므로 이 속성을 사용하면 데이터 소스의 필요한 부분을 편리하게 읽어 들일 수 있다.
        
- - -
- - -