---
layout: post
title:  "JSON 데이터 형식과 Swift 형식으로의 변경"
date:   2020-02-11
categories: iOS, Swift
---

edwith의 iOS 강의 중 서버에서 데이터를 받아와 테이블 뷰에 넣어주는 [강의](https://www.edwith.org/boostcourse-ios/lecture/16915/)를 듣고 있는 중

강의의 내용 중에 JSON 형식을 Swift에서 사용 가능한 형식으로 바꾸는 것에 대하여 설명하는 부분을 정리하여 놔두면 나중에 도움이 될 것 같아서 정리를 해 보았다

- - -

### 받아 올 데이터의 형식

![dataFormatImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/dataFormatImage-1.png?raw=true)

위의 그림은 서버로부터 받아 올 데이터 형식이다.

데이터를 받아 오기 전 가장 먼저 해야하는 것이 있는데, 먼저 받아 올 데이터의 형식을 파악해야 한다.

서버로 부터 받아 올 데이터의 형식을 파악해야 내가 어떻게 JSON 형식을 Swift에서 사용이 가능한 형식으로 바꾸어 사용 할지 알 수 있기 때문이다.

- - -

### 데이터 형식 파악하기

![dataFormatImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/dataFormatImage-2.png?raw=true)

- 데이터 오브젝트 안에 `results`라는 `key`가 있고 그 안에 데이터 들이 담겨 있는데 `Array`형식으로 정보가 쭉 담겨져 있다.

- `results`안에있는 하나의 데이터 정보를 보게되면 `name` 이라는 오브젝트와 `email`, `picture`를 가지고 있다

- `name` 오브젝트 안에는

    - title, first, last라는 오브젝트로 나뉘어져 있으며 각각의 오브젝트에 맞는 정보가 string 값으로 들어가 있다

- `email` 오브젝트 안에는

    - 정보가 string 값으로 들어가 있다
    
- `picture` 오브젝트 안에는

    - large, medium, thumbnail라는 오브젝트로 나뉘어져 있으며 각각의 오브젝트에 맞는 정보가 string 값으로 들어가 있다
    
- - -

### Swift Type로 변환

![TransferSwiftTypeImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TransferSwiftTypeImage-1.png?raw=true)

- results 키를 가지고는 오브젝트 하나를 만들어 준다

- Friend라는 이름으로 그 안에 Name, Picture는 type로 만들어주었고 email은 그냥 받아 올 수 있도록 만들어 놨다

    - 즉 Friend 안에 name, email, picture 정보가 들어오게 된다
    
- - -

### 데이터의 사용

- JSON 데이터를 Swift 에서 사용 가능한 형식으로 바꾸고 그 데이터들을 받아와 JSON Decoding을 통하여 자신이 원하는 곳에 데이터들을 사용 할 수 있도록 만들면 된다.