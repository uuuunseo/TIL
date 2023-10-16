# <b> Combine </b>
비동기 이벤트를 핸들링할 수 있게하는 Apple의 순정 Framwork

<br>
<hr>
<br>

## <b> Publisher </b>
하나 혹은 여러 개의 Subscriver 객체에 시간이 흐름에 따라 값을 내보낼 수 있는 타입을 선언하기 위한 프로토콜
- Output, Failure 타입이 제네릭으로 구현되어 있다.
- Future, just, Deferred, Empty, Fail, Record같은 Publisher 프로토콜을 준수하는 Struct, Class들을 구현해두었다.

<br>
<hr>
<br>

## <b> Subscriber </b>
Publisher에게 값을 받을 수 있는 타입을 선언하기 위한 프로토콜이다.
- Input, Failure 타입이 제네릭으로 구현되어 있다.

<br>
<hr>
<br>

## <b> Operator </b>
Publisher를 반환하는 Publisher 프로토콜에 정의된 메서드
- 여러 종류의 Operator를 Combine하여 사용해 Publisher가 내보내는 값을 처리한다.
- Upstream, DownStream이라고 하는 Input, Output을 가지고 있다.

## <b> Subscriotion </b>
Publisher와 Subscriber의 연결을 나타내는 프로토콜
- Publisher + Operator + Subscriber로 이루어진 하나의 작업

## <b> 흐름 </b>
먼저 Subscriber가 Publisher를 Subscribe하기 전까지 Publisher는 대기 상태로 존재한다. 
1. Publisher의 subscribe(_ :)메서드의 전달인자로 Subscriber prtocol을 준수하는 인스턴스를 전달하여 Publiser와 Subscriber를 연결한다.
   
2. Subscriber의 receive(subscription:)메서드는 subscribe요청을 인지하고 Publiser로 부터 Subscription인스턴스를 전달받는다. (Publisher-Subscriber 연결 완료)

3. Subscriber는 전달 받은 Subscription의 request(_:) 메서드를 통해 Publisher의 값을 전달하라고 요청한다. (Publisher는 Subscriber에게 값과 오류 타입을 함께 전달한다. - 오류가 발생하지 않으면 Never오류 타입 전달)

4. Subscriber의 receive(_ :)메서드는 Publisher에게 전달 받은 값을 처리한다.

5. 더이상 Subscriber에게 전달할 값이 없으면 receive(completion:)메서드를 통해 completion, 혹은 오류를 전달받는다.

