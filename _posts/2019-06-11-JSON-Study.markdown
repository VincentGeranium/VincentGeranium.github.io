---
layout: post
title:  "JSON에 대한 개념 정리 - 2"
date:   2019-06-11
categories: iOS, Swift
---

### 참고자료

이 포스트는 Zedd님의 블로그 글 중 `왕초보를 위한 JSON Parsing - 2(JSON 파싱)`을 읽고, 참고하여 작성한 포스트 임을 미리 밝힙니다

아래의 링크를 누르시면 Zedd님의 블로그로 이동 합니다.

[Zedd님의 왕초보를 위한 JSON Parsing - 2(JSON 파싱)](https://zeddios.tistory.com/148?category=685736)

---

# JSON에 대한 개념 정리 - 2

![jsonImage](https://user-images.githubusercontent.com/42841888/59244098-00301680-8c4e-11e9-9922-879ff1f2a35a.png)

위의 그림에서 보이듯이

- 큰 객체 하나가 들어왔다 -> `{ }`로 전체가 묶여있음

- **JSON에서 객체는 -> name - value 쌍**

- "person" : [] 이렇게 쌍으로 이루어져있다 -> "person" = name, [] = value
    - 배열 `[ ]` 안에 여러 쌍이 들어가 있다
    
- `"person" : [ ]` -> person이라는 name의 짝인 value `[ ]` 이 배열 안에 `{ }, { }` 객체 두개가 들어 있다

- 객체 = name - value의 쌍 -> 중요!!

---

# JSON 파싱

JSON 파싱으로 하려면 JSON안에 있는 **내용**을 가져와야 한다

![JSONimage2](https://user-images.githubusercontent.com/42841888/59244120-10e08c80-8c4e-11e9-8b45-7c6ccd0166b3.png)

**위 사진은 맨 위의 사진에서 나오는 person.json과는 다른 데이터임**

- .json 파일 내에서 `내용`만 가져온다고 JSON 파싱을 진행할 수 없다

## .json에서 가져온 "내용"을 "데이터화"

**Swift에서 제공하는 JSONSerialization**을 사용해야 한다

- JSONSerialization는 파라미터로 data를 받게된다 -> 이 data는 Data 타입
    - 위의 그림을 보면 person.json을 통해 받은 String타입인 person.json의 `내용`을 `Data`타입으로 바꿔줘야 한다
    
## JSONSerialization을 사용하여 Foundation 객체화

![funcimage1](https://user-images.githubusercontent.com/42841888/59244186-65840780-8c4e-11e9-8d96-8e04eafa1692.png)

![funcimage2](https://user-images.githubusercontent.com/42841888/59244201-7af93180-8c4e-11e9-8c4a-3b0719c47a73.png)

JSONSerialization에는 jsonObject라는 메소드가 있다

- jsonObjcet 메소드 = **json 데이터를 파라미터로 받아 Swift에서 가공/처리 할 수 있는 Foundation 객체로 만들어주는 역활**

## 주의할점

- JSONSerialization에서 jsonObject 메소드를 사용하여 Foundation 객체로 만들어줄 때 

```
let json = try! JSONSerialization.jsonObject(with: data, options: []) as! [String : Any]
```

- as! [String : Any]에서 주의해야 한다

- as 는 타입캐스팅을 해주는 예약어

- [String : Any], 즉 Dictionary의 Key는 String타입, value는 아무거나 들어올 수 있다고 말하는것

**즉, as 뒤에 올 타입은 파싱할 json 파일 형식과 맞아야 한다**

![JSONExamplimage](https://user-images.githubusercontent.com/42841888/59244098-00301680-8c4e-11e9-9922-879ff1f2a35a.png)

위의 그림을 보면 전체적인 구조를 요약해서 보면 **{"person":[{},{}]}**

`Swift타입으로 보자면 [String:Any]`

그런데 JSON은 위의 그림과 같은 구조로만 이루어져 있지 않다

![anotherJSON](https://user-images.githubusercontent.com/42841888/59244212-86e4f380-8c4e-11e9-95cf-8bc98e981b8e.png)

맨 위의 그림과는 다르게, 전체가 `[ ]` 배열로 묶여있다

위의 그림을 보면 전체적인 구조를 요약해서 보면 **[{},{},{}]** -> [String:Any]와는 다른 형태

**[{},{},{}]** -> `[[String:Any]]` 이렇게 가져와야 한다
