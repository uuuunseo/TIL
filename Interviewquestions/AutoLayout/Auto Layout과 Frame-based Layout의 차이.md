# <b> Auto Layout과 Frame-based Layout의 차이 </b>
AutoLayout : 뷰에 주어진 제약조건에 따라 뷰의 크기와 위치를 동적으로 계산해 배치 하는 것
-> 외부 또는 내부의 변화에 동적으로 반응해 유저 인터페이스를 구성

<br>

이런 AutoLayout을 구성할 때 iOS에서 3가지 주요 접근 방식을 사용  
1. Frame 기반의 프로그래밍 방식 (Frame-based Layout)
2. Autoresizing masks
3. Auto Layout
 
<br>

<hr>

<br>

## <b> Frame 기반의 프로그래밍 방식 (Frame-based Layout) </b>
- 코드로 하나하나 view의 frame을 설정해주어야 한다.
- super view에서 해당 view의 위치, 원점, 높이 너비를 지정해 주어야 한다.

<br>

개발자가 view의 frame 정보를 일일이 지정해야한다.  
view를 사용자 인터페이스에 배치하려면 view계층에 있는 모든 view에 대한 크기와 위치를 계산  
인터페이스에 변경이 있다면 영향을 받는 모든 view에 대해서 frame을 다시 계산

<br>

view frame을 정의하는 방식은 가장 유연하고 강력하지만,  
개발자가 직접 관리 해야하기 때문에 레이아웃 설계, 디버그 및 유지보수 하는데 상단한 시간낭비

<br>

<hr>

<br>

## <b> Autoresizing masks </b>
view의 frame이 변경되는 방식을 정의  
복잡한 사용자 인터페이스인 경우 Frame-based Layout으로 보충해줘야 한다.  
외부변경에만 적용

<br>

### <b> External Changes </b>
super view의 크기나 모양이 변경되면 발생
변경될 때 마다 view 게층의 레이아웃을 업데이트

<b> 일어나는 경우 </b>
- 사용자가 window 사이즈를 변경할 때 (OS X)
- 사용자가 iPad에서 Split View에 진입하거나 떠날때 (iOS)
- 디바이스가 회전될 때 (iOS)
- 통화 혹은 오디오 녹음 bar가 나타나거나 사라질 때 (iOS)
- 다양한 Size Class를 지원할 때
- 다양한 screen size를 지원할 때

외부변경은 런타임에 발생할 수 있고, App은 동적으로 응답해야한다.

<br>

### <b> Internal Changes </b>
사용자 인터페이스에 의해 view의 크기 또는 컨트롤의 크기가 변경될 때 발생

<b> 일어나는 경우 </b>
- App에 표시되는 콘텐츠가 변경될 때
- App이 국제화를 지원하는 경우
- App이 Dynamic Type을 지원하는 경우 (iOS)

<br>

<hr>

<br>

## <b> Auto Layout </b>
view 사이의 관계  
제약조건(두 view 사이의 관계)로 사용자 인터페이스를 정의  
제약조건을 기반으로 각 view의 크기와 위치를 계산  
내부와 내부 변경 모두에 동적으로 반응하는 레이아웃 생성

<br>

<hr>

<br>

## <b> 정리 </b>

### <b> 레이아웃 변화 </b>

- 외부변화 : superview의 변화로 생기는 변화 사용자의 인터랙션과 상관없는 변화
- 내부변화 : 사용자의 인터랙션과 상관있는 변화

<br>

### <b> 차이? </b>  

<b> Frame-based Layout </b>  
<b> 장점 </b> : 속도가 빠르고, 가장 유연하고 강력한 기능  
<b> 단점 </b> : 모든 디바이스에 대응하도록 설계해야하고, 그에 따라 레이아웃이 복잡해지면 디버그, 유지보수가 힘들다

<b> Auto Layout </b>  
<b> 장점 </b> : view와의 관계를 정의하므로 모든 디바이스에 자동으로 적용 가능  
<b> 단점 </b> : Frame-based Layout보다 속도가 느리다.
 