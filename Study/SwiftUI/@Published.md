# <b> Published </b>

- 프로퍼티의 값이 바뀌면 외부로 바뀐값들을 퍼블리시 하는 타입  
  
- @Published속성으로 프로퍼티를 게시하면, 그 타입에 대한 퍼블리셔가 생성된다.  
  
- 퍼블리셔에 접근하려면 $ 사인을 붙여야 한다.  
  
- 클래스의 프로퍼티에만 사용할 수 있고, structure 같은 non-class 타입에서는 사용이 제한된다.

```Swift
class Weather {
	@Published var temperature: Double
    init(temperature: Double) {
    	self.temperature = temperature
    }
}

let weather = Weather(temperature: 20)
cancellable = weather.$temperature
	.sink() {
    	print("Temperature now: \($0)")
}
weather.temperature = 25
```

<br>
<hr>
<br>

## <b> 동작과정 </b>
1. @Published로 선언된 프로퍼티 값이 변경
2. 그 프로퍼티의 WillSet 블럭에서 퍼블리싱이 발생
3. 그 프로퍼티를 구독하고 있는 구독자들이 실제로 그 프로퍼티에 새로운 값이 세팅되기 전에 새로운 값을 전달 받음

<br>
<hr>
<br>

## <b> MVVM </b>
- 프로젝트를 진행할 때 ViewModel이 옵저빙하고, 값이 바뀜에 따라 뷰가 다시 그려지도록 하기 위해서 ViewModel을 다 @ObservableObject를 채택하도록 해준다.

- @ObservableObject는 AnyObject를 채택하는 프로토콜이기 때문에 ViewModel을 class로 선언해주고, 내부 프로퍼티들을 @Published로 선언해준다.

```Swift
final class ContentViewModel: ObservableObject {
	@Published var isShowingSheet = false
	@Published var isShowingHistory = false
}
```