# <b> hugging, resistance </b>
AutoLayoutPriority이다.  
Content hugging과 Compression resistance로 나뉜다.

<br>

<hr>

<br>

## <b> intrinsicContentsize </b>
view 자체의 본질의 크기  
이 크기가 존재함으로 UILabel, UIButton등등 기본적으로 제공되는 view들이 width와 height를 가질 수 있다.  

각각 width와 height에는 제약이 걸려있다.
- <b> Content hugging </b> : 최대 크기에 대한 제한
- <b> Compression resistance </b> : 최소 크기에 대한 제한

이걸 다른 뜻으로 해석해보면
- <b> Content hugging </b> : 주어진 크기보다 작아질 수 있다.
- <b> Compression resistance </b> : 주어진 크기보다 커질 수 있다.

<br>

<hr>

<br>

## <b> Content hugging </b>
상대적으로 작아지려고 하는 세기  
주어진 크기보다 작아짐의 우선순위 수치가 클 수록 먼저 작아지려고 한다.

aLabel hugging = 249, bLabel hugging = 251일 때, bLabel이 더 작아지려고 한다!

<br>

<hr>

<br>

## <b> Compression resistance </b>
상대적으로 커지려고 하는 세기  
둘 다 길어서 view를 넘어가는 경우 어느 Label을 우선순위로 짤라야 하는지 우선순위를 정할 수 있다.  

hugging으로는 해결할 수 없는 부분 -> 길기 때문에 어느 쪽이 작아지든 다 보여줄 수 없다!  
어느 것을 먼저 보여줄지 정해야 한다.

<br>

<hr>

<br>

## <b> 그럼 언제 구분해서 사용? </b>
<b> Content hugging </b> : 공간이 남을 때 어떤 것을 줄이고 늘릴 것인지 (수치가 높을 수록 줄어듬)  
<b> Compression resistance </b> : 공간이 부족할 때 어떤것을 줄이고 늘릴 것인지 (수치가 높을 수록 늘어남)  
