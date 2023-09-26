# <b> MVI </b>
Model + View + Intent  
아키텍처 패턴이다.  
단방향 데이터 흐름을 제공한다.

<br>
<hr>
<br>

## <b> Model </b>
- 화면에 보여질 데이터를 가지고 있다.
  
- 앱의 상태를 나타내는 데이터 모델이다.
  
- Intent로부터 데이터를 받아 UI로 보여주기 위해 준비하고, 현재 상태(가장 최근 데이터)를 가진다.
  
- 항상 View의 현 상태 (State = Model)을 유지한다.
  
- View를 참조한다.
  
<br>
<hr>
<br>

## <b> View </b>
Model을 참조하여 데이터를 보여준다. 

- 전달받은 Model(상태)로 UI를 제공한다.

- Intent를 참조한다.

<br>
<hr>
<br>

## <b> Intent </b>
유저의 Action에 대한 핸들링, 라이프 사이클에 따른 실행등을 담당한다.

- View에서 event를 받아 business logic을 실행한다.

- Model을 참조한다.

<br>
<hr>
<br>

## <b> Container </b>
Intent와 Model에 대한 참조를 관리하고 접근성을 제공해주는 역할을 한다.

- View생성 시 Container를 포함하여 생성한다.

<br>
<hr>
<br>

## <b> 장단점 </b>

### <b> 장정 </b>
- 데이터의 흐름이 한 방향으로 정해져 있어 흐름을 이해하고 관리하기 쉽다.

- 상태 문제 (부수 효과)발생 가능성이 적다.

### <b> 단점 </b>
- 다른 MV*에 비해 러닝 커브가 높다.

- 작은 변경이 생겨도 Intent를 통해야 하기 때문에, 작은 앱에서도 최소한의 Intent와 Model을 가져야 한다.
