# <b> Property Wrapper </b>
특별한 기능을 갖는 속성을 정의하는 데 사용한다.
 
코드를 간결하고 읽기 쉽게 만들 수 있다.  

속성에 적용되는 래퍼(Wrapper)로, 속성의 값에 추가적인 로직을 적용하거나, 값이 변경될 때 다른 동작을 수행할 수 있도록 해준다.  

Swift의 속성 관찰자를 대체할 수도 있다.  

반복되는 로직들을 프로퍼티 자체에 연결할 수 있다.

<br>
<hr>
<br>

## <b> 사용법 </b>

### <b> propertyWarpper 정의하기 </b>

```swift
@propertyWrapper
struct TestPropertyWrapper<T> {
    private var value: T

    init(wrappedValue: T) {
        self.value = wrappedValue
    }

    var wrappedValue: T {
        get {
            return value
        }
        set {
            value = newValue
        }
    }
}
```

프로퍼티 래퍼를 정의하려면 먼저 @propertyWrapper 속성을 사용해 구조체를 만든다.

WrappedValue 이름의 변수를 사용해 래핑되는 값의 타입을 정의하고, 필요한 초기화 및 접근 로직을 구현한다.

<br>

### <b> Property Wrapper 적용 </b>

프로퍼티 래퍼를 적용하려면 클래스나 구조체의 프로퍼티 앞에 @기호와 함께 래퍼 이름을 사용한다.

→ 프로퍼티에 대한 접근 로직이 프로퍼티 래퍼에서 정의한 대로 처리된다.

<br>

### 활용 예시

**UserDefault**

```swift
@propertyWrapper
struct UserDefault<Value> {
    let key: String
    let defaultValue: Value

    init(key: String, defaultValue: Value) {
        self.key = key
        self.defaultValue = defaultValue
    }

    var wrappedValue: Value {
        get {
            return UserDefaults.standard.object(forKey: key) as? Value ?? defaultValue
        }
        set {
            UserDefaults.standard.set(newValue, forKey: key)
        }
    }
}
```

```swift
class Settings {
    @UserDefault(key: "isDarkModeEnabled", defaultValue: false)
    var isDarkModeEnabled: Bool

    @UserDefault(key: "lastUpdated", defaultValue: nil)
    var lastUpdated: Date?
}
```

<br>
<hr>
<br>

## <b> 종류 </b>
1. <b> @State </b>
   - SwiftUI 뷰의 상태를 저장하는데 사용된다.
  
   - 값을 변경할 때 마다 뷰가 다시 렌더링 된다.
  
   - UI컴포넌트의 상태를 저장하는ㄴ데 사용된다.

2. <b> @Binding </b>
   - 부모 뷰에서 자식 뷰로 값을 전달하고, 자식 뷰에서 부모 뷰로 값을 다시 전달하는데 사용된다.
  
   - 부모 뷰의 속성을 자식 뷰에서 변경하는 데 유용하다.

3. <b> @ObservedObject </b>
   - 외부에서 제공되는 ObservableObject 프로토콜을 준수하는 객체의 상태를 저장하는 데 사용된다.
  
   - 뷰에서 @ObservableObject 속성을 참조하면 해당 객체가 변경될 때마다 뷰가 다시 렌더링 된다.

4. <b> @EnvironmentObject </b>
   - 앱의 전역 상태를 저장하는 데 사용한다.
  
   - 앱의 다른 뷰에서도 동일한 객체에 접근하여 상태를 공유할 수 있다.

5. <b> @FetchRequest </b>
   - CoreData에서 데이터를 검색하는 데 사용된다.
  
   - 뷰에서 CoreData의 적절한 엔터티와 조건을 설정하여 데이터를 가져올 수 있다.

<br>
<hr>
<br>

## <b> Projected Value </b>

프로퍼티 래퍼와 관련된 추가정보나 기능을 노출하려면 projected Value를 사용한다.

보조 데이터 제공, 프로퍼티 래퍼에 추가적인 동작을 수행하도록 할 수 있다.

```swift
@propertyWrapper
struct WrapperWithProjectedValue<T> {
    var wrappedValue: T
    var projectedValue: String

    init(wrappedValue: T, projectedValue: String) {
        self.wrappedValue = wrappedValue
        self.projectedValue = projectedValue
    }
}
```

프로퍼티 래퍼 구조체에 projectedValue를 정의해야 한다.

<br>

원하는 값을 반환하도록 구현하면 된다.

```swift
class MyClass {
    @WrapperWithProjectedValue(projectedValue: "Example")
    var value: Int = 0
}

let myInstance = MyClass()
print(myInstance.$value) // 출력: Example
```

프로퍼티에 프로퍼티 래퍼를 적용한 후 $기호를 사용해 projectedValue에 접근할 수 있다.