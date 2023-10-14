# <b> Sheet & FullScreenCover </b>
ZStack과 Overlay처럼 뷰를 중첩하기 위한 방법이다.

## <b> Sheet </b>
설정한 Bool값이 true일 때 Sheet를 표시한다.
- 화면을 모두 채우지 않는다.
  
- 화면 아래 스크롤을 통해서 이전의 뷰로 돌아갈 수 있다.

```Swift
.sheet(isPresented:, onDismiss:, content:)
```

## <b> FullScreecover </b>
설정한 Bool값에 바인딩 되었을 때 화면을 가능한 많이 덮는 모달 뷰를 표시한다.
  
- 화면 모두를 채운다.

- 바인딩 값을 처리해줘야 이전의 뷰로 돌아갈 수 있다.

```Swift
.fullScreenCover(isPresented:, onDissmiss:, content:)
```

