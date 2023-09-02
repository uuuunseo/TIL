
# <b> available </b>
해당 속성을 이용해 특정플랫폼이나 또는 OS 버전에서 코드를 실행하도록 해주고, 분기처리를 할 수 있다.  
Swift는 #available로 Objective-C는 @available로 사용된다.

<br>

---

<br>

## <b> 분기처리 </b>
버전 별로 코드를 다르게 동작시키는 경우들이 종종있다.  
iOS17에서 지원하는 기능을 사용하고 싶은데 프로젝트의 미니멈 타겟이 iOS15라고 한다면  
iOS17 이상에서는 A동작, 그 밑에는 B동작 이렇게 나누어 주는 것이 분기처리이다.

<br>

---

<br>

## <b> available의 attribute들 </b>
- 모든 애플 생태계의 모든 플랫폼을 속성으로 둘 수 있다.  
  
- 둘 이상의 속성은 쉼표로 나타낸다.  
  
- *는 나열된 모든 플랫폼에서 선언의 가용성을 나타낸다. (Swift버전 번호를 사용해 가용성을 지정하는 속성에는 사용이 불가능하다.)

<br>

---

<br>

## <b> #available </b>
여러 플랫폼에서 서로 다른 논리 처리를 결정하기 위해 조건문과 함께 사용한다.   
Bool타입을 반환하는 런타임 검사이다.  

<br>

```Swift
if #available(iOS 17, *) {
  // 17 이상 버전 코드
}
else {
  // 17 미만 버전 코드
}
```

<br>

- <b> *</b>는필수로 적어주어야 한다.
- 해당 버전을 포함하여 그 이상의 버전인지를 확인한다.

<br>

---

<br>

## <b> @available </b>
함수(메서드), 클래스 또는 프로토콜 앞에 사용한다. (타입 또는 프로토콜이 적용되는 플랫폼 및 OS를 나타낸다.)  
조건문과 같이 분기처리를 할 수 없고, 배포 타겟 버전을 체크한다.

<br>

```Swift
@available(iOS 17, *)
func example() { }
```
- 배포타겟이 17미만이라면 컴파일 시 에러가 나타난다.

<br>

---

<br>

### <b> unavailable </b>
지정된 플랫폼에서 사용할 수 없다.
Swift 버전 가용성을 지정할때는 사용할 수 없다.

<br>

```Swift
@available(*, unavailable)
func example() { }
```
- 대신 특정 플랫폼을 지정하면 그 플랫폼에서만 사용할 수 없는 메소드가 된다.

<br>

---

<br>

### <b> introduced </b>
선언이 도입된 지정된 플랫폼 혹은 언어의 첫 번째 버전을 나타낸다.

<br>

```Swift
@available(*, introduced: 17.0)
func example() { }
```
- 17 이상 버전에서만 사용할 수 있고 미만 버전에서 사용 시 컴파일 에러가 생기게 된다.

<br>

---

<br>

### <b> deprecated </b>
선언이 사용되지 않는 지정된 플랫폼 혹은 언어의 첫번째 버전을 나타낸다.  
버전 번호를 생략하면 선언이 현재 사용 중단되었음을 나타내며 언제 사용중단이 발생했는지에 대해서는 정보를 제공하지 않는다. (버전번호를 생략해야 한다면 콜론도 생략)

<br>

```Swift
@available(*, deprecated: 17.0)
func example() { }
```
- 17버전에서 deprecated 되었다는 경고 메시지를 노출시키도록 할 수 있다.  

<br>

---

<br>

### <b> obsoleted </b>
선언이 폐기된 지정된 플랫폼 혹은 언어의 첫번째 버전을 나타낸다.  
선언이 폐기되면 지정된 플랫폼이나 언어에서 제거되기 때문에 사용할 수 없다.

<br>

```Swift
@available(swift, obsoleted: 5.9)
func nyamnyam() { }
```
- deprecated는 경고, obsoleted는 에러를 띄운다.  
- swift5.9 버전 이하이면 에러가 난다.

<br>

---

<br>

### <b> message </b>
더 이상 사용되지 않거나 폐기된 선언을 사용시 경고 혹은 오류를 내보낼 때 컴파일러가 표시하는 텍스트 메시지를 제공한다.  

<br>

```Swift
@available(*, unavailable, message: "헤헤헹")
func example() { }
```
- unavailable과 같이 선언해주면 example메서드를 사용하려고 할 때 컴파일 오류 메시지로 헤헤헹이 나오게 된다.

<br>

---

<br>

### <b> renamed </b>
이름이 변경된 선언의 새 이름을 나타내는 텍스트 메시지를 제공한다.

<br>

```Swift
protocol HiProtocol {
    ...
}

protocol ByeProtocol {
    ...
}

@available(*, unavailable, renamed: "ByeProtocol")
typealias HiProtocol = ByeProtocol
```
- 컴파일러는 이름이 바뀐 선언을 사용 시 오류를 내보낼 때 새 이름을 표시하여 보내준다.
