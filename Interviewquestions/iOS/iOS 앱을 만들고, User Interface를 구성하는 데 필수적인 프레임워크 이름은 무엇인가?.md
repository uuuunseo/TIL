# <b> iOS 앱을 만들고, User Interface를 구성하는 데 필수적인 프레임워크 이름은 무엇인가? </b>

UIKit이다.

<br>
<hr>
<br>

## <b> UIKit </b>
iOS Application의 cocoaTouch에서 UserInterface를 구현하고 이벤트를 관리하는 프레임워크

- Gesture처리, Animation, 그림 그리기, 이미지 처리, 텍스트 처리 등 UserEvent처리를 한다.
  
- TableView, Slider, Button, TextField, Alert등 Application의 화면을 구성하는 요소를 포함하고 있다.

- UIResponder에서 파생된 클래스나 User Interface에 관련된 클래스는 Application의 Main Thread (Main Dispatch Queue)에서만 사용해야 한다.

- iOS, tvOS에서 사용한다.

<br>
<hr>
<br>

## <b> User Interface </b>
- View and Controller : 화면에 콘텐츠 표시
  
- ViewController : 사용자 인터페이스 관리
  
- Animation and Haptics : 애니메이션과 햅틱을 통한 피드백 제공
  
- Window and Screen : 뷰 계층을 위한 윈도우 제공

<br>
<hr>
<br>

## <b> User Action </b>
- Touch, Press, Gesture : 제스처 인식기를 통한 이벤트 처리 로직이다.

- Drag and Drop : 화면 위에서 드래그 앤 드롭 가능이다.

- Pencil Action : 애플 펜슬의 더블 탭 동작을 인식하는 기능이다.

- Focus Animation : 원격 또는 게임 컨트롤러를 사용

- Peek and Pop : 3D터치에 대응한 미리보기 기능

- Keyboard and Menu : 키보드 입력처리 및 사용자 정의 메뉴 표시

<br>
<hr>
<br>

## <b> Text </b>
- Text Display and font : UIKit View를 사용한 텍스트 표시, 폰트 관리, 맞춤법 검사

- Text Storage : 텍스트 스토리지를 관리하고 텍스트 레이아웃 조정

- Keyboard and Input : 시스템 키보드를 설정하거나 직접 키보드를 만들어 입력 처리

- Handwriting Recongnition : 애플펜슬로 텍스트 필드와 커스텀 뷰를 통해 입력받는 텍스트를 감지