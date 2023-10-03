# <b> Combine </b>
비동기 이벤트를 핸들링할 수 있게하는 Apple의 순정 Framwork

<br>
<hr>
<br>

## <b> Publisher </b>
이벤트 또는 값을 전달하는 존재

<br>
<hr>
<br>

## <b> Subscriber </b>
Publisher가 내보낸 이벤트 또는 값을 수신하는 존재

<br>
<hr>
<br>

## <b> 흐름 </b>
먼저 Subscriber가 Publisher를 Subscribe하기 전까지 Publisher는 대기 상태로 존재한다. 
1. Publisher의 subscribe(_ :)메서드의 전달인자로 Subscriber prtocol을 준수하는 인스턴스를 전달하여 Publiser와 Subscriber를 연결한다.
   
2. Subscriber의 receive(subscription:)메서드는 subscribe요청을 인지하고 Publiser로 부터 Subscription인스턴스를 전달받는다. (Publisher-Subscriber 연결 완료)

3. Subscriber는 전달 받은 Subscription의 request(_:) 메서드를 통해 Publisher의 값을 전달하라고 요청한다. (Publisher는 Subscriber에게 값과 오류 타입을 함께 전달한다. - 오류가 발생하지 않으면 Never오류 타입 전달)

4. Subscriber의 receive(_ :)메서드는 Publisher에게 전달 받은 값을 처리한다.

5. 더이상 Subscriber에게 전달할 값이 없으면 receive(completion:)메서드를 통해 completion, 혹은 오류를 전달받는다.

