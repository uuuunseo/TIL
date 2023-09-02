# <b> State </b>

SwiftUI에서 프로퍼티가 하고 싶은 행동을 정의하는 타입

<br>

```Swift
struct ContentView: View {
    @State var textMessage: String = ""
    ...
}
```

<br>

- SwiftUI에서 View는 Struct로 선언되어있다.
    
    (일반적으로 Struct는 값 타입이라서 Struct안에 있는 값을 변경 할 수 없다.)
    
    그래서 @State라는 키워드로 값을 변경 할 수 있도록 해준다.  

- State로 선언된 변수의 값이 변경되는 경우, value의 appearance를 무효화  다시 body 값을 계산한다.

- state 변수 값이 변경되면 view를 다시 랜더링 하기 때문에 항상 최신 값을 가진다.

- 값 자체가 아닌 값을 읽고 쓰는 수단으로 사용한다.

- 현재 뷰 UI의 특정 상태를 저장하기위해 만들어진 것이기 때문에 보통 private를 사용한다.

- View 혹은 View에서 호출된 메서드에서만 접근해야 한다.

- 초기값을 지정했다면, 다른 값으로 재할당이 불가하다.