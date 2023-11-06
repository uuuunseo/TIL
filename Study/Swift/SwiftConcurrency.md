# <b> SwiftConcurrency </b>
비동기 프로그래밍을 지원하기 위한 도구
코드를 간결하고 효율적으로 작성할 수 있게 도와준다.

## <b> 동작 방식 </b>

### Structured Concurrency:
- Swift Concurrency는 구조적 동시성을 지원한다.
  - 비동기 작업 간의 종속성을 명시적으로 관리하여 프로그램의 실행 흐름을 제어하는 방법
   
- async let 구문을 사용하여 여러 비동기 작업을 동시에 실행
  - await를 사용하여 해당 작업들이 완료될 때까지 대기 할 수 있다.

### <b> Actor </b>
- 동시성을 위한 새로운 개념으로 도입
  - 동시에 실행되는 여러 작업에 안전하게 접근할 수 있는 독립된 단위

- 데이터를 보호하고, 동기화 없이 안전하게 공유 상태를 업데이트 할 수 있다.
  - Actor메서드는 자동으로 스레드에 안전하게 실행된다.

- actor 키워드를 사용하여 Actor를 정의한다.
  - 다른 코드에서는 해당 Actor의 메서드와 속성에 await를 사용하여 접근할 수 있다.

### <b> Async / Await </b>
- 가장 중요한 키워드이다.
  - async : 비동기 작업을 선언하는 데 사용
  - await : 비동기 작업이 완료될 때까지 기다리는데 사용

- async 키워드로 선언된 함수는 비동기 작업을 반환
- await 키워드로 해당 작업이 완료될 때까지 기다릴 수 있다.
  - 이를 통해 비동기 코드를 동기 코드처럼 작성할 수 있다.

### <b> Task </b>
- 비동기 작업의 실행을 나타내는 타입
- 비동기 작업을 생성하고, 실행중인 작업을 취소하거나 대기하고 있는 작업을 확인 가능

## <b> 사용방법 </b>
async 키워드를 정의하는 함수에 붙여야 한다.
함수를 호출하는 구문에서 await라는 키워드를 사용한다.

```Swift
func tenSecondsWaitFunction() async throws -> Int {
  try await Task.sleep(for: .second(10))
  return 10
}

// async 함수가 아닐 때 -> Task 키워드를 사용해주어야 한다.(사용하지 않으면 오류!)

func nomalFunction() {
  Task {
    try await tenSecondsWaitFunction() 
  }
}

// async 함수에서 호출할 때

func asyncFunction() async throws {
  try await tenSecondsWaitFunction()
}
```

## <b> Swift Concurrency 원리 </b>

### <b> 작동 원리 </b>
await와 같은 함수가 작동될 때 중단되고 쓰레드의 제어를 포기한다.
함수에게 쓰레드 제어가 다시 돌아가는 것 대신, 시스템에게 쓰레드 제어권을 제공한다.

함수는 중단 되어있고, 시스템이 위임된 수많은 Task중 가장 중요한 작업을 시스템이 선변해서 우선적으로 처리한다. 


