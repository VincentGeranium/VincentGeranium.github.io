---
layout: post
title:  "Swift - Array[1]"
date:   2019-03-15
categories: Swift
---

# Swift Array 공부

- **Playground File을 보고 싶으신 분은 [Github](https://github.com/VincentGeranium/Swift-Study)**
- **파일명 : 2019-03-15-Swfit-Study-Syntax-10.playground**

```
// 배열 Array

// 가변 객체와 불변 객체
// Mutable and Immutable

var numberVariable = [1,2,3]
numberVariable = []

let numberConstant = [1,2,3]
// numberConstant = [] // error


// 배열 타입 Array Type
var numberArray = [1,2,3,4]
numberArray = []

//let noInArray = [] // error: empty collection literal reuqires an explicti type

let noInArray: [String] = [] // 빈 배열로 정의시 타입을 명시해야 함


// 배열 초기화 Initialize
let initArray1: Array<String> = ["where","are","you"]
let initArray2: [String] = ["where","are","you"]
let initArray3 = ["where","are","you"]
let initArray4 = Array<String>(repeating: "Love You", count: 5)
//let initArray5 = ["apple", 18.5, 4] // error

// 배열 갯수 세기
let nameOfDrink: [String] = ["SOJU", "Water", "Coke"]
let countOfDrink = nameOfDrink.count

if !nameOfDrink.isEmpty {
    print("\(nameOfDrink) is Very good")
} else {
    print("empty array")
}

// 배열 인덱스 값 검색

nameOfDrink[0]
nameOfDrink[1]
nameOfDrink[2]
//nameOfDrink[4] // error: Index out of range
//nameOfDrink[123] // error: Index out of range

nameOfDrink[nameOfDrink.startIndex]
//nameOfDrink[nameOfDrink.endIndex] // error: Index out of range
nameOfDrink[nameOfDrink.endIndex - 1]

// 중요 !!
nameOfDrink.startIndex == 0
nameOfDrink.endIndex - 1 == 2
nameOfDrink.endIndex == 3


// 검색
let getAlphabet = ["A", "B", "C", "D", "E"]

if getAlphabet.contains("A") {
    print("getAlphabet Array hava A")
}

if getAlphabet.contains(where: { str -> Bool in
    // code
    return str == "A"
}) {
    print("getAlphabet Array hava A")
}

if let index = getAlphabet.firstIndex(of: "D") {
    print("index of D is \(index)")
}

//let index1 = getAlphabet.firstIndex(of: "D") // getAlphabet의 "D"의 index 를 뽑아줌
//print(index1) // Optional(3)으로 나옴

//let index2 = getAlphabet.firstIndex(of: "Q") // getAlphabet의 "Q"가 없으므로 nil 값을 돌려줌
//print(index2) // nil 값이 나옴

// 배열에 값 추가

//var alphabetList: [String] = [] // 빈 배열 생성
//var alphabetList: Array<String> = [] // 빈 배열 생성
//var alphabetList = [String]() // 빈 배열 생성

//var listOfAlphabet: [String] = []
var listOfAlphabet = ["A"]
listOfAlphabet.append("B")
listOfAlphabet += ["C"]
listOfAlphabet

var listOfAlphabet2 = ["Q", "W", "E"]
listOfAlphabet + listOfAlphabet2

//listOfAlphabet.append(5.0) // error: cannot convert value of type, 타입이 맞지 않아 에러
//listOfAlphabet + 1 // error expected an argument list of type '(Int,Int)'

listOfAlphabet.insert("S", at: 0) // index 0번째 자리에 "S" 삽입
listOfAlphabet.insert("F", at: 3) // index 3번째 자리에 "F" 삽입
listOfAlphabet

// 배열 값의 교환

var newListOfAlphabet = ["A", "B", "C"]
newListOfAlphabet[0] = "Z" // index 0번째 자리에 "A" 와 "Z" 교환
newListOfAlphabet

newListOfAlphabet = ["A", "B", "C"]


newListOfAlphabet.endIndex
newListOfAlphabet.endIndex.advanced(by: -1)
newListOfAlphabet.endIndex.advanced(by: +1)

newListOfAlphabet[newListOfAlphabet.startIndex ..< newListOfAlphabet.endIndex.advanced(by: -1)] = ["X", "Y"]
newListOfAlphabet

1...5 // 1 ~ 5
1..<5 // 1 ~ 4
1... // 1 ~

newListOfAlphabet = ["A", "B", "C", "D", "E", "F"]
newListOfAlphabet[2...] = ["Q", "W", "E", "R"]
newListOfAlphabet

newListOfAlphabet[2...] = ["Q", "W"]
newListOfAlphabet

// 배열 값의 제거

var alphabet: [String] = ["A", "B", "C", "D", "E"]

let removeAlphavet = alphabet.remove(at: 0)
alphabet

alphabet.removeAll()
alphabet.removeAll(keepingCapacity: true)

// index 찾아 지우기
alphabet = ["A", "B", "C", "D", "E"]

if let indexD = alphabet.firstIndex(of: "D") {
    alphabet.remove(at: indexD)
}
alphabet
```
