---
layout: post
title:  "Swift - Enumeration"
date:   2019-03-14
categories: Swift
---



# Swift 열거형 공부

- **Playground File을 보고 싶으신 분은 [Github](https://github.com/VincentGeranium/Swift-Study)**
- **파일명 : 2019-03-14-Swift-Study-Syntax-9.playground**

```
enum Nation {
    case korea
    case usa
    case france
    case greece
}


var nationList = Nation.korea
nationList = .usa

var nationList1: Nation = .france

let nationList2: Nation = .greece

switch nationList {
case .korea:
    print("This nation is Korea")
case .usa:
    print("This nation is USA")
case .france:
    print("This nation is France")
case .greece:
    print("This nation is Greece")
}

enum Fruit {
    case apple, orange, banana
}

var fruitList = Fruit.apple
fruitList = .banana

var fruitList2: Fruit = .orange

let nationList3 = Nation.korea

switch nationList {
case .greece:
    print("This nation is Greece")
case .korea:
    print("This nation is Korea")
case .france:
    print("This nation is France")
case .usa:
    print("This nation is USA")
}

let fruitListTypeAnnotation: Fruit = .apple
let anotherFruit = Fruit.banana

switch anotherFruit {
case .banana:
    print("This Banana is very good")
default:
    print("This is not Banana")
}

enum NumberList {
    case odd(Int)
    case even(Int)
}

var numberPick: NumberList = .even(24)
numberPick = NumberList.odd(91)

numberPick
type(of:numberPick)

switch numberPick {
case .odd(let x): print("홀수 :", x)
case .even(let x): print("짝수 :", x)
}


var numberPick2: NumberList = .odd(7)
numberPick2 = NumberList.even(20)

switch numberPick2 {
case .odd(let x): print("홀수 :", x)
case .even(let x): print("짝수 :", x)
}

enum CodeNumber {
    case code(String)
    case number(Int, Int, Int, Int)
}

var makeCodeNumber = CodeNumber.number(1, 3, 7, 4)
makeCodeNumber = .code("Flower")

makeCodeNumber
type(of: makeCodeNumber)

switch makeCodeNumber {
case let .number(number1,number2,number3,number4):
    print("Your Number is \(number1), \(number2), \(number3) and \(number4)")
case let .code(codeName):
    print("Yout Code Name is \(codeName)")
}

enum NameOfDay: Int {
    case sunday, monday, tuesday, wednesday, thursday, friday, saturday
}

NameOfDay.thursday
NameOfDay.thursday.rawValue

enum NameOfNumber: String {
    case one, two, three, four, five
}

NameOfNumber.four
NameOfNumber.four.rawValue

enum Gender: String {
    case male = "남자" , female = "여자" , other = "제 3의 성"
}

Gender.male
Gender.female
Gender.other

Gender.male.rawValue
Gender.female.rawValue
Gender.other.rawValue

// 문제 2. 문자(A,B,C,D,F)을 enum 으로 표현하고 각 케이스에 알맞은 0.0 ~ 4.0 까지의 값 부여

enum GPA: Double {
    case A = 4.0 , B = 3.0 , C = 2.0 , D = 1.0 , F = 0.0
}

GPA.A
GPA.A.rawValue


enum Number: Int {
    case one = 1, two, three, four, five
}

Number.one
Number.one.rawValue
Number.four
Number.four.rawValue

enum WeekDay: String {
    case sunday, monday = "mon", tuesday, wednesday = "wed", thursday, friday, saturday
}

WeekDay.sunday
WeekDay.sunday.rawValue

WeekDay.wednesday
WeekDay.wednesday.rawValue

enum NumberIntRaw: Int {
    case one = 1, two, three, four, five
}

NumberIntRaw(rawValue: 3)
NumberIntRaw(rawValue: 5)

NumberIntRaw(rawValue: 0)
NumberIntRaw(rawValue: 13)

let pickNumber = 2
//let pickNumber = 11

if let someNumber = NumberIntRaw(rawValue: pickNumber) {
    switch someNumber {
    case .one:
        print("You are pick 1")
    case .two:
        print("You are pick 2")
    default:
        print("Wrong Pick")
    }
} else {
    print("There is not \(pickNumber)")
}

enum PickPresent {
    case iPhone, tv, macPro, appleWatch
    
    func showType() {
        switch self {
        case .iPhone, .tv, .macPro:
            print("You are Pick : ", self)
        case .appleWatch:
            print("Apple Watch is good on you")
        }
    }
}

let Present = PickPresent.iPhone
Present.showType()

enum City {
    case seoul, tokyo, paris, rome
    
    mutating func travelToParis() {
        self = .paris
    }
}

var whereAreYou = City.seoul
whereAreYou

whereAreYou.travelToParis()
whereAreYou
```
