---
layout: post
title:  "TableView List Method 공부(2) - 190415"
date:   2019-04-15
categories: Swift, iOS
---

TableView의 List를 만들때 필요한 코드와 메소드들을 알아보는 두번째 시간이에요

아주 주관적으로 저만 모르고 저만을 위한 글이라서 모든것을 다루지 않아요~

자 그럼 시작해볼까요 ㅋㅋ

```
final class ListViewController: UIViewController {
  let tableView = UITableView()
  var viewControllers: [UIViewController] = []

 override func viewDidLoad() {
    super.viewDidLoad()
    tableView.frame = view.frame
    tableView.delegate = self
    tableView.dataSource = self
    tableView.register(UITableViewCell.self, forCellReuseIdentifier: "List")
    view.addSubview(tableView)
  }
```

처음 클래스를 만들고 viewDidLoad 메소드에 앱의 초기에 필요한 값들을 정의하는 과정이에요

그 중에서 제가 궁굼했던 코드는 바로

```
tableView.register(UITableViewCell.self, forCellReuseIdentifier: "List")
```

바로 이 부분이랍니다

그럼 바로 알아봅시다

일단 **tableView.register** 이 부분에서 tableView는 이미 클래스를 생성하면서

정의해두었네요, 바로 아래와 같이 말이죠

```
let tableView = UITableView()
```

즉, tableView 는 UITableView 를 상속받아 인스턴스가 되는 상수에요

다시말해, tableView 는 UITableView의 인스턴스라는 말이죠~

자 그럼 UITableView 내에 있는 메소드겠네요 이 register 라는 친구는 말이죠

오호!! 그럼 이 register에 대해 알아봅시다~

register 메소드의 Quick Help에 보면 **새로운 테이블 셀을 만들기 위해 사용할 클래스를 등록 합니다** 라고 summary에 나와있어요

아하 그럼 register는 새로운 테이블 셀을 만들때 사용할 클래스를 등록하여 구분하거나 뭔가 다른 구현에 필요한 것들을 하겠죠?! 아직은 모르겠지만요...

여튼 다시 본론으로 돌아와 메소드의 정의 구문을 볼까요??

이 register 메소드는 이렇게 정의 되어 있어요, 바로 아래 처럼 말이죠.

```
func register(_ cellClass: AnyClass? forCellReuseIdentifier identifier: String)
```

이 register 메소드는 2개의 파라미터를 가지고 있네요, 그럼 이 두개의 파라미터를 어떤것을 받는지 알면 조금 더 이해도가 높아질꺼 같아요

그럼 먼저 첫번째 파라미터인 **cellClass: AnyClass?** 를 알아봐요

cellClass 는 **테이블에서 사용할 셀의 클래스**를 받는데요 그리고 UITableViewCell의 SubClass를 받아야 한데요 (Must be!!)

그런데!! 저는 여기서 궁굼한 점이 생겼죠,,,, 아니 몰랐어요,,,

이 메소드의 정의 구문 말고 코드에 작성된 것을 볼까요??

```
tableView.register(UITableViewCell.self, forCellReuseIdentifier: "List")
```

바로 이렇게 되어있는데 UITableViewCell.self 에요!!

잉?? UITableViewCell은 클래스이긴 한데 저는 파라미터로 받아야하는데 어디에도 없는

UITableViewCell을 어디서 받아오는거지?? 하고는 엄청 고민하고 알아봤어요

그런데,,,

이 UITableViewCell은 Apple에서 미리 정해놓은 지정 기본형인것이에요

무슨 말인지 모르겠죠?? 저도 잘 모르겠었어서, 더 공부를 해봤어요

그랬더니!! 바로 저 UITableViewCell은 클래스잖아요?? 이 UITableViewClass 를 상속 받은 새로운 클래스를 만들어 그 클래스를 UITableViewCell 형태
즉, Apple가 미리 정해놓은 Cell의 기본형이 아닌 제가 스스로 커스텀 해서 넣은 수 있다는 것을 알았어요!!

오!! 그럼 조금 이해가 가시나요?? 맞아요 저기에는 UITableViewClass를 상속 받은 모든 subclass 가 들어갈 수 있다고 위에 설명했듯이

UITableViewClass 를 상속받아 (subclassing) 원하는 모양으로 바꿔 넣으면 등록이 된다는 것이죠!!

이제야 궁굼증이 풀렸네요!1 그럼 다음으로 넘어가 봅시다~

이번에는 register 메소드의 두번째 파라미터인 forCellReuseIdentifier indentifier: String 를 알아봐요

아규먼트까지 쓰니까 길어서 이제는 파라미터 명만 쓰고 설명하도록 할게요

indentifier 메소드는 **셀의 재사용 식별자**라고 해요 그리고 **절대로 nil이거나 빈 문자열 값이면 안됩니다** 라고 설명되어 있어요

음,,, 그럼 다시말해보면 이 메소드에 들어가는 String는 ID와 같은 느낌이네요??

조금 더 쉽게 접근해봅시다

이 메소드의 summary 에 **새로운 테이블 셀을 만들기 위해 사용할 클래스를 등록 합니다** 라고 나와있었죠??

새로운 테이블 셀을 만들기 위해 사용할 클래스를 등록?!

그렇다면 **새로운 테이블 셀을 만들기 위해 사용할 클래스는** 바로 파라미터 cellClass 로 받은 값이겠네요?!

이 등록된 셀 클래스를 어떻게 사용할 것인지 혹은 다른 코드에 넣어 상호작용을 일으킬건데

정확하게 등록된 셀만 사용하기 위해 셀의 ID를 등록해준다고 생각하면 되겠네요

바로 indentifier: String 이 파라미터가 말이죠

```
extension ListViewController: UITableViewDataSource {
  func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return viewControllers.count
  }
  
  func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "List", for: indexPath)
    cell.textLabel?.text = "\(viewControllers[indexPath.row])"
    return cell
  }
}
```

아직은 정확하게 모르는 코드지만 UITableViewDataSource 프로토콜에 구현되어있는 메소드들을 사용하여 ListViewController 클래스를 확장하여 사용하는데,

그 중에 구현되어 있는 메소드 중에

```
  func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "List", for: indexPath)
    cell.textLabel?.text = "\(viewControllers[indexPath.row])"
    return cell
  }
```

이 메소드에 withIdetifier에 "List"가 들어가있는 것이 보이시나요??

무슨 메소드이고 어떤 행동을 하는지는 다음에 알아보도록 하고

이것만 보면 우리가 등록한 forCellReuseIdentifier indentifier: String
로 넣어준 값인 "List"를 사용하고 있네요

즉, register한 셀 클래스를 가지고 뭔가를 하겠다는 소리같은데,,,

다음에 알아보도록 해요 그건 중요한게 아니고 이렇게 "List"가 쓰인다는 것만 알면 된거에요

그래도 보면 forCellReuseIdentifier 이 아규먼트의 이름 그대로를 해석하면 뭔가 감이 잡히긴 해요

계속해서 **재사용, 재사용, 재사용!!!** 을 말하는걸 보니 재사용에 관한것이겠죠

아래의 모든 코드를 뜯어보고 해석해보면 더욱더 정확히 알 수 있을거에요. 

그럼 오늘은 여기까지!!
