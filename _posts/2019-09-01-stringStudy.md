---
layout: post
title:  "String 다루기"
date:   2019-09-01
categories: iOS, Swift
---

## String 다루기

---

## Extended Grapheme Clusters (확장적 문자소 집합)

- Grapheme : 문자소(의미를 나타내는 최소 문자 단위)

- Swift에서 하나의 Character는 `Single Extended Grapheme Clusters`를 나타냄

    - `Extended Grapheme Clusters`라는 것은 사람이 읽을 수 있는 하나의 문자를 지칭한다
    
```swift
let precomposed: Character = "\u{D55C}" // 한
let decomposed: Character = "\u{1112}\u{1161}\u{11AB}" //ㅎ,ㅏ,ㄴ 

print(precomposed) // 한
print(decomposed) // 한
```

- `decomposed`는 Character 타입에 3개의 `scala`가 들어간다.

    - `scala` = 최소 의미를 담은 `Character 값` 을 의미

        - ex. \u{1112}

- 즉, `Exteded Grapheme Clusters`에서는 `1 scala = 1 Character` 가 `아니고` `1 Character = 1개 혹은 여러개의 scala` 가 `되는 것이다.`

- **인덱스를 통해서 String를 다룰 수 없는 이유가 여기서 나타난다.**

    - **각각의 `Character`가 `여러개`의 `scala` 값을 `가질 수 있기 때문에` `동일한 메모리`로 `한정된 저장공간`을 `가지기 어렵다`**
    
- 그렇기 때문에 `String`을 만들 때 `Character 별로 동일한 크기의 메모리를 할당할 수 없고`, 이는 `인덱스`를 `통한 접근을 불가능`하게 만든다

---

```
Swift에서 채택한 Extended Grapheme Clusters는 다양한 언어를 직관적으로 표시할 수 있게 도와준다

하지만

Extended Grapheme Clusters는 서로 다른 크기의 Character를 만들기 때문에 String[Int]를 통한

String의 개별 Character로의 접근은 불가능하다.
```

---

## Swift의 String 접근하기