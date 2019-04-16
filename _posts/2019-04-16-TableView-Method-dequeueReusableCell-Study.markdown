---
layout: post
title:  "TableView Method dequeueReusableCell 공부 - 190416"
date:   2019-04-16
categories: Swift, iOS
---

# dequeueReusableCell Method Study

오늘은 지난번에 말했던 것 처럼 dequeueReusableCell Method에 대해 알아보는 시간입니다!!

에효,, 오늘도 먼 길을 가야 할듯한 느낌이,,,

![destinationImg](https://user-images.githubusercontent.com/42841888/56182229-1b1a4c00-604c-11e9-8e4f-d254f8883eb9.png)

그래도 화이팅 해서 가봅시다!!

먼저 dequeueReusableCell 이 뭔지 까먹엇을 수도 있으니 우리 한번 봐 볼까요??

![dequeueImage](https://user-images.githubusercontent.com/42841888/56182469-5d905880-604d-11e9-8c50-e72d97704c70.png)

위의 그림에 나와있죠?? 반가워,, 다시만났네,,, ㅋㅋㅋ

일단 뭐든지 궁굼하고 모르겠으면 Documentation이나 Quick Help가 최곱니다!!

그럼 이 메소드가 어떤식으로 정의되었는지 메소드의 원형을 알아볼까요??

```
func dequeueReusableCell(withIdentifier identifier: String, for indexPath: IndexPath) -> UITableViewCell
```

벌써부터 현기증이나네요,,,

이 메소드는 2개의 파라미터를 받는데 identifier 와 indexPath를 받네요

그리고 반환으로는 UITableViewCell을 반환합니다

자 그럼 하나씩 알아봅시다~

dequeueReusableCell(withIdentifier:for:)의 summary를 보면 다음과 같이 나와있어요

**지정된 재사용 ID에 대한 재사용 가능한 테이블 뷰 셀 객체를 반환하고, 이를 테이블에 추가 합니다** 라고 나와있어요

오호?! 뭔소리지??

![qustionImg](https://user-images.githubusercontent.com/42841888/56182798-c1ffe780-604e-11e9-864f-25e6b76ea46d.png)

차근 차근 뜯어 먹어봅시다

위의 그림에서 **let cell = tableView.dequeueReusableCell(withIdentifier:"List", for:indexPath)**

우리가 사용한 코드는 위와 같은데 **지정된 ID(식별자)라고 하는 것은 withIdentifier**가 되겠죠?!

그럼 정확하게 이 identifier(ID)를 주면, 어떤일을 하는지 알아야지 조금 더 이해가 갈것같아요, 어떤일을 할까요??

역시 모를때는 Quick Help를 보면 되요ㅋㅋ

이 메소드의 파라미터인 identifier는 다음과 같이 나와있어요

**재사용 할 셀 객체를 식별하는 문자열입니다, 이 매개변수는 nil이 아니어야 합니다**

아~ 이 identifier는 재사용할 객체를 나타내는 문자열이군요 !!

그리고 이건 꼭 지켜줘야 해요 **nil이 아니어야 한다는 점**

다시 쉽게 정리해보면 **우리가 지정해주는 string형 identifier는 재사용할 객체를 나타내주는 것이네요**

이번엔 두번째 파라미터인 for에 대해 알아봅시다

for를 보면 Quick Help에는 다음과 같이 나와있어요

**셀의 위치를 지정하는 인덱스 경로입니다. 데이터 소스는 셀에 대한 요청이 있을 때 이 정보를 수신하며 이를 전달해야 합니다. 이 방법은 인덱스 경로를 사용하여 테이블 뷰에서 셀의 위치를 기반으로 추가 구성을 수행합니다**

우와~ 정말 길고 뭔말인지 모르겟죠??

저도 그래요 ㅋㅋ

그럼 같이 알아봐요!!

일단 위의 그림을 봐보면 for에 indexPath가 들어가 있어요

이 indexPath는 어디서 온걸까요?? 아,,,

identifier는 우리가 직접 지정해준걸로 알고 있는데 indexPath는 뭐지??

아래 그림을 한번 봐 볼까요??

![indexPathImg2](https://user-images.githubusercontent.com/42841888/56184041-aea34b00-6053-11e9-86e4-522ece6eab1e.png)

그림에 나온것처럼 indexPath는 tableView 메소드 안에 있었어요

tableView 메소드는 파라미터로 UITableView와 IndexPath를 받네요?!!

즉, tableView 메소드에서 파라미터로 받은 IndexPath의 이름은 indexPath라고 해준거에요

**그것을 당연히 이 메소드 안에서 사용이 가능하겟죠?!**

오 조금은 dequeueReusableCell에 대해 알꺼같기도 하죠??

예를들어서 이야기를 이어나가면 이해가 조금 더 될꺼 같아요

만약에 내가 2500개의 항목(엔트리)를 가지는 테이블을 만들었다고 생각해봐요

그럼 테이블을 만들 때, 이 2500개의 엔트리를 셀마다 만들어야 할 것이고,

이 2500개의 테이블 뷰 셀에 대해 메모리 할당이 이루어지게 될거에요.

그럼 10만개면?? ㅇㅇ?? 10만개면 정말 많은 메모리가 들꺼에요

**이를 방지하기 위해 나온것이 바로 dequeueReusableCell 입니다!!**

이 dequeueReusableCell의 목적은 **메모리를 재사용해 메모리를 줄이자! 입니다**

그럼 실제 예를 한번 더 들어서 설명해볼게요

만약에 제가 **화면**에 테이블 뷰 셀을 10개를 볼 수 있다고 가정할게요

**현재 화면**이라는 점을 꼭 인지하고 예시를 들어봐야지 이해가 되니까 이점 기억하시고~

다시 본론으로 돌아와 나머지 뷰들은 스크롤해서 볼 수 있다고 생각해봐요

그럼, 이 테이블 뷰는 테이블 높이와 셀의 높이를 기반으로 정확하게 셀 수를 생성해요(10개를 말이죠 예를 들었으니까~)

그럼 지금 시점에서 메모리 할당은 10개의 셀에 대한 메모리 할당만 이루어지면 되는것이에요

근데 저는 밑에 셀도 보고싶어서 뷰를 스크롤 해봤어요

계속 동일한 셀이 사용되기는 하는데, **DataSource**를 기반으로 셀 내용이 바뀌게 되요

셀이 스크롤 되어 화면 밖으로 밀려서 나가게되면, 이 셀은 reuse poll에 들어가게 되고, 우리가 dequeueReusableCell을 호출할 때 테이블 셀에 의해 반환이 되죠.

아직도 조금 어렵다면 직접 코드로 구현해보고 직접 봐가면서 이해를 해보도록 해요!!

오늘은 여기까지~
