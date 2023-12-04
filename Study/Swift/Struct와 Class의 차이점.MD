# <b> Struct와 Class의 차이점 </b>

**Class** : 참조 타입 ARC로 메모리 관리를 한다.

**Struct** : 값 타입이다.

**→ Class와 Struct의 차이점을 확실히 알고 있다면 성능개선을 할 수 있다.**

<br>
<hr>
<br>

## <b> 공통점 </b>

- 값을 저장할 프로퍼티를 선언할 수 있다.
  
- 함수적 기능을 하는 메서드를 선언 할 수 있다.
  
- 내부 값에 .을 사용해 접근할 수 있다.

- 생성자를 사용해 초기 상태를 설정할 수 있다.
  
- extention을 사용해 기능을 확장할 수 있다.
  
- Protocol을 채택하여 기능을 설정할 수 있다.

<br>
<hr>
<br>

## <b> 차이점 </b>

### <b> Class </b>

- 참조 타입이다.
  
- ARC로 메모리를 관리한다.
  
- 같은 클래스 인스턴스를 여러 개의 변수에 할당한 뒤 값을 변경시키면 할당한 모든 변수에 영향을 준다. (메모리만 복사)
  
- 상속이 가능하다.
  
- 타입 캐스팅을 통해 런타임에서 클래스 인스턴스의 타입을 확인할 수 있다.
  
- deinit을 사용해 클래스 인스턴스의 메모리 할당을 해제할 수 있다.

<br>

### <b> Struct </b>

- 값 타입이다.
  
- 구조체 변수를 새로운 변수에 할당할 때마다 새로운 구조체가 할당된다.
  
- 같은 구조체를 여러 개의 변수에 할당한 뒤 값을 변경시키더라도 다른 변수에 영향을 주지 않는다. (값 자체를 복사)

<br>

### <b> 예시 </b>

```swift
import Foundation

class test {
    var count = 0
    
    deinit {
        print("할당 해제")
    }
}

struct testt {
    var count = 0
}

var class1 = test()
var class2 = class1
var class3 = class1

print("------class 값 바꾸기 전------")

print(class1.count)
print(class2.count)
print(class3.count)

class3.count = 4

print("------class 값 바꾼 후------")
print(class1.count)
print(class2.count)
print(class3.count)

var struct1 = testt()
var struct2 = struct1
var struct3 = struct1

print("------struct 값 바꾸기 전------")
print(struct1.count)
print(struct2.count)
print(struct3.count)

struct3.count = 4

print("------struct 값 바꾼 후------")
print(struct1.count)
print(struct2.count)
print(struct3.count)
```

<br>

### <b> 출력 </b>

![Untitled](./../../img/Class_Struct_img_1.png)

클래스는 참조타입이라 같은 클래스를 할당한 변수의 값을 변경 시키면 참조된 객체의 값이 변경,

구조체는 객체를 할당해도 매번 새로운 메모리가 할당되어 값을 변경하더라도 다른 구조체 변수에 영향을 주지 않는다.

<br>
<hr>
<br>

## <b> Class와 ARC, Retain Cycle </b>

### 예시

```swift
print("ARC\n")
var classARC1: test? = test()
print(CFGetRetainCount(classARC1))

var classARC2 = classARC1
print(CFGetRetainCount(classARC1))

classARC1 = nil
print(CFGetRetainCount(classARC2))
classARC2 = nil
```

<br>

### <b> 출력 </b>
![Untitled](./../../img/Class_Struct_img_2.png)

클래스 인스턴스를 여러곳에 참조하게 되면, 원래 인스턴스를 해제하더라도 참조 카운트가 남아있어 deinit이 실행되지 않는다. → 참조되는 모든 값들을 해제해줘야 deinit이 실행된다.

이러한 특징 때문에 retain cycle이 발생하기도 한다. → weak, unowned 참조를 사용해서 해결

<br>
<hr>
<br>

## <b> 할당 </b>

구조체는 언제 생기고 사라질지 컴파일 단계에서 알 수 있기 때문에 메모리의 Stack공간에 할당

클래스는 참조가 어디서 어떻게 될지 모르기 때문에 Heap공간에 할당

### <b> stack </b>

- LIFO 형태의 자료구조

- 가장 마지막에 들어간 객체가 가장 먼저 나오게 되는 자료구조 (후입선출)

- 컴파일 단계에서 언제 생성되고 해제되는지 알 수 있는 구조체와같은 값들이 스택에 저장된다.

- 메모리 할당과 해제가 하나의 명령어로 처리할 수 있다. (pop, push)

- 스레드들은 각각 독립적인 Stack공간을 가지고 있기 때문에 상호 배제를 위한 자원이 필요하지 않다. → 스레드로부터 안전하다.

- Stack의 값을 사용하는 것이 Heap의 값을 사용하는 것보다 빠르다.

<br>

### <b> Heap </b>

- 컴파일 단계에서 생성과 해제를 알 수 없는 참조 타입의 객체가 할당된다. ex) 클래스 객체

- 메모리 할당과 해제를 하나의 명령어로 처리 할 수 없다. → 참조 계산도 해줘야 하므로 Stack보다 복잡

- 스레드가 공유하는 메모리 공간이기 때문에 스레드로부터 안전하지 않다. → 관리해주기 위한 lock같은 자원도 필요하다. → 오버헤드가 발생

<br>

### <b> 섞어서 쓰게 됐을 때 </b>

- **값 타입을 포함하는 참조타입**
    - Class 안에 Struct프로퍼티가 존재하는 경우
  
    - 참조 타입이 할당 해제되기 전에 값 타입도 할당 해제되지 않게 하기 위해 값 타입도 힙에 저장
  
    - 클로저 내부에서 사용하는 값 타입도 포함된다.
  
- **참조 타입을 포함하는 값 타입**
    - Struct안에 Class 프로퍼티가 존재하는 경우
  
    - 값 타입은 힙에 할당되지 않지만 내부에 참조 타입이 있기 때문에 참조 카운트 처리를 해줘야 한다.

<br>
<hr>
<br>

## <b> Copy-on-assignment, Copy-on-write </b>
<br>

**Copy-on-assignment**

- 값 타입을 다른 변수에 할당하면 복사한다.
  
- 새로운 메모리 공간에 값은 값을 복사한다.

<br>

**Copy-on-write**

- 메모리를 할당하지 않고 같은 곳을 본다.
  
- 해당 값을 변경할 때 실제로 메모리에 값을 복사하고 값을 변경하게 된다.

<br>
<hr>
<br>

## <b> 언제 클래스를 쓰고 언제 구조체를 쓰는 것이 좋을까? </b>

1. 단순한 데이터 값을 보유하기 위해서는 구조체
   
2. 메모리의 스택은 크기가 크지 않기 때문에 작은 값을 갖는 데이터를 처리할 때 구조체를 사용
   
3. Objectice-와 상호 운용성을 원할 때는 클래스를 사용한다.