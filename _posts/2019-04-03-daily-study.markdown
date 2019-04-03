---
layout: post
title:  "2019-04-03-Daily Study"
date:   2019-04-03
categories: Swift
---

# Today Study

---

오늘 Type Casting에 대해 공부하면서 다시 기초적인 부분에 대한 이해가 부족하다는 것을 느꼈다  
먼저, 타입 비교 **"is"** 에 대한 예시를 보고 내가 직접 코드를 작성해보면서 내가 몰랐던것과 이해 되지 않았던 점을 정리해서 간단히 말해보겠다  
  
- is로 타입을 비교하는 코드를 쳐보고 이 코드의 결과를 보면서 is로 타입을 비교하는 것에 대한 이해도를 높였다  
  
```
let stringArray:[String] = ["A","B","C"]

if stringArray[0] is Int {
    print("Int 타입의 Array 입니다")
} else if stringArray[0] is Double {
    print("Double 타입의 Array 입니다")
} else if stringArray[0] is String {
    print("String 타입의 Array 입니다")
} else {
    print("타입을 알 수 없습니다")
}
```

- 출력 : String 타입의 Array 입니다  
  
위에 나온 코드를 치면서 알게 된 점은 "객체 is 객체의 타입" 으로 하여 객체의 타입이 객체와 같은 타입이면 true, 아니면 false를 반환한다  
이것을 응용하여 String 타입의 Array를 만들어 if문 안에 Array의 0번째 인덱스와 각각의 타입인 Int, Double, String를 is 로 비교하여 맞으면 true 아니면 false를 반환하므로 그에 맞는 출력을 하도록 만들었다  
  
그렇다면 클래스의 인스턴스를 담은 Array도 is 로 타입 확인이 가능할까?  
  
먼저 클래스를 만들고 클래스 별로 상속을 한 코드를 만들어 보자  
  
```
class Human {
  var name: String = "name"
}
class Baby: Human {
  var age: Int = 1
}
class Student: Human {
  var school: String = "school"
}
class UniversityStudent: Student {
  var univName: String = "Univ"
}
```
  
그리고 각각의 클래스 인스턴스를 한 배열에 담아보고 is로 타입을 비교해보자
  
```
let arrayAll = [Human(), Baby(), Student(), UniversityStudent()]
type(of: arrayAll)

arrayAll[0] is Human // T
arrayAll[0] is Baby // F
arrayAll[0] is Student // F
arrayAll[0] is UniversityStudent // F

arrayAll[1] is Human // T
arrayAll[1] is Baby // T
arrayAll[1] is Student // F
arrayAll[1] is UniversityStudent // F

arrayAll[2] is Human // T
arrayAll[2] is Baby // F
arrayAll[2] is Student // T
arrayAll[2] is UniversityStudent // F

arrayAll[3] is Human // T
arrayAll[3] is Baby // F
arrayAll[3] is Student // T
arrayAll[3] is UniversityStudent // T
```
  
이렇게 Array의 각 인덱스 별로 Human, Baby, Student, UniversityStudent 와 is 로 타입을 비교해보고 그에 따른 true와 false를 값을 확인했다  
  
다음으로는 변수에 타입을 지정하고 다른 클래스 인스턴스를 할당해 그 변수 값의 타입과 그 타입에 따른 프로퍼티의 사용가능 범위를 확인해보자  
  
```
var human: Human = Student()

type(of: human) // _lldb_expr_43.Student.Type

그렇다면 human이 사용 할 수 있는 범위를 알아보자

human.name // "name"
human.school // error Human type엔 school이라는 멤버가 없다는 오류 메시지가 뜬다

그럼 다른 확인을 위해 다른 코드를 작성

human = Baby() // Baby, Baby 인스턴스가 할당이 잘 된다
human = UniversityStudent() // UniversityStudent() , 이 또한 잘된다

var sua: Student = Student() // Student
sua = UniversityStudent() // UniversityStudent
sua = Baby() // error Baby 타입은 Student 타입으로 assign 할 수 없다는 오류 메시지가 뜬다
```
  
- sua 는 Student 인스턴스도 받고 UniversityStudent도 받는데 Baby는 못받는 이유는 무엇일까?
    - **바로 처음 초기 타입의 할당 때문이다**
  
내가 이 점에서 너무 많은 착각과 공부를 덜했구나 라는 생각을 하였다.  
처음 초기값을 할당 할 때 sua에게 Student라는 타입을 주었다, 이것이 var이든 let이든 처음 초기값으로 준 타입은 변하지 않는다는 점을 인지하고 있어야 위의 내용이 이해가가는데 나는 미쳐 생각하지 못했던것이다.  
  
그렇다면 sua가 접근 가능한 속성들이 어떤것들이 있는지 알아보자  
  
```
sua.name // name , Human의 속성은 가능
sua.age // error // Baby 속성은 불가능
sua.school // school // Student 속성은 가능
sua.univName // error // UniversityStudent 속성은 불가능
```
  
여기서 또 의문점이 들었다 "sua는 분명히 UniversityStudent 인스턴스를 받았는데 왜 UniversityStudent 속성인 univName이 접근이 불가능하지??"
그 이유는 역시 타입 때문이였다.  
sua는 UniversityStudent 인스턴스를 할당 받았지만 Student 타입을 갖고 있기 때문에 컴파일러는 Student가 가지고 있는 school 만 접근이 가능하게 알고 있기 때문이다.
