# 2장. 스니펫(Snippets)

JShell은 자바 문(statements), 변수 정의, 메서드 정의 및 클래스 정의, 임포트 문 및 식(expression)을 처리할 수 있습니다. JShell이 수용하는 이러한 코드 조각을 스니펫(snippet)이라고 합니다.

- 주제
  - 스니펫 실행하기
  - 정의 변경
  - Forward References
  - 예외 처리
  - 스니펫 텝 자동 완성
  - 스니펫 변환

## 스니펫 실행하기

JShell에 자바 코드 스니펫이 입력되면 즉시 평가됩니다. 평가 결과, 수행 액션 및 발생한 에러에 대한 피드백이 출력됩니다. 이 섹션의 예제를 사용하여 JShell을 시도해보십시요  

Verbose 옵션으로 JShell을 시작합니다. Verbose 옵션을 사용하면 피드백을 최대로 받을 수 있습니다.

```
% jshell -v
|  Welcome to JShell -- Version 9
|  For an introduction type: /help intro
```
프롬프트에 다음 예제의 문(statement)을 입력하고 출력 결과를 살펴보십시오.

```
jshell> int x = 45
x ==> 45
|  created variable x : int
```
출력된 결과를 읽어보면, 변수 x의 값은 45입니다. verbose 모드일 경우에, 발생한 내용에 대한 설명을 표시합니다. 정보 제공 메시지는 수직 막대로 시작되며, 생성된 변수의 이름과 유형이 모두 표시됩니다.

먼저 결과가 표시됩니다. 변수 x의 값은 45입니다. 자세한 정보 표시 모드에 있기 때문에 발생한 내용에 대한 설명도 표시됩니다. 정보 제공 메시지는 수직 막대로 시작됩니다. 생성 된 변수의 이름과 유형이 모두 표시됩니다.

> __주의__
> 완료된 스니펫이 끝에 세미콜론이 없다면 문(statement) 종료를 표시하는 세미콜론(;)은 자동으로 추가됩니다.


When an expression is entered that doesn't have a named variable, a scratch variable is created so that the value can be referenced later. The following example shows scratch values for an expression and for the results of a method. The example also shows the continuation prompt (...>) that is used when a snippet requires more than one line of input to complete:


[^1]: Scratch variable: 의미있는 값을 갖지 않고 그때그때 상황에 따라 값들을 잠시 보관해 두기 위한 변수로, 대개 보유한 값이 얼마 후에 의미가 없어지거나 삭제됨

  이름이 지정된 변수가없는식이 입력되면 나중에 값을 참조 할 수 있도록 스크래치 변수가 만들어집니다. 다음 예는 표현식 및 메소드 결과에 대한 스크래치 값을 보여줍니다. 이 예제는 또한 코드 조각이 완료 될 때 한 줄 이상의 입력이 필요할 때 사용되는 연속 프롬프트 (...>)를 보여줍니다.
```
jshell> 2 + 2
$3 ==> 4
|  created scratch variable $3 : int

jshell> String twice(String s) {
   ...>    return s + s;
   ...> }
|  created method twice(String)

jshell> twice("Ocean")
$5 ==> "OceanOcean"
|  created scratch variable $5 : String
```

```
jshell> String twice(String s) {
   ...>    return "Twice:" + s;
   ...> }
|  modified method twice(String)

jshell> twice("thing")
$7 ==> "Twice:thing"
|  created scratch variable $7 : String
```

```
jshell> int x = 45
x ==> 45
|  created variable x : int

jshell> String x
x ==> null
|  replaced variable x : String
|    update overwrote variable x : int
```
