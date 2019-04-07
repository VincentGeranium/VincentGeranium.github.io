# Lazy Stored Properties
---

게으른 저장 프로퍼티(Lazy Stored Properties)

뭔가 이름부터 귀엽다. 게으른 저장 프로퍼티 나 같은 느낌의 프로퍼티 :)
나도 한 게으름하기 때문이다
다시 본론으로 들어가 게으른 저장 프로퍼티는 어떻게 구현되고 실행되고 행동하는지 알아보자!!

게으른 저장 프로퍼티는 **값이 사용되기 전까지는 값이 계산되지 않는 프로퍼티**이다

**lazy** 라는 키워드를 사용하여 선언합니다

전혀 감이 안잡힌다,,,, :(
그럴땐 역시 예제가 최고지!! 예제를 봐 봅시다!!

```
class DataImporter {
    var fileName: String = "data.txt"
}

class DataManager {
    lazy var importer = DataImporter()
    var data = [String]()
}

let manager = DataManager()

manager.data.append("Some data")

manager.data.append("Some more data")
```

DataImporter 클래스를 정의 했다, 이 클래스는 데이터를 가져오는 클래스이다
그 안에는 fileName이라는 String 타입의 가변 저장 프로퍼티가 선언되있고 초기값으로 data.txt로 되어있다.

그다음 클래스는 DataManager이다 데이터를 관리하는 클래스이다 
이 클래스의 importer는 **lazy** var 형식으로 선언되었고 DataImporter클래스의 인스턴스이다
그 다음 data 프로퍼티는 빈 배열 String타입으로 초기화 되어있다

let manager는 DataManager 클래스의 인스턴스이고 DataManger 클래스는 data라는 빈 배열 프로퍼티와 importer라는 DataImporter의 인스턴스를 가지고 있다
manager 상수 인스턴스는 클래스 인스턴스라서 let으로 선언해도 값이 들어간다 왜냐하면 manager는 인스턴스이고 그 인스턴스의 클래스는 참조타입이기 때문이다 -> 값, 참조에 대한 차이점은 나중에 더 자세히 설명하겠다

다시 돌아와서 manager.data.append()를 이용하여
data 프로퍼티에 ()안에 들어간 데이터들을 배열에 추가하고 있다

**하지만 아직까지 DataImport의 인스턴스인 게으른 저장 프로퍼티 importer는 생성되지 않았다 그 이유는 바로 게으른 저장 프로퍼티이기 때문이다**

게으른 저장 프로퍼티는
- **초기값이 인스턴스의 초기화가 될때까지 값을 모르는 외부요소에 의존하는 경우에 유용**
- **초기값이 복잡하거나 계산비용이 많이드는 설정을 필요로 할때도 유용**
  
**Importer 라는 DataImporter의 인스턴스는 lazy로 선언되었으니 게으른 저장 프로퍼티**이다
**하지만 밖에서 manager라는 DataManager의 인스턴스를 이용해 importer에 한번도 접근을 안했다**
- lazy로 선언을 안했다면 (원래대로라면) importer가 생성이 되었겠지만, lazy로 선언되었으니 사용되기 잔까지 생성하지 않는다
- **importer 프로퍼티에 처음 엑세스 할 때 만들어지게 된다**

```
print(manager.importer.fileName)
```

- **위와 같이 해야 비로소 importer라는 DataImporter 인스턴스가 생성된다**
  
여기서 궁굼한점!! 왜 importer라는 프로퍼티를 lazy stored property로 만들었을까??
  
DataManager 인스턴스인 manager는 파일에서 데이터를 가져오지 않고도 데이터를 관리 할 수 있다
무슨말인지 도무지 이해가 안간다,,,,
그러니까 DataManager 인스턴스를 만들때 (manager를 만들 때) DataImporter 인스턴스를 만들 필요가 없다는 말이다, **대신 DataImporter 인스턴스를 처음 사용하게 될 때 생성하는 것이 더 합리적이다 라는 말이다**

오! 뭔가 감이 잡힌다!!
이 게으른 저장 프로퍼티를 잘 사용하면 성능도 올라가고, 공간낭비도 줄일 수 있다!!
  
이제는 게으른 저장 프로퍼티의 특징을 조금 더 알아보자
  
- 첫번째 **반드시 lazy 프로퍼티는 항상 변수로서 선언**해야한다
    - **초기값은 인스턴스 초기값이 검색되지 않을 수 있기 때문이다**
    - let으로 선언한 프로퍼티는 인스턴스를 만들 때 빼고, 값을 변경 할 수 없다
        - 이렇게 let으로 선언한 프로퍼티는 초기화를 함과 동시에 값을 가져야하기 때문에, 게으른 저장 프로퍼티로 선언 할 수 없다
        - **게으른 저장 프로퍼티는 "값이 필요할 때" 초기화를 하기 때문이다**
- 두번째 **lazy로 선언했다고 해도 lazy 프로퍼티가 초기화 되지 않은 상태에서 여러 쓰레드가 동시에 이 lazy 프로퍼티에 엑세스 하려 한다면, 이 프로퍼티가 단 한번만 초기화 된다는 것을 보장할 수 없다**
