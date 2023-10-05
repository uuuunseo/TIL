# <b> MVC </b>
Model + View + Controller  
소프트웨어 아키텍처 패턴이다.  
View와 Model사이의 의존성이 크다.

<br>
<hr>
<br>

## <b> Model </b>
앱이 정확히 무엇을 할지 코딩하는 것이다.  
비즈니스 로직을 담당하는 함수들이 정의되고, 처리되는 데이터(클래스, 구조체 등)와 내부 알고리즘이 정의된다.

<br>
<hr>
<br>

## <b> View </b>
사용자에게 말 그대로 보여지는 영역으로 볼 수 있다.  
Storyboard 파일을 비롯해서 인터페이스를 구축하는 영역으로 생각하면 될 것 같다.

<br>
<hr>
<br>

## <b> Controller </b>
Model 과 View 사이의 다리라고 보면 된다.  
Controller는 Model이 가지고 있는 데이터를 어떻게 할 것인지 명령을 내린다.  
명령을 토대로 사용자에게 보여지는 인터페이스 부분도 수정을 한다.
사용자가 View를 통해 Interaction을 하면 Controller가 이를 control한다는 것이다.

Model 에서는 비즈니스 로직을, View에서는 사용자에게 보여지는 것들을, 그리고 Controller 에서는 어떻게 Model 을 활용해서 View 에게 보여질 것인지만 정의하면 되니, 코드가 간결해지고, 관리가 용이해진다.

<br>
<hr>
<br>

## <b> 동작 순서 </b>

1. 사용자의 Action이 View를 통해 들어옴
2. View는 데이터를 Presenter에 요청
3. Presenter는 Model에게 요청
4. Model이 응답
5. Presenter는 View에 응답
6. View가 화면에 보여줌