# <b> MVVM </b>
Model + View + ViewModel  
소프트웨어 아키텍처 패턴이다.

- 앱이 수정되고, 규모가 커지면서 UI와 비지니스 로직사이의 결합도가 커지게 되면서 UI수정에 대한 비용이 커지고 유닛테스트가 어렵게 된다.

- MVVM패턴을 사용함으로써 비지니스 로직과 프레젠테이션 로직을 UI로 부터 분리할 수 있다.

- 코드 재사용이 가능하게 된다.

- 앱의 개발, 유지보수, 테스트를 더 용이하게 해준다.

<br>
<hr>
<br>

## <b> Model </b>
- 데이터와 관련된 코드를 담고있다.  
  
- 데이터를 담아두기 위한 구조체, 네트워크로직, JSON 파싱 코드를 가진다.

```Swift
struct Person {
  let name: String
  var age: Int
  init(json: JSON) {
    name = json["name"].stringValue
    age = json["age"].intValue
  }
}
```

- View, ViewModel 계층을 전혀 신경쓰지 않아도 된다.  
  
- 데이터를 어떻게 저장할지만 생각하면 된다.

<br>
<hr>
<br>

## <b> View </b>
- 유저에게 보여지는 앱의 UI에 대한 코드를 담고 있는 계층이다.
  
- View의 각 컴포넌트에 대한 정보를 담고있다.

- 어느 위치에 어떻게 배치될지 작성되어있다.
  
- View는 디자인적 요소에 더불어 ViewModel로 부터 데이터를 가져와 어떻게 배치할 지, 특정 상황에 따라 ViewModel의 어떤 Method를 이용할 지에 대해서도 담고 있다.
  
- MVC와 마찬가지로 View는 재사용성이 강조된다.

- 컴포넌트를 잘 설계하여 중복된 코드를 줄이는 것이 중요하다.

- MVVM패턴에서 View는 Model을 직접 소유하지 않고, ViewModel로 부터 받아와서 정보를 넣어주는 방식이 일반적이다.

<br>
<hr>
<br>

## <b> ViewModel </b>
- 앱의 핵심적인 비지니스 로직을 담고 있는 코드의 계층이다.
  
- MVC 패턴의 Controller와 비슷한 역할이다.
  
- View와 Model사이에서 View의 요청에 따라 로직을 실행하고, Model의 변화에 따라 데이터를 처리하여 View를 refresh한다.
  
- Model에 변화가 생기면 View에게 notification을 보내는 역할을 한다.
  
- View로부터 전달받는 요청을 해결할 비지니스 로직을 담는다.
  
- ViewModel은 UI관련 코드로부터 완전히 분리되어있다.
  
- ViewModel파일에는 SwiftUI같은 UI프레임워크를 import하지 않아도 된다.
  
<br>
<hr>
<br>

## <b> 동작과정 </b>
1. 유저의 Action들은 View를 통해 입력된다.
2. Viewdp Action이 들어오면, Command패턴으로 ViewModel에 Action을 전달한다.
3. ViewModel은 Model에게 데이터를 요청한다.
4. Model은 ViewModel에게 요청받은 데이터로 응답한다.
5. ViewModel은 응답받은 데이터를 가공해 저장한다.
6. View는 ViewModel과 Data Binding해 화면을 표시한다.