<br>

__API_Design_Guidelines - CamelCase__
=====================================

<br><br>

## __CamelCase__

단어가 합쳐진 부분마다 맨 처음 글자를 대문자로 표기하는 방법   
    
- 두 개 이상의 단어가 모인 합성어에서 사용된다.
- 쌍봉낙타의 등과 닮았다고 하여 CamelCase라고 부른다.   
- lowerCamelCase와 UpperCamelCase로 나뉜다.

<br>

----

<br><br>

## __lowerCamelCase__

CamelCase에서, 맨 앞글자를 소문자로 표기하는 것   
* 나머지 뒤에 따라붙는 단어들의 앞글자는 모두 대문자로 표기한다.   
* 함수, 변수, 상수, enum 등을 lowerCamelCase로 작성한다.
```Swift
someVariableName
```

<br>

----

<br><br>

## __UpperCamelCase__

CamelCase에서, 맨 앞글자를 대문자로 표기하는 것   
- PascalCase라고도 불린다.   
- 나머지 뒤에 따라붙는 단어들의 앞글자는 모두 대문자로 표기된다.   
- 파일명, class, struct 등을 UpperCamelCase로 작성한다.   
```Swift
Person, Point, Week
```