---
layout: post
title:  "TableView Code Review"
date:   2019-04-13
categories: Swift
---

# Table View Study

---

# Table View Code Review

---

이번에는 다음 사진처럼 시뮬레이터에 나올 수 있도록 구현한 코드의 내용들을 정리해보겠습니다

![firstImg](https://user-images.githubusercontent.com/42841888/56051271-08242500-5d89-11e9-94a1-08e2f225c832.png)

- 위의 사진 속 빨간 네모 칸 안에 들어있는 내용 구현 리뷰
    - 그걸 터치하면 아래의 사진과 같은 테이블 뷰가 나온다

![secondImg](https://user-images.githubusercontent.com/42841888/56051399-6d781600-5d89-11e9-946c-81f62fabfabc.png)

- 위의 사진과 같은 뷰가 나올 수 있게 구현 한 코드 내용 리뷰

위에서 사진과 함께 밑에 설명한대로 학습 목표를 잡고 코드를 리뷰 해보겠습니다.

주관적인 리뷰이므로 제가 모르거나 궁굼했던 코드만 쏙쏙 뽑아 설명하고 어떻게 쓰이는지에 대한 내용 정리 할 것입니다.

전체 코드는 아래에 하이라이트로 하여 보여드리겠습니다

---

```
override var description: String {
    return "TableView - Basic"
  }
```

위의 코드는 description라는 프로퍼티를 override하였다
이 description이라는 프로퍼티의 return 값으로 String 타입을 받는데
이 return 값으로 들어가는 String가 바로 맨 처음 그림의 네모 박스 안에 있는 테이블 뷰 셀의 이름이 되는 것이다

```
tableView.dataSource = self 
```

블로그에 포스팅 된 글 중에 [ListViewController 공부](https://vincentgeranium.github.io/swift,/ios/2019/04/12/ListViewController-Study.html) 있는데 이 글의 처음부분에 UITableViewDataSource 프로토콜에 대한 코드 리뷰를 해놓은 부분이 있다 그 부분과 함께 보면 이해가 잘 될것이다

다시 본론으로 돌아와 그 UITableViewDataSource 프로토콜을 구현하고 그 구현된 코드를 어디에서 받아서 실행하고 구현 할 것인지에 대한 코드이다

tableView.dataSource = self 는 현재 이 글의 전체코드에서 보면 알 수 있듯이 final class TableViewBasic 스코프 안에서 구현되고 있다 그래서 그 self은 TableViewBasic 클래스를 뜻하고 그 UITabelViewDataSource 프로토콜 안에 구현된 내용들을 이 class 가 받아서 구현하겠다는 뜻이다

**delegate 와 같은 방법이다**

delegate 프로토콜을 만들고 그 프로토콜 안에 어떠한 메소드나 여러가지를 구현할 것이라는 설명서만 만들어 놓고 그것을 어디서 직접 커스텀하여 **어디** 구현 할 것인가에 대한 코드도 위의 코드와 똑같이 하면 된다 즉, **어디** 라는 키워드가 중요하다

```
view.addSubview(tableView)
```

view 즉 rootView 위에 .addSubview() 메소드를 사용하여 다른 뷰 객체를 쌓는것이다
저 view가 굳이 rootView 일 필요는 없다
다시말해 어떤 뷰 위에 다른 뷰를 띄울때, superviewName.addSubview(subviewName) 이런식으로 쌓으면 되는 것이다

```
tableView.register(UITableViewCell.self, forCellReuseIdentifier: "CellId")
```

UITableView의 메소드인 .register()을 봐보자 register 메소드의 정의는 다음과 같다

```
func register(_ cellClass: AnyClass?, forCellReuseIdentifier idetifier: String)
```

이 코드를 하나씩 뜯어보자

먼저 이 register 메소드의 summary를 보면 **새 테이블 셀을 만드는데 시용할 클래스를 등록합니다** 라고 나와 있다.

이 register 메소드의 discussion을 보면 모든 셀을 큐에서 제거하기 전에 이 메소드 또는 레지스터 메소드 (_:forCellReuseIdentifier: )를 호출하여 테이블 뷰에 새로운 셀의 생성을 알리고, 지정된 유형의 셀이 현재 재사용 큐에 없으면 테이블 뷰는 제공된 정보를 가지고 새로운 셀 객체를 자동으로 생성한다.
이전에 동일한 indentifier로 클래스 또는 nib 파일을 등록한 경우 cellClass 파라미터가 지정한 클래스가 이전의 항목을 대체하게 된다.
지정된 reuse indentifier 에서 클래스 등록을 취소 하려면 파라미터인 cellClass에 nil 값을 지정하면 된다

이번에는 파라미터를 살펴보자

이 메소드에는 cellClass 라는 파라미터와 identifier 라는 파라미터가 있다
이 두 파라미터에 대해 알아보면, 

먼저 cellClass는 table에서 사용하려는 셀의 클래스를 받는데 UITableViewCell의 subclass이어야 한다(UITableViewCell 자기 자신도 가능)

두번째로, identifier 라는 파라미터는 셀의 재사용 식별자이다. 이 파라미터는 nil이 아니어야 하며 빈 문자열이면 안된다.
즉, 쉽게 말하 아이디라고 생각하면 된다, 나라는 것을 인터넷이나 여러 온라인 상에서 식별되게 하려는 매개체가 ID 이듯이 이것도 그와 같은 기능을 한다고 생각하면 된다

```
extension TableViewBasic: UITableViewDataSource {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 10
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
      let cell = tableView.dequeueReusableCell(withIdentifier: "CellId", for: indexPath)
        cell.textLabel?.text = "\(indexPath.row)"
        return cell   
    }
```

이번에는 TableVieBasic 클래스를 확장하여 UITableViewDataSource 프로토콜을 채택하는 코드를 한번 봐보자

일단 UITableViewDataSource는 **데이터를 관리하고 테이블 뷰에 셀을 제공하는데 사용하는 객체에서 사용** 라고 summary에 나와있다.

즉, 위와 같은 기능들을 구현하고 싶으면 위의 이 프로토콜 내에 있는 기능들을 커스텀해서 사용하면 된다

먼저

```
extension TableViewBasic: UITableViewDataSource
```

어떠한 대리자 delegate나 프로토콜을 명시하여 그 클래스에서 사용하게 하려면 위와 같이 extension 을 사용하여 해당 클래스를 확장시켜 줘야 한다 그 키워드가 방금 전에 말한 **extension** 이다

즉,쉽게 말해 게임의 확장팩 같은 느낌으로 받아들이면 된다.
내가 디아블로2의 확장팩 구매했다고 가정을 하자, 확장팩은 디아블로2 게임의 기능을 넓히고 어떠한 다른 캐릭터나 스킬 또는 여러 아이템이나 게임의 컨텐츠를 넓혀서 더해주는 역활은 하는것이다. 
이것을 extension 키워드와 같은 개념으로 보면 되는것이다.

UITableViewDataSource 프로토콜이 가지고 있는 여러 기능들 중 몇가지를 선택하고, TableViewBasic 클래스를 확장하여 UITableViewDataSource 프로토콜이 가지고 있는 여러 메소드들 중 내가 구현하고 싶은 기능들이 들어있는 메소드를 내 방식으로 커스텀 하여 그 기능들을 TableViewBasic 클래스에 넣어 기능을 구현하겠다는 것이다.

그렇게 되면 TableViewBasic는 원래의 TableViewBasic Class 확장팩이 되는것이다

위의 코드 상에서는 UITableViewDataSource 프로토콜이 가지고 있는 메소드 중 2가지를 사용하였는데 그 2가지의 메소드를 뜯어보자

먼저

```
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 10
    }
```

위의 메소드는 **테이블 뷰에 지정된 섹션에 있는 행 수를 반환하도록 데이터 소스에 지시** 한다고 summary에 나와있다.

그렇다면 어떠한 파라미터를 쓸까?? 한번 알아보자.

이 메소드는 2개의 파라미터를 사용하는데 tableView 와 section을 사용한다

먼저 tableView 파라미터를 알아보자, tableView 파라미터는 **정보를 요청하는 테이블 뷰 객체** 를 받는다

어떠한 정보냐 하면 이 메소드에서 리턴 값으로 반환하는 **섹션의 행의 수**를 의미한다

두번째로 section 파라미터는, **테이블 뷰에서 섹션을 식별하는 인덱스 번호** 를 받는다

그리고 **리턴 값으로는 섹션의 행의 수를 반환한다**

이번에는 아래의 메소드에 대해 알아보자

```
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {

let cell = tableView.dequeueReusableCell(withIdentifier: "CellId",
for: indexPath)
cell.textLabel?.text = "\(indexPath.row)"
return cell 

}
```

먼저 메소드 내에 구현한 내용을 보기전에 어떠한 기능을 하는지 위 코드의 메소드에 대해 알아보자

위 코드에 나와있는 메소드는 **테이블 뷰의 특정 위치에 삽입 할 셀의 데이터 소스를 요구**하는 기능을 하는 메소드 이다.

이 메소드에는 두 개의 파라미터를 받는데 tableView와 indexPath 두 가지가 있는데, 이 두가지를 알아보자

먼저, tableView 파라미터는 **셀을 요청하는 테이블 뷰 객체**를 받는다

두번째로, indexPath 파라미터는 **테이블 뷰에서 행을 찾는 index path**를 받는다

리턴으로는 UITableViewCell 타입을 반환 받는데 이 리턴값은 **테이블 뷰가 지정된 행으로 사용 할 수 있는 UITableViewCell로 부터 상속한 객체이다, UIKit은 nil를 반환하면 assertion을 일으킨다**

여기서 **assertion**은 assert(_:_:file: line:) 함수를 사용하는 것인데 assert 함수는 디버깅 모드에서만 동작한다. 주로 디버깅 중 조건의 검증을 위하여 사용하는 것인데

이것은 아직 더 파고들기에는 내가 지식이 부족하므로 천천히 나중에 더 알아가보도록 하자

다시 본론으로 돌아와

이 메소드 내에 작성된 코드를 뜯어보자

```
let cell = tableView.dequeueReusableCell(withIdentifier: "CellId", for: indexPath)
cell.textLabel?.text = "\(indexPath.row)"
return cell
```

먼저 상수인 cell을 만들고 UITableView내에 있는 메소드인 dequeueReusableCell를 작성하여 cell에 넣어주는데 그럼 dequeReusableCell 메소드를 알아보자

```
func dequeueReusableCell(withIdentifier identifier: String, for indexPath: IndexPath) -> UITableViewCell
```

dequeReusableCell 의 정의를 보면 위와 같다

이 dequeReusableCell은 **지정된 재사용 ID에 대한 재사용 가능한 테이블 뷰 셀 객체를 반환하고 이를 테이블 뷰에 추가한다** 라고 summary 에 나와있다

dequeReusableCell은 두가지의 파라미터를 받는데 identifier와 indexPath를 받는다

먼저 identifier에 대해 알아보면, identifier는 **재사용 할 셀 객체를 식별하는 문자열**을 받는다 이 파라미터는 **nil이면 안된다**

두번째는 indexPath에 대해 알아보자 indexPath는 **셀의 위치를 지정하는 인덱스 경로**를 받는다 이 파라미터는 **항상 데이터 소스 객체에서 제공하는 인덱스 경로를 지정해야 한다**
그리고 **인덱스 경로를 사용하여 테이블 뷰에서 셀의 위치를 기반으로 하여 추가 구성을 수행한다**

---

# Code

```
import UIKit

final class TableViewBasic: UIViewController {
  
  override var description: String {
    return "TableView - Basic"
  }
  
  override func viewDidLoad() {
    super.viewDidLoad()
    
    let tableView = UITableView(frame: view.frame)
    tableView.dataSource = self
    view.addSubview(tableView)
    
    tableView.register(UITableViewCell.self, forCellReuseIdentifier: "CellId")     
  }
}

extension TableViewBasic: UITableViewDataSource {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 10
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {

        let cell = tableView.dequeueReusableCell(withIdentifier: "CellId", for: indexPath)
        cell.textLabel?.text = "\(indexPath.row)"
        return cell
    }
}
```
