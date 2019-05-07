---
layout: post
title:  "About Segue(종류, 메소드)"
date:   2019-05-07
categories: iOS, Swift
---

# About Segue

---

#### 이 포스트는 얄미대디님의 블로그 포스트를 참고하여 작성했다는 점을 미리 알려드립니다

[얄미대디님 블로그](http://blog.naver.com/PostView.nhn?blogId=jdub7138&logNo=220393890771&categoryNo=81&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView)

---

### Segue

사전적으로 Segue는 하나에서 다른 것으로 부드럽게 넘어가다라는 뜻을 가지고 있다

앱으로 말하면 화면전환을 뜻한다

(예를들어 아이폰에서 어떤 버튼을 눌렀을 때 다른 화면으로 넘어가는 것)

**세그웨이를 할 때는 늘 새로운 인스턴스 객체가 생성된다**

---

### Segue의 종류

- **Show**
    가장 일반적인 세그웨이, 새 화면으로 이동.
    Stack 구조로서 새 화면이 원래 화면 위를 덮는 구조
    
- **Show Detail**
     SplitView 구조에서 원해 화면을 Master, 새 화면을 Detail로 표시
     **아이폰에서는 똑같아 보이지만 아이패드로 보면 화면이 둘로 분할되서 보이게 된다**

- **Present Modally**
    새 화면이 모달처럼 원래 화면 위 전체를 뒤덮는다.
    원래 화면은 새 화면 뒤에 그대로 존재하게 된다.
    
- **Popover Presentation**
    **아이패드에서 팝업창을 띄운다**
    아이폰 앱에서는 Show Detail과 마찬가지로 큰 의미가 없다
    
---

### Unwind Segue

Segue가 여러개이고 서로 엉키고 설킬 때 dismiss로는 해결이 안되는 경우가 생긴다, 이때 사용할 수 있는 것이 바로 Unwind Segue이다

한마디로 꼬인 것들을 다 풀고 가는 Segue라고 보면 된다.

예를들어 화면이 두개라고하자, 이 두개의 화면 중 뒤에 있는 화면에 버튼을 만들고 첫번째 화면의 View Controller에

아래와 같은 코드를 적어준다

```
@IBAction func myExit(sender: UIStoryboardSegue) {
}
```

**여기서 중요한 것은 두번째 화면에 있는 버튼을 첫번째 ViewController가 제어하도록 할 것이라는 점**이다

보통 버튼이 있는 뷰에서 그 View Controller 파일에서 버튼에 대한 소스코드를 넣고 관리하는것이 정상적이지만

다르게 할 수 있다는 것도 알고싶어서 두번째 화면의 버튼을 이용하여 Unwind하는 것을 이 포스트에서 설명하려 한다

다시 본론으로 돌아와 첫번째 화면에 위와 같은 코드를 쓰고 두번째 화면에 버튼을 드래그하여 도크 안에 맨 오른쪽에 있는 Exit에다가 드래그를 놓아주면 **Action Segue 메소드 이름**이 뜰것이다 이것을 클릭하면

첫번째 화면에 써준 코드와 연결이 되면서 Unwind 기능을 하게 된다

---

### Segue 데이터 교환

세그웨이를 통해 화면을 전환하면서 두 화면 간에 데이터를 서로 주고받고, 갱신하고, 무엇인가를 보여줄 수 있다.

**이러한 세그웨이의 데이터 교환과 관련해서 다음과 같이 UIViewController 에서는 2가지 메서드를 제공한다**

#### prepareForSegue -> 세그웨이 실행 전 준비

#### performSegueWithIdentifier -> 세그웨이 실행

---

### Segue Identifier

데이터를 교환하는 메서드를 수행할 때, 메서드가 어떤 세그웨이에 대해 일을 처리해야하는지 알아야 한다.

**이에 각 세그웨이 별로 이름을 이름을 정해주는 것이다**

하는 방법은 스토리보드에서 세그웨이를 선택한 다음, 우측 상단의 **Attributes Inspector** 안에 **Identifier**에다가 적절한 이름을 넣어 주면 된다

---

### prepareForSegue

prepareForSegue는 세그웨이가 실행되기 전 준비하는 메서드로서 **이동 전 화면의 ViewController**에서 작성

여기서 준비를 한더는 것은 다음과 같은 사항들을 정의해준다는 것이다.

- 어느 세그웨이가 실행될 때를 말하는 것인가? (어느 세그웨이)
- 해당 세그웨이가 실행되면 이동할 화면은 무엇인가? (어느 화면)
- 이동할 화면의 어느 데이터를 어떻게 변경할 것인가? (데이터 변경)

prepareForSegue만 정의해주고 버튼 클릭 등으로 세그웨이가 실행되면 바로 데이터 교환이 발생하게 된다.

따로 performSegueWithIdenifier를 할 필요가 없다.

**참고로 이때 세그웨이 데이터 교환에서 주의할 점은 이동할 화면의 IBOutlet 데이터를 바로 바꿔줄 수 없다는 점이다**

즉, 예를들어 말해보자면 이동할 화면(다음화면)의 Label Outlet의 텍스트 값을 이동 전 화면(이전화면)에서 가져온 텍스트 값으로 변경하고 싶을때, 바로 변경이 안된다는 말이다.

**이럴때는 중간다리 역활을 하는 property가 필요하다**

**이동할 화면에 다른 property를 만들어 세그웨이가 이를 변경하게 하고, 이동할 화면의 viewController 에서 IBOutler 데이터가 변경될 수 있도록 해준다**

---

### performSegueWithIdentifier

prepareForSegue로 다 기능 구현이 가능한데 왜 performSegueWithIdentifier가 필요한것일까??

**performSegueWithIdentifier는 원하는 임의의 순간에 prepareForSegue를 통해 세그웨이를 실행시키는 코드이다**

여기서 중요한 점은 바로 **원하는 임의의 순간에**라는 문장이다

즉, **세그웨이 시점을 통제할 수 있게 되는 것이다**

performSegueWithIdentifier는 주로 처음 화면이 테이블 뷰나 컬렉션 뷰 일때 사용하게 된다.

첫 화면의 특정 셀이나 아이템을 누르면 다음화면으로 세그웨이를 이용하여 관련 데이터를 보여주는 경우이다.

테이블뷰의 경우 didSelectRowAtIndexPath, 컬렉션 뷰의 경우 didSelectItemAtIndexPath 메서드를 사용해서 이를 구현한다.

그리고 바로 이 메서드들 안에서 performSegueWithIdentifier이 사용이 된다.

셀이나 아이템을 누르면 화면이 이동하는 것이다.

위 didSelectRowAtIndexPath 와 같은 메서드들은 사용자가 선택한 IndexPath를 인자값으로 갖고 오기 때문에 그대로 IndexPath를 활용할 수 있다는 장점도 있다

이와는 달리 그냥 prepareForSegue만을 사용한다면 tableView.indexPathForCell(cell: UITableViewCell)메서드를 사용해서 별도로 indexPath를 가져와야 하는 번거로움이 생긴다.

정리해서 말해보면 사용자가 셀이나 아이템을 선택하는 순간 바로 prepareForSegue에서 준비된 코드들이 실행되도록 하는 것이 바로 didSelectRowAtIndexPath 내의 preformSegueWithIdentifier 인 것이다.
