# <b> GCD </b>

iOS에서 멀티코어 프로세서에 코드를 동시에 실행시키게 해주는 프레임워크

- iOS에서 멀티스레드 환경에서 다수의 스레드에 작업을 적절히 분배 시키는 방법
  
- 프로그래머가 Dispatch Queue에 작업을 보내면 그에 따라 스레드를 적절히 생성해서 실행하고 작업이 종료되면 스레드를 제거한다.

```swift
DispatchQueue.global().async {
  //task
}
// global dispatch queue 에 작업을 비동기 적으로 보낸다!
```

- DispatchQueue : iOS에서 동시성 프로그래밍을 돕기 위해 제공하는 Queue
  
- global : DispatchQueue의 종류
  
- async : 비동기

<br>
<hr>
<br>

- 실제로 iOS에서 제공하는 Dispatch Queue의 종류는 세가지이다.
  
- Queue의 종류에 따라 Queue의 특성이 다르기 때문에 작업의 특성, 원하는 일 처리 방식에 따라 Queue를 선택해야 한다.
    - 메인큐
  
    - 글로벌 큐
  
    - 커스텀 (프라이빗) 큐

<br>
<hr>
<br>

### <b> main Queue </b>

- 오직 한개만 존재하며 Serial 특성을 가지고 있다.
  
- Main Queue에 할당된 task는 메인 스레드에서 처리 (UI 업데이트 내용 처리)

```swift
DispatchQueue.main.sync {
// task 1
}
```

- 그러나 위에 같이 작성하면 에러가 발생한다.

- 메인 큐에서 task는 메인 스레드로만 보낸다.
  
- 메인 스레드는 오직 한 개밖에 없다.
  
- 메인 큐에 있는 task들을 다른 곳에 분산시키려고 해도 분산 시킬만한 곳이 없다.
  
- 큐의 특성은 무조건 Serial이 된다. (분산은 Concurrent의 특징)

<br>
<hr>
<br>

## <b> Global Queue </b>

- Concurrent 특성을 가진 Queue
  
- QoS (Quality of Service)에 따라 알맞는 스레드에 나누어 분배된다.

```swift
Dispatch.global(qos: .utility).async {
// task 1
}
```

<br>
<hr>
<br>

### <b> QoS의 종류 </b>

<br>

**userInteractive**

- 사용자와 직접 상호작용하는 UI업데이트, 애니메이션 등의 작업

- 메인 스레드에서 직렬적으로 처리하면 시간이 오래 걸리는 작업드를 userInteractive에서 처리해 바로 동작하는 것처럼 보이게 한다.

<br>

**userInitiated**

- 즉각적인 결과가 필요한 작업
    - ex) 저장된 문서를 여는 작업
  
- userInteractive 보다는 조금 오래 걸릴 수 있고 유저가 어느정도 인지하고 있다.

<br>

**default**

- 일반적인 작업

<br>

**utility**

- 데이터 다운로드와 같이 보통 progress basr와 함께 길게 진행되는 작업

<br>

**unspecified**

- QoS정보가 없음을 나타낸다.

- 거의 사용할 일이 없다.

설정된 qos에 따를 각 queue에 작업들이 분배된다.

- 실제로 우선순위가 더 높은 Queue의 작업들에 더 많은 스레드를 배치한다.

<br>

### <b> Custom Queue </b>

- 프로그래머가 커스텀으로 만드는 큐
  
- 디폴트로 Serial 특성을 가지는 Queue, Concurrent로 설정 가능하다.
  
- Qos 설정 가능

```swift
let customQueue = DispatchQueue(label : "custom", qos: .background, attribute: .concurrent)
```

<br>
<hr>
<br>

## <b> GCD의 필요성 </b>

기존에 멀티 스레드를 사용하려면 개발자가 직접 스레드를 생성하고 관리했어야 했는데 GCD를 사용하면 스레드 생성, 유지, 삭제등에 개발자가 신경쓰고 개입하지 않아도 된다.

<br>

## <b> GCD 사용 시 주의 사항 </b>

### <b> 1. UI업데이트는 메인 스레드에서 처리 해야한다. </b>

- 메인 스레드는 UI 그리는 일을 담당한다.
  
- iOS를 비롯한 모든 OS에서 마찬가지이다.
  
- 이미지 등을 global에서 다운 받아오더라도, 해당 데이터를 UIImageView에 넣어서 UI 업데이트 시켜주는 작업은 main에서 진행해야 한다.

<br>

### <b> 2. 메인 큐에서 다른 큐로 작업을 보낼 때 sync를 사용해선 안된다. </b>

- sync로 보내게 되면 작업을 보내고 완료될 때 까지 기다린다는 의미!
  
- 메인 스레드는 UI를 업데이트 해주어야 하는 역할, 기다릴 수 없고 기다려서는 안된다.
  
- 메인스레드에서는 항상 비동기 async로 작업을 보내야 한다.

<br>

### <b> 3. 현재 작업중인 큐와 동일한 큐에 sync로 작업을 보내선 안된다. </b>

- 각 큐에서 사용하는 스레드는 정해져 있다.
  
- 같은 큐에 작업을 보낸다면 동일한 스레드에 배치될 수 있고, 이 때 sync로 보낸다면 동일한 스레드에 보내진 작업이 끝날 때 까지 보낸 작업도 수행될 수 없는 데드락 상태가 발생할 수 있다!

```swift
DispatchQueue.global().async {
	DispatchQueue.global().sync {
	
	}
}
// TaskA 수행 중 TaskB를 동일한 큐로 sync로 보낸다. -> 
// Thread2에서 TaskA 수행 도중 TaskB가 동일한 큐에 보내진다. ->
// TaskB 역시 동일한 Thread2에 배치 된다면? -> 데드락 발생!!
```

<br>

```swift
//데드락 발생 가능성 있음
DispatchQueue.global().async {
  DispatchQueue.global().sync 
}
//데드락 발생 가능성 없음
DispatchQueue.global(qos: .utility).async {
  DispatchQueue.global().sync 
}
```

- qos가 다르게 설정된다면 동일한 스레드에 배치되지 않는다!

<br>

### <b> 4. 메인 스레드에서 DispatchQueue.main.sync를 사용해선 안된다. </b>

- 메인스레드에서 작업중
- DispatchQueue.main.sync사용시 동일한 메인큐로 보내진다
- sync로 보냈기 때문에 데드락 발생!

<br>

### <b> 5. 객체에 대한 캡처에 주의해야 한다. </b>

- task를 큐에 보낸다는 것은 클로저를 보낸다는 것을 의미한다.
- 객체에 대한 캡처 현상 발생할 수 있게 되고, 자칫하면 retain cycle이 생길 수도 있다.
- weak self를 써서 방지할 수 있다.