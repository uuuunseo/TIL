# <b> LazyStack </b> 
StackView의 일종으로 아이템들이 화면에 렌더링 되는 순간에 생성된다.  
미리 생성해 놓지 않아 메모리를 낭비하지 않는다.

<br>
<hr>
<br>

## <b> LazyVStack </b>
- 세로로 늘어나는 (스택으로 쌓이는) 하위 View들을 필요한 만큼 추가할 수 있는 View
```Swift
ScrollView {
    LazyVStack(alignment: .leading) {
        ForEach(1...10, id: \.self) {
            Text("Row \($0)")
        }
    }
}
```

<br>
<hr>
<br>

## <b> LazyHStack </b>
-가로로 늘어나는 (스택으로 쌓이는) 하위 View들을 필요한 만큼 추가할 수 있는 View
```Swift
ScrollView(.horizontal) {
    LazyHStack(alignment: .top, spacing: 10) {
        ForEach(1...100, id: \.self) {
            Text("Column \($0)")
        }
    }
}