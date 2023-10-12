# <b> Navigation </b>

- 원래는 NavigationView가 있었는데  WWDC22에서 NavigationView가 deprecated 되었다.
  
- 그리고 NavigationStack/NavigationSplitView가 나왔다.

<br>

```
🚫 NavigationStack/NavigationSplitView는 iOS16+ 부터 사용할 수 있기 때문에   
Deployment Target이 iOS 16+ 이상인 경우에만 진행하는 것이 좋다.
```

<br>
<hr>
<br>


# <b> NavigationStack </b>

RootView를 표시하고, Root View에 대한 추가 (additional) View를 제공할 수 있는 View

- 항상 NavigationLink와 .navigationDestination(for:) 수정자를 항상 같이 사용해야한다.
  
- Stack은 항상 최근에 추가한 View를 보여주며 Root View는 제거되지 않은 특징을 가지고 있다.
  
<br>
<hr>
<br>

## <b> NavigationLink </b>

- 눌렀을 때 원하는 View가 나오게 하는 역할이다.
  
- NavigationLink만 있다고 해서 다음 View로 넘어가는 것은 아니고 .navigationDestination(for:) 수정자를 사용해야 한다.

<br>
<hr>
<br>

### <b> navigationDestination </b>

- 특정 종류의 데이터를 제공할 때 Stack이 가리키는 View를 보여주는 역할을 한다.
  
- View를 데이터 유형과 연결하고 동일한 종류의 데이터 인스턴스를 제공하는 NavigationLink를 초기화 하게 된다.

<br>
<hr>
<br>

## <b> 실행과정 </b>

1. 모든 NavigationStack은 Stack이 표시하는 모든 데이터를 나타내는 경로를 추적한다. (root View에 있는 경우 Path는 비어있게 된다.)
   
2. Stack은 내부 또는 Stack에 push된 View 내부에서 선언된 모든 .navigationDestinations(모든 탐색대상)을 추적
   
3. 섹션에 있는 목록을 누르게 되면 해당 value가 path에 추가된다.
   
4. 자연스럽게 NavigationStack은 path값에 대상을 mapping하여 Stack에서 push할 View를 결정하게 된다.
   
5. 해당 DetailView를 보고 이전 View로 돌아가게 되면 NavigationStack이 path와 pushed views에 있는 최근 항목인 view를 제거하게 된다.

## Navigation State

- NavigationStack에는 기본적으로 State를 관리하여 Stack에 있는 View를 추적하게 되는 데 이걸 직접 사용자가 관리 할 수 있도록 한다.
  
- Stack에 있는 View를 맘대로 순서를 바꾸거나 제거할 수 있다!
  
- Binding을 통해 여러 경로로 연결이 가능하게 됐는데 Binding을 하기 위해선 State를 추가해 주어야 한다.

<br>
<hr>
<br>

# <b> NavigationSplitView </b>

2분할 또는 3분할 되는 View를 만들 때, 1개 또는 2개의 Sidebar를 만들 때 사용하는 View

- 기종 및 윈도우 영역에 따라 navigationStack 형태로 자동 변환된다.
  
- 2분할은 init(sidebar:detail:) 사용
    
    ```swift
    @State private var employeeIds: Set<Employee.ID> = []
    
    var body: some View {
        NavigationSplitView {
            List(model.employees, selection: $employeeIds) { employee in
                Text(employee.name)
            }
        } detail: {
            EmployeeDetails(for: employeeIds)
        }
    }
    ```
    
<br>

- 3분할은 init(sidebar:, content:, detail) 사용
    
    ```swift
    @State private var departmentId: Department.ID? // Single selection.
    @State private var employeeIds: Set<Employee.ID> = [] // Multiple selection.
    
    var body: some View {
        NavigationSplitView {
            List(model.departments, selection: $departmentId) { department in
                Text(department.name)
            }
        } content: {
            if let department = model.department(id: departmentId) {
                List(department.employees, selection: $employeeIds) { employee in
                    Text(employee.name)
                }
            } else {
                Text("Select a department")
            }
        } detail: {
            EmployeeDetails(for: employeeIds)
        }
    }
    ```

    <br>
    
- <b> columnVisibility </b> : 사이드바 표시 유무를 저장하고 접근하기 위해 사용한다.
  
    - State 변수를 선언하여 Binding으로 전달한다.
  
    - NavigationStack 형태로 표시되는 경우 무시 된다.
  
    - 4개의 static 타입 프로퍼티가 있다.

        - <b> automatic </b> : 해당 기종 및 윈도우 영역에 따른 기본값을 사용
  
        - <b> all </b> : 모든 사이드바를 표시

        - <b> doubleColumn </b> : 하나의 사이드바만 표시한다. → 3분할 View에서 첫 번째 사이드바는 표시되지 않는다.
  
        - <b> detailOnly </b> : 사이드바를 표시하지 않는다.
        
<br>
<hr>
<br>

### <b> sidebar 인자 또는 content 인자의 클로저의 사용법 </b>

- selection 인자를 받는 List + value 인자를 받는 NavigationLink

```swift
var categories : [Category]

// NavigationPath를 사용하면 다양한 타입을 단일 State 변수에 저장하여 path로 사용할 수 있다.
@State var selectedCategory : Category? = nil
@State var selectedItem : Item? = nil

var body: some View {
    NavigationSplitView {
        List(categories, selection: $selectedCategory) { category in
            NavigationLink(category.title, value: category)
            // 선택시 List의 selection 인자에 value 인자값을 대입한다.
        }
    } content: {
        List(selectedCategory?.items ?? [], selection: $selectedItem) { item in
            NavigationLink(item.title, value: item)
        }
    } detail: {
        Text(selectedItem?.title ?? "nothing selected")
    }
}
```
<br>

- NavigationStack 및 NavigationSplitView는 서러의 클로저 내에 중첩해서 사용할 수 있다.

<br>
<hr>
<br>

## <b> 관련 수정자 </b> 

```swift
func navigationSplitViewStyle<S>(_ style: S) -> some View where S : NavigationSplitViewStyle
func navigationSplitViewColumnWidth(_ width: CGFloat) -> some View
func navigationSplitViewColumnWidth(min: CGFloat? = nil, ideal: CGFloat, max: CGFloat? = nil) -> some View
```
<br>

위 수정자들로 Sidebar의 스타일을 지정하거나, Sidebar 및 detail View의 폭을 지정할 수 있다.

NavigationSplitViewStyle 프로토콜은 3개의 static 타입 프로퍼티를 가진다.

- <b> automatic </b> : 현재 맥락(기기 크기)에 기반하여 자동으로 적합한 스타일로 표시한다.
  
- <b> balanced </b> : Sidebar를 띄울 때 detail View의 영역을 줄여 공간을 확보한다.
    - Sidebar가 detailView를 가리지 않는다.
  
- <b> prominentDetail </b> : Sidebar를 띄울 때 detail View의 영역을 조절하지 않고 오버레이한다.
    - Sidebar가 detailView를 가린다.
  
- 스타일을 커스텀 할 수 있도록 <b>makeBody(configuration: )</b> 함수, NavigationSplitViewStyleConfiguration 구조체를 제공하지만, 구조체 내에 공개된 프로퍼티는 없다.

- <b> navigationSplitViewColumnWidth(_:)</b>를 사용하여 사이드바의 폭을 특정 값으로 고정할 수 있다.

- <b>navigationSplitViewColumnWidth(min:, ideal:, max: )</b>를 사용하여 사이드바의 폭을 윈도우 크기에 기반하여 유연하게 조정되도록 할 수 있다.