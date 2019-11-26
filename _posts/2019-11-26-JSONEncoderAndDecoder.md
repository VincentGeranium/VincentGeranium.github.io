---
layout: post
title:  "JSONEncoder And JSONDecoder Summary"
date:   2019-11-26
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - Codable](https://www.edwith.org/boostcourse-ios/lecture/20145/)

- - -

### What is JSONEncoder And JSONDecoder ?

- 스위프트 4 버전 이전에는 JSONSerialization을 사용해 JSON 타입의 데이터를 생성했다

- 그러나 스위프트 4 버전부터 JSONEncoder / JSONDecoder가 Codable 프로토콜을 지원하기 때문에 JSONEncoder / JSONDecoder와 Codable 프로토콜을 이용해 손쉽게 JSON 형식으로 인코딩 및 디코딩 할 수 있다

    - 즉, JSONEncoder 및 JSONDecoder를 활용하여 스위프트 타입의 인스턴스를 JSON 데이터로 인코딩, JSON 데이터에서 스위프트 타입의 인스턴스로 디코딩 할 수 있다.
    
- - -

### JSONEncoder

- Codable 프로토콜을 준수하는 GroceryProduct 구조체의 인스턴스를 JSON 데이터로 인코딩하는 방법

![JSONEncoderImg](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/JSONEncoderImg.png?raw=true)

- - -

### JSONDecoder

- JSON 데이터를 Codable 프로토콜을 준수하는 GroceryProduct 구조체의 인스턴스로 디코딩하는 방법

![JSONDecoderImg](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/JSONDecoderImg.png?raw=true)

- - -

#### Example Code

[ExampleCode](https://github.com/VincentGeranium/Swift-Study/blob/master/2019-11-26-JSONEncoderExample.playground/Contents.swift)