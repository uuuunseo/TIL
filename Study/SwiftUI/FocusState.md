# <b> FocusState </b>

scene 내에 포커스 배치가 변경될 때 SwiftUI가 업데이트 하는 값을 읽고 쓸 수 있는 프로퍼티

<br>

---

<br>

## <b> iOS 15부터 나온 개념 </b>
이전 OS에서는 TextField에서 포커스 기술을 지원하지 않아서 UIKit의 도움을 받아야 했었다.
(UIViewRepresentable을 사용해 UITextView를 만들어 적용  
-> UITextFieldDelegate 프로토콜을 채택해 아래 보이는 제공 메서드를 통해 TextField의 포커싱을 해제 시켜주거나 포커싱 시켜주거나를 구현해주기)

<br>

---

<br>

## <b> FocusState </b>
- 프로퍼티 래퍼 (프로퍼티 래퍼를 앞에 붙여 해당 프로퍼티가 이미 정의되어 구현된 기능을 가질 수 있게 한다.)

<br>

```Swift
@frozen @propertyWrapper struct FocusState<Value> where Value : Hashable
```

<br>

- 래퍼를 이용해 씬의 포커싱 위치와 엮어 뷰를 사용한다.  
  
- 포커싱이 잡힌 TextField로 진입되면 속성의 래핑된 값이 지정된 값과 동일하게 업데이트 된다.
  
- 반대로 포커싱이 아웃되면 그에 맞게 다시 설정된다.
  
- 포커싱이 없는 경우를 허용해주기 위해 TextField를 옵셔널 값으로 지정해준다.
  
- 필드에서 모든 포커스를 제거하고 싶을 때 focusedField = nil로 지정해준다.

<br>


```Swift
focused(_:equals:)
focused(_:)
```

를 사용해 포커싱을 컨트롤 할 수 있다.
  