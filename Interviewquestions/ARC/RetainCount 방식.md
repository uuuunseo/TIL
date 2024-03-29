# <b> RetainCount 방식 </b>
ARC의 메모리 관리 방법  
compile time에 자동으로 retain, release를 적절한 위치에 삽입하는 방식

<br>

### <b> compile time </b>
코드를 분석하고 예측하여 적절한 위치에 retain, release를 삽입해준다.

<br>

### <b> run time </b>
삽입된 코드가 실행되면서 retain, release에 의해 reference count를 증감하고 count가 0이 되었을 때 메모리에서 제거(deinit)한다.

<br>

## <b> 참조 횟수 count up (+) </b>
인스턴스의 주소값을 변수에 할당할 때 참조횟수가 증가

<br>

### <b> 인스턴스를 새로 생성할 때 </b>
지역변수는 스택에 할당되고 실제 인스턴스는 힙에 할당되고, 지역변수에는 힙에 할당된 인스턴스의 주소값이 들어 가므로  
RC값이 증가한다

<br>

### <b> 기존 인스턴스를 다른 변수에 대입할 때 </b>
기존 인스턴스를 다른 변수에 대입할 때도 참조에 의하기 때문에  
RC값이 증가한다

<br>
<hr>
<br>

## <b> 참조 횟수 count down (-) </b>

<br>

### <b> 인스턴스를 가리키던 변수가 메모리에서 해제되었을 때 </b>
인스턴스를 참조하고 있던 변수가 메모리에서 해제되면 해당 인스턴스의 RC값이 감소

<br>

### <b> nil이 지정되었을 때 </b>
지역변수가 옵셔널타입일 떼  
변수의 값에 nil이 지정되었을 때 해당 인스턴스의 RC값이 감소 

<br>

### <b> 변수에 다른 값을 대입한 경우 </b>
변수에 저장된 주소값이 바뀌어서 참조 카운터가 변경된다.

<br>

### <b> 프로퍼티의 경우, 속해 있는 클래스 인스턴스가 메모리에서 해제될 때 </b>
a클래스 안에 b라는 클래스 인스턴스가 존재하고,   
a인스턴스 c를 생성하면 c는 물론,   
프로퍼티인 b의 인스턴스도 생성되면서 두 인스턴스 각각의 RC가 증가된다.  

b는 c가 가리키던 인스턴스에 소속된 프로퍼티이기 때문에, c가 가르키던 인스턴스가 메모리에서 해제될 경우 b의 RC가 감소한다.

<br>

<b> c가 가리키던 a인스턴스가 메모리에서 해제된다고 해서, 프로퍼티인 b가 가리키던 b인스턴스의 메모리가 같이 해제되는 것은 아니다! </b>  
b인스턴스의 RC값이 감소할 뿐이다.
