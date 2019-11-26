---
layout: post
title:  "Codable Summary"
date:   2019-11-26
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - Codable](https://www.edwith.org/boostcourse-ios/lecture/18732/)

- - -

### What is Encoding and Decoding ?

- - -

#### 인코딩 (Encoding)

- 인코딩은 정보의 형태나 형식을 표준화, 보안, 처리 속도 향상, 저장 공간 절약 등을 위해 다른 형태나 형식으로 변환하는 처리 혹은 그 처리 방식

- - -

#### 디코딩(Decoding)

- 디코딩은 인코딩의 반대 작업을 수행하는 것을 뜻함

- - -

#### 인코더(Encoder)

- 인코더는 부호화를 수행하는 장치나 회로, 컴퓨터 소프트웨어, 알고리즘을 뜻한다

- - -

### What is Codable ? 

- 스위프트 4 버전에서는 스위프트의 인스턴스를 다른 데이터 형태로 변환하고 그 반대 역활을 수행하는 방법을 제공한다

    - 스위프트의 인스턴스를 다른 데이터 형태로 변환할 수 있는 기능을 Encodable 프로토콜로 표현하였다
    
    - Encodable의 반대 역활을 할 수 있는 기능을 Decodable로 표현하였다
    
    - `그 둘을 합한 타입을 Codable로 정의`
    
```swift

typealias Codable = Decodable & Encodable

```

- Codable은 스위프트 4 버전에서 처음 소개한 프로토콜이다

- Codable은 다양한  상황에서 사용할 수 있다

    - 예를 들어 JSON 형식으로 서버와 애플리케이션이 통신한다면 Codable 프로토콜을 이용해 편리하게 인코딩 및 디코딩 할 수 있다
    
![EncodingAndDecodingImg](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EncodingAndDecodingImg.png?raw=true)

- `Decodable : 스위프트 타입의 인스턴스로 디코딩 할 수 있는 프로토콜`

- `Encodable : 스위프트 타입의 인스턴스를 인코딩 할 수 있는 프로토콜`

- - -

### Example

- Codable

    - Coordinate 타입과 Landmark 타입의 인스턴스를 다른 데이터 형식으로 변환하고 싶은 경우에 Codable 프로토콜을 준수하도록 하면 된다
    
    - Codable 타입의 프로퍼티는 모두 Codable 프로토콜을 준수하는 타입이어야 한다
    
    - 스위프트의 기본 타입은 대부분 Codable 프로토콜을 준수한다

![CodableExampleImg](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/CodableExampleImg.png?raw=true)

- Codingkey

    - 자주 사용하게 될 JSON 형태의 데이터로 상호 변환하고자 할 때는 기본적으로 인코딩/디코딩 할 JSON 타입의 키와 애플리케이션의 사용자정의 프로퍼티가 일치해야 한다
    
    - 만약 JSON의 키 이름을 구조체 프로퍼티의 이름과 다르게 표현하려면 타입 내부에 String 타입의 원시값을 갖는 CodingKeys라는 이름의 열거형을 선언하고 CodingKey 프로토콜을 준수하도록 하면 된다
    
    - CodingKeys 열거형 케이스의 이름은 해당 프로퍼티의 이름과 일치해야 한다
    
    - 그리고 프로퍼티의 열거형 케이스의 값으로 매칭할 JSON 타입의 키를 할당하면 된다
    
    - 만약 JSON 타입의 키와 프로퍼티 이름이 일치한다면 값을 할당하지 않아도 무방하다

![CodingKeyExampleImg](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/CodingKeyExampleImg.png?raw=true)