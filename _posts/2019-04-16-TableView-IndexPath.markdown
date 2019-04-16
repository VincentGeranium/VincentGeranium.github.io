---
layout: post
title:  "TableView 코드 중 indexPath에 대해 공부"
date:   2019-04-16
categories: Swift, iOS
---

# IndexPath

오늘은 TableView 코드에 나와있는 IndexPath에 대해 간단하게 알아보려고 해요

왜냐하면 제가 모르니까요??,,,,,,

일단 이 코드를 볼까요??

```
override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "reuseIdentifier", for: indexPath)
        
        cell.textLabel?.text = arr[indexPath.row]

        return cell
    }
```

엄청 많은 코드들이,,,,

우리는 오늘 알아보려고 하는게 일단 indexPath에 대해 알아보는거니까 나머지 코드는 제껴두고!!

일단 indexPath가 어디에 있나 봐볼까요??

바로 let cell = tableView.dequeueReusableCell(withIdentifier: "reuseIdentifier", for: **indexPath**)

여기에 나와있네요?!

찾앗다 요놈!!

![img](https://user-images.githubusercontent.com/42841888/56176316-b2c07000-6035-11e9-80d4-ffed3ed0baa8.png)

그런데 그 밑에도 보면 우리가 지금 코드에는 보이지는 않지만

**arr이라는 배열**을 미리 제가 만들어 놨어요 전체 코드는 밑에 넣어둘게요 한번 봐 보세요~

다시 본론으로 들어가 

코드를 보면 아래와 같이 또 **indexPaht** 가 나와요

```
cell.textLabel?.text = arr[indexPaht.row]
```

도데체 indexPath가 뭐길래?!

![zzangguImage](https://user-images.githubusercontent.com/42841888/56176612-a4bf1f00-6036-11e9-80af-6ae8a22d1334.png)

일단 이코드를 해석을 해야 하는데 이 코드 블럭은 이렇게 해석하면 되요

ID가 reuseIdentifier인 cell의 textLable의 text에 arr[indexPaht.row]를 넣어주세요

하는 거죠

그럼 이제 우리가 알고 싶어했고 알아야할 indexPath를 알아야 indexPath.row도 알 수 있겠죠??

Quick Help의 summary를 보면 **indexPath는 tableView의 행을 식별하는 인덱스 경로** 라고 나와요

그럼 indexPath.row는 그 경로 행에 위치를 인덱스로 가지는 arr의 원소를 textLabel에 써주겠다는 말이겠네요??

아하!! 정말 이해가 하나도 안가요!!

그리고 이런 궁굼증도 생기지 않나요?? 

indexPath.row를 가져왔는데 그게 arr의 인덱스로 들어가면 그게 나오는건가??

![questionMark](https://user-images.githubusercontent.com/42841888/56176942-ca98f380-6037-11e9-94bc-4b39d1bcd343.png)

그러면 일단 arr[indexPath.row]가 어떻게 arr의 원소에 접근하는지 알아봐야겠네요

아래의 그림을 봐 볼까요??

![codeImg](https://user-images.githubusercontent.com/42841888/56177299-15673b00-6039-11e9-96d6-020ec728dbc2.png)

이 그림은 제가 미리 만들어둔 코드에요 

그런데 cell.textLabel?.text = arr[indexPaht.row] 아래에
**print("Function Call")** 로 지금 테이블 뷰 결과물을 만들때 이 함수가 몇번이나 불리우는지 출력을 해봤어요

그림을 보니 5번이 나오네요?!

그림에서 보면 제가 따로 배열을 만들어 그 안에 5개의 원소들을 넣어두었거든요

오호?! 그럼 우리가 이제 알 수 있는건 배열 즉, arr에 있는 원소의 개수만큼 셀을 그려야 하니까 5번이 나오는구나

하고 알 수 있어요

그러면 위의 메소드가 셀의 갯수만큼 호출된다는 것은 알았으니 indexPath가 뭔지 print 해봅시다

![indexCall](https://user-images.githubusercontent.com/42841888/56177562-0f258e80-603a-11e9-9267-5de2a59bdaa0.png)

어?! 값이 2개가 나와요

그럼 우리가 알고 싶어하는 indexPath.row를 찍어봅시다!!

![indexPathRowCall](https://user-images.githubusercontent.com/42841888/56177702-89561300-603a-11e9-81a5-7d902d51d947.png)

위의 그림에서 보는 바와 같이 **0,1,2,3,4** 로 나와요 

그럼 indexPath.row는 indexPath의 두번째에 위치한 값을 가져온거라는 답이 나오죠!!

조금 더 쉽게 말해 **indexPath는 [?.row]** 가 되겠네요 ㅋㅋㅋ

점점 답에 가까워지고 있어 기분이 좋아져요!! ㅋㅋ

자 다시 보면 indexPath.row의 값을 가져와보니 우리가 아까 그림에서 봤던것처럼 0,1,2,3,4 잖아요

그럼 arr[indexPath.row]는 뭘까요??

방금 전에 indexPath는 [?,row]로 되어있다고 했는데, 첫번째 값은??

**우리가 본 그림에서는 모두 0 이였어요**

이것은 바로 **section**을 의미해요, 전체 코드에서 보면 알듯이 우리는 섹션을 하나만 만들었었어요

그러면 [0,0], [0,1], ... [0,4] 는 무엇일지 알겠죠??

바로 0번째 섹션의 1번째 행, 0번째 섹션의 2번째 행,..., 0번째 섹션의 4번째 행

이렇게 된다는 것을 말이에요!!

아하 그럼 이렇게 보면 더 쉽겠네요!! **indexPath는 [section,row]로 이루어져 있는 행을 식별하는 상대적인 경로** 이렇게 말이에요

후,,, 먼길이였어요 ㅠㅠ 그래도 열심히 찾아보고 해석해보니 그나마 머리에 조금 들어오는듯 해요

오늘은 여기까지 다음에는 다른 코드 해석을 해봅시다!!






