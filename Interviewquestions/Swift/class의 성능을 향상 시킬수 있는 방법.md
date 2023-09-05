# <b> class의 성능을 향상 시킬수 있는 방법 </b>

class에 final 혹은 private 키워드를 붙여서 성능을 향상할 수 있다.

<br>
<hr>
<br>

## <b> 접근 제어 </b>
- final, private는 접근 제어를 하기 위해 쓰이는 키워드이다.  

- 다른 소스파일이나 코드에서 어떠한 코드의 전체나 일부에 대한 접근을 제한한다.  

- A 클래스에 선언되어있는 함수나 변수들을 B 클래스에서의 사용여부를 제어하는 것이다.  
  
- 선언 시 앞에 키워드를 붙여서 사용하면 된다.
    ```Swift
    public class TestClass {
	    final let testStr: String = "test"
	    private var testInt: Int = 0
	    private func testFunc() { print("TEST") }
    }
    ```

- 객체지향의 특징 중 하나인 은닉화를 가능하게 한다.

<br>

### <b> 은닉화 </b>
객체 내부의 데이터, 자료들의 접근은 제한하여 은닉 시키는 것  
외부에서는 이 데이터에 있는 값이 있는 지 모른 채 수정, 조작하는 동작을 내부의 메서드(getter, setter)만을 통해 결과만 전달 받을 수 있게 된다.

<br>
<hr>
<br>

## <b> Dispatch </b>
어떤 상황에서 어떤 메서드를 호출(전송)할 것인지를 결정하고 실행하는 매커니즘이다.  
Dynamic Dispatch(동적), Static Dispatch(정적) 두 가지의 방식이 있다.

<br>

### <b> Dynamic Dispatch(동적) </b>
컴파일 시점에서 호출 할 함수를 결정한다.
앱 실행 전, 어떤 상황에서 이 함수가 호출될 것이라는 확정이 나기 때문에 성능이 좋다.

<br>

### <b> Static Dispatch(정적) </b>
런타임 시점에서 호출 할 함수는 결정한다.  
하위 클래스가 상위 클래스의 메서드를 호출할 때 해당 메모리 배열을 참조하여 호출하는 함수를 결정하는 과정을 런타임에 결정하고 성능은 떨어지게 된다.

<br>

<b> Dynamic Dispatch 메커니즘으로 작동하는 Class를 Static Dispatch 방식으로 작동하게 한다면 성능이 좋아진다 </b>

<br>
<hr>
<br>


## <b> 결론 </b>
Class의 성능을 향상시키기 위해선
1. 상속이나 오버라이딩이 필요없는 클래스나 메서드, 프로퍼티에 final을 선언
2. 파일 내에서만 접근해도 되는 경우에는 private 선언