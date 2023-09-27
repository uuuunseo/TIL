# <b> @ObservedObject </b>
- observable 객체를 구독 하는 property wrapper  

- observable 객체가 변경되면 뷰에 업데이트 시켜주는 기능  

- class 형태만 가능하므로 struct가 아님을 주의해야한다.

### <b> 사용방법 </b>
- ObservedObject를 준수하는 모델을 만들고, 그 모델에서 값이 변경되면 뷰에 반영하기 위해 사용한다.

- ObservedObject를 준수하는 인스턴스를 참조하기 위해 @ObservedObject로 선언하여 참조한다.

<br>
<hr>
<br>

# <b> @StateObject </b>

- SwiftUI는 상태가 변경되면 뷰를 처음부터 다시 만들어서 그리는 동작이 있지만, @StateObject를 사용하면 뷰를 다시 만들지 않고 항상 동일한 뷰를 만든다.

### <b> 사용방법 </b>

- @ObservedObject와 동일하게 ObservableObject를 만들고, 그 인스턴스를 @StateObject로 만들어서 사용한다.

<br>
<hr>
<br>

## <b> 둘의 차이점 </b>

- 둘 다 ObservableObject를 구독하여, 값이 변경되면 뷰에 반영해주는 property wrapper의 형태이다.

- 상태 변경이 있을 때 @ObservedObject는 뷰를 다시 생성해서 그리지만,   
  @StateObject는 뷰를 다시 생성하지 않고 항상 동일한 뷰가 사용된다.

- 기본적으로 @StateObject를 사용하되, 해당 프로퍼티를 subview에게도 주입시켜야 한다면,   
    @ObservedObject로 선언하여 사용한다.
    - subview에 @StateObject 프로퍼티를 주입하면, 해당 @StateObject의 수명 주기가 두 곳에서 관리가 되므로 의존성을 줄이기 위해 @ObservedObject를 사용한다.