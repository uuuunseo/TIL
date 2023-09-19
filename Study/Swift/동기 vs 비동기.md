# <b> 비동기 async/ 동기 sync </b>
메인 스레드가 기다리느냐 안 기다리느냐의 차이

<br>
<hr>
<br>

## <b> 비동기, async </b>

```swift
DispatchQueue.global().async {
  // task1
}
```

- global dispatch queue에 작업을 비동기적으로 보낸다.

- 메인스레드에서 global dispatch queue에 task1을 보낸 후 해당 작업이 끝나는 여부에 관계없이 바로 다음 작업을 실행한다.
  
- task1이 끝나는 시점은 swift에서 클로저를 통해 알려준다.
    - completionHandler 또는 completion

<br>
<hr>
<br>

## <b> 동기, sync </b>

```swift
DispatchQueue.global().sync {
  // task1
}
```

- 메인 스레드가 task1을 dispatch queue에 보내고 task1이 끝날 때까지 기다린 후에 다음 작업을 실행한다.
  
- 실제로는 동기적으로 코드를 짜더라도 메인스레드에서 작업을 수행한다.

<br>

### <b> 비동기 처리가 필요한 이유 </b>

```swift
URLSession.shared.dataTask(with: request) { (data, response, error) in

}
```

- 시간이 절약된다!
  
- 시간이 많이 드는 작업의 대부분은 서버와의 통신이기 때문에 네트워크와 관련된 작업들은 내부적으로 비동기적으로 구현이 되어있다.
  
- URLSession → 내부적으로는 다른 스레드를 사용하며 비동기적으로 구현되어있다.