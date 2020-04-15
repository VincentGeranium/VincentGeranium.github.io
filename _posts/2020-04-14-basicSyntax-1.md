---
layout: post
title:  "기본 문법 공부(옵셔널 체이닝과 빠른종료 - 옵셔널 체이닝)"
date:   2020-04-14
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Optional Chaining Example - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-15-optionalChainingExample-1.playground)

- [Optional Chaining Example - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-15-optionalChainingExample-2.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/OptionalChaining.html)

- - -

### 옵셔널 체이닝 (Optional Chaining)

- 옵셔널 체이닝은 옵셔널에 속해 있는 nil일지도 모르는 프로퍼티, 메서드, 서브스크립션 등을 가져오거나 호출할 때 사용할 수 있는 일련의 과정이다.

- 옵셔널에 값이 있다면 프로퍼티, 메서드, 서브스크립트 등을 호출할 수 있고, 옵셔널이 nil이라면 프로퍼티, 메서드, 서브스크립트 등은 nil을 반환한다.

- 즉, 옵셔널을 반복 사용하여 옵셔널이 자전거 체인처럼 서로 꼬리를 물고 있는 모양이기 때문에 옵셔널 체이닝이라고 부른다.

- 자전거 체인에서 한 칸이라도 없거나 고장나면 체인 전체가 동작하지 않듯이 중첩된 옵셔널 중 하나라도 값이 존재하지 않는다면 결과적으로 nil을 반환한다.

- 옵셔널 체이닝은 프로퍼티나 메서드 또는 서브스크립트를 호출하고 싶은 옵셔널 변수나 상수 뒤에 물음표(?)를 붙여 표현한다.

- 옵셔널이 nil이 아니라면 정상적으로 호출될 것이고, nil이라면 결괏값으로 nil을 반환할 것이다.

- 결과적으로 nil이 반환될 가능성이 있으므로 옵셔널 체이닝의 반환된 값은 항상 옵셔널이다.

- - -

### 사람의 주소 정보 표현 설계와 함께 알아보는 옵셔널 체이닝

<img width="1058" alt="optionalChainingImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-1.png?raw=true" title="optionalChainingImage">

- 사람의 정보를 표현하기 위해 Person 클래스를 설계했다.

    - Person 클래스는 이름이 있으며 주소를 옵셔널로 갖는다.
    
- 주소 정보는 Address 구조체로 설계했다.

    - 주소에는 광역시/도, 시/군/구, 도로명이 필수며, 건물 정보가 있거나 건물이 아니면 싱세주소를 기재할 수 있도록 했다.
    
- 건물 정보는 Building 클래스로 설계했다.

    - 건물은 이름이 있으며, 호실의 정보를 갖는다
    
- 호실 정보는 Room 클래스로 설계했다.

    - 각 호실은 번호를 갖는다.
    
<img width="760" alt="optionalChainingImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-2.png?raw=true" title="optionalChainingImage">

- 위의 코드는 jun 인스턴스를 생성한 코드이다.

<img width="1058" alt="optionalChainingImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-3.png?raw=true" title="optionalChainingImage">

- jun이 사는 호실 번호를 알고싶다. 옵셔널 체이닝과 강제 추출을 사용하여 프로퍼티에 접근해보면 위와 같은 결과를 볼 수 있다.

- jun에는 아직 주소, 건물, 호실 정보가 없다.

- junRoomViaChaining 상수에는 호실 번호를 할당하려고 옵셔널 체이닝을 사용하면 jun의 address 프로퍼티가 nil이므로 옵셔널 체이닝 도중 nil이 반환된다.

- junRoomViaOptionalUnwrapping 상수에 호실 번호를 할당할 때는 강제 추출을 시도했기 때문에 nil인 address 프로퍼티에 접근하려 할 때 런타임 오류가 발생한다.

- - -

### 옵셔널 체이닝과 강제 추출 동작의 흐름

![optionalChainingImage-4](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-4.png?raw=true)

- - -

### 옵셔널 바인딩을 사용하여 Jun이 사는 호실 정보 가져오기

<img width="1058" alt="optionalChainingImage-5" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-5.png?raw=true" title="optionalChainingImage">

- - -

### 옵셔널 체이닝의 사용하여 Jun이 사는 호실 정보 가져오기

<img width="1058" alt="optionalChainingImage-6" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-6.png?raw=true" title="optionalChainingImage">

- '옵셔널 바인딩을 사용하여 Jun이 사는 호실 정보 가져오기'의 코드와 '옵셔널 체이닝의 사용하여 Jun이 사는 호실 정보 가져오기' 코드는 완전히 같은 결과를 내놓지만, 코드의 간결함과 분량은 꽤 차이가 크다.

- 그런데 여기서 중요하게 봐야 할 점은 '옵셔널 체이닝의 사용하여 Jun이 사는 호실 정보 가져오기'의 옵셔널 체이닝 코드가 옵셔널 바인딩 기능과 결합했다는 점이다.

    - 옵셔널 체이닝의 결괏값은 옵셔널 값이기 때문에 옵셔널 바인딩과 결합할 수 있는 것이다.
    
    - 이렇게 옵셔널 체이닝과 옵셔널 바인딩은 좋은 조합을 이룬다.
    
        - 옵셔널 바인딩을 통해 jun.address?.building?.room?.number의 결괏값이 nil이 아님을 확인하는 동시에 roomNumber라는 상수로 받아올 수 있다.
        
- 위의 그림 속 코드에서 옵셔널 체이닝을 실행할 때, jun의 address가 nil이기 때문에 더 이상 다음 체인의 building을 체크하지 않고 nil을 반환한다.

- - -

### 옵셔널 체이닝 동작 흐름

![optionalChainingImage-7](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-7.png?raw=true)

- - -

### address가 존재할 때 옵셔널 체이닝 동작의 흐름

![optionalChainingImage-8](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-8.png?raw=true)

- 만약 address의 값이 있었다면 위와 같이 다음 체인인 building을 체크해보았을 것이다.

- 이처럼 옵셔널 체이닝을 통해 한 단계뿐만 아니라 여러 단계로 복잡하게 중첩된 옵셔널 프로퍼티나 메서드 등에 매번 nil을 체크를 하지 않아도 손쉽게 접근할 수 있다.

- 또한 옵셔널 체이닝을 통해 값을 받아오기만 하는 것이 아니라 반대로 값을 할당해줄 수도 있다.

- - -

### 옵셔널 체이닝을 통한 값 할당 시도

<img width="1058" alt="optionalChainingImage-9" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-9.png?raw=true" title="optionalChainingImage">

- - -

<img width="1058" alt="optionalChainingImage-10" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-10.png?raw=true" title="optionalChainingImage">

- 위의 코드처럼 '옵셔널 체이닝의 사용하여 Jun이 사는 호실 정보 가져오기'의 코드 바로 아래에 '옵셔널 체이닝을 통한 값 할당 시도'의 코드를 작성하면, 아직 jun의 address 프로퍼티가 없으며 그 하위의 building 프로퍼티도 room 프로퍼티도 없다.

- 그렇기 때문에 '옵셔널 체이닝을 통한 값 할당 시도'의 옵셔널 체이닝은 동작 도중에 중지될 것이다.

    - number 프로퍼티는 존재조차 하지 않았으므로 707이 할당되지 않는 것은 물론이다.
    
- - -

### 옵셔널 체이닝을 통한 값 할당

<img width="1058" alt="optionalChainingImage-11" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-11.png?raw=true" title="optionalChainingImage">

- 위의 코드를 통해 옵셔널 체인에 존재하는 프로퍼티를 실제로 할당해준 후 옵셔널 체이닝을 통해 값이 정상적으로 반환되는 것을 확인할 수 있다.

- 옵셔널 체이닝을 통해 메서드와 서브스크립트 호출도 가능하다.

    - 서브스크립트는 인덱스를 통해 값을 넣고 빼올 수 있는 기능이다.
    
- - -

### 옵셔널 체이닝을 통한 메서드 호출

<img width="1058" alt="optionalChainingImage-12" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-12.png?raw=true" title="optionalChainingImage">

- - -

### 옵셔널 체이닝을 통한 서브스크립트 호출

<img width="1058" alt="optionalChainingImage-13" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-13.png?raw=true" title="optionalChainingImage">

- 서브스크립트를 가장 많이 사용하는 곳은 Array와 Dictionary이다.

- 옵셔널의 서브스크립트를 사용하고자 할 때는 대괄호([])보다 앞에 물음표(?)를 표기해주어야 한다.

- 이는 서브스크립트 외에도 언제나 옵셔널 체이닝을 사용할 때의 규칙이다.