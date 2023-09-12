# <b> LazyGrid </b>

<b> Grid </b> : 2차원의 행과 열을 구성하는 레이아웃이라는 뜻

<b> Lazy </b> : 필요할 때만 해당 subView를 정렬해 생성한다.

2차원의 행과열의 레이아웃으로 정렬되고 세로 스크롤이 되는것이 특징

<br>
<hr>
<br>

## <b> LazyVGrid </b>

- 열이 우선되게 뷰가 정렬되고 쌓이는 컨테이너 뷰
- 행이 무수히 증가해 구성될 수 있고, 열에 최대 몇개의 View가 담길지 특정하게 지정가능
- GridItem타입을 이용해 인스턴스를 만들 수 있다.
    
    ```swift
    import SwiftUI
    
    struct ContentView: View {
      let columns = [GridItem(.flexible()), GridItem(.flexible())]
      let cute = ["cat", "hamster", "squirrel", "quokka"]
      
      var body: some View {
        LazyVGrid(columns: columns) {
          ForEach(cute, id: \.self) { cute in
            RoundedRectangle(cornerRadius: 10)
              .frame(width: 150, height: 100)
    					.overlay(Text(cute))
          }
        }
        .padding()
      }
    }
    
    ```
    
<br>
<hr>
<br>

## <b> LazyHGrid </b>

- 수평으로 늘어나는 그리드에 SubView를 정렬하여 나타낼 수 있는 컨테이너 뷰

- 열은 무수히 증가해 구성될 수 있고 행에 최대 몇개의 View가 담길지는 특정하게 지정할 수 있다.

    ```swift
    import SwiftUI

    struct ContentView: View {
    let rows = [GridItem(.flexible()), GridItem(.flexible())]
    let cute = ["cat", "hamster", "squirrel", "quokka"]
  
      var body: some View {
        LazyVGrid(rows: rows) {
            ForEach(cute, id: \.self) { cute in
                RoundedRectangle(cornerRadius: 10)
                .frame(width: 150, height: 100)
			    .overlay(Text(cute))
            }
        }
        .padding()
        }
    }
    ```

Horizontal이 많이 쌓일테니 스크롤뷰로 감싸 주는 방법도 많이 사용된다. (주로 배너, 앨범)

<br>
<hr>
<br>

### <b> GridItem </b>

- 그리드의 행 혹은 열에 대한 디스크립션이다.
  
- Grid를 만들 때 GridItem 타입의 컴포넌트를 만들어야 한다.
  
- 초기화 시 넘겨줄 수 있는 파라미터는 alignment, spacing, size가 있다.

- size는 Size enum 타입으로 케이스가 선언되어있다.  
  <br>

    <b> adaptive(minimum: CGFloat, maximum: CGFloat) </b>  
    최소값과 최대값을 정하고 이 사이의 사이즈로 가장 많이 배치 가능하게 할 때 사용

<br>

  - **flexible(minimum: CGFloat, maximum: CGFloat)**  
    최소/ 최대 값을 정해두고 뷰 크기에 따라 사이즈를 조절할 수 있다.  
    인자에 아무것도 주어지지 않는다면 해당 뷰의 크기를 아이템의 수로 나눠 계산해 그려준다.

<br>

  - **fixed(CGFloat)**
    고정된 사이즈로 아이템을 지정해준다.

  - Spacing도 줄 수 있다.
    ```Swift
    GridItem(.flexible(), spacing: 50)
    ```