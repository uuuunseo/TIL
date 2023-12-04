# <b> Property Wrapper </b>

속성이 저장되는 방식을 관리하는 코드와 속성을 정의하는 코드 사이에 분리 계층을 추가한다.

프로퍼티를 감싸 특별한 타입으로 만들어 준다.

프로퍼티에 커스텀한 어떤 로직들을 매번 동일하게 지정해주지 않고 Property Wrapper로 만든 타입으로 프로퍼티를 선언해 동일 로직을 수행하게 한다.

지역 변수에서만 사용가능하다.

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