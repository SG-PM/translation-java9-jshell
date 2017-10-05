# 2장. 스니펫(Snippets)

JShell은 자바 문(statements), 변수 정의, 메서드 정의 및 클래스 정의, 임포트 문 및 식(expression)을 처리할 수 있습니다. JShell이 수용하는 이러한 코드 조각을 스니펫(snippet)이라고 합니다.

- 주제
  - 스니펫 실행하기
  - 정의 변경
  - Forward References
  - 예외(Exceptions)
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

이름이 지정된 변수가 없는 식(expression)이 입력된다면, 다음에 값을 참조하는 목적으로 스크래치 변수[^1]가 생성되고 결과가 저장됩니다. 다음 예제는 식과 메서드 실행 결과를 저장하는 스크래치 값을 설명합니다. 그리고 이 예제에서 스니펫을 완료하기 위해서는 한 줄 이상의 입력이 필요할 때 사용되는 연속 프롬프트 (...>)를 볼 수 있습니다.

> 역자주: 스크래치 변수(Scratch variable)
> 의미있는 값을 갖지 않고 그때그때 상황에 따라 값들을 잠시 보관해 두기 위한 변수로, 대개 보유한 값이 얼마 후에 의미가 없어지거나 삭제됨.


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

## 정의 변경

코드를 실험하면서 변수, 메서드 및 클래스 정의가 의도한 겻과 다르게 동작하는 경우가 있습니다. 이러한 정의는 새로운 정의를 입력으로 쉽게 변경됩니다. 새로 입력된 정의는 이전 정의를 덮어씁니다.

변수, 메서드 및 클래스의 정의를 변경해야 한다면, 단순히 새로운 정의를 입력하면 됩니다. 예를 들어서 앞에 "스니펫 실행하기" 절에서 정의한 twice 메서드는 다음 예제에서 새로운 정의로 변경됩니다.

```
jshell> String twice(String s) {
   ...>    return "Twice:" + s;
   ...> }
|  modified method twice(String)

jshell> twice("thing")
$7 ==> "Twice:thing"
|  created scratch variable $7 : String
```

앞에서 처럼 "__생성된 메서드(created method)__"로 표시하는 대신 피드백에 "__수정된 메서드(modified method)__"로 표시됩니다. 이 메시지는 정의가 변경되었지만, 변경된 메서드가 이전과 동일한 서명을 가지므로 기존의 사용법이 계속 유효함을 나타냅니다.

호화되지 않는 방식으로 정의를 변경할 수도 있습니다. 다음 예제는 변수 __x__ 타입이 __int__에서 __String__ 으로 변경되었음을 보여줍니다.

```
jshell> int x = 45
x ==> 45
|  created variable x : int

jshell> String x
x ==> null
|  replaced variable x : String
|    update overwrote variable x : int
```

변수 x의 타입 변경에 대해서, 피드백은 "__replaced__"로 표시 됩니다.

### 피드백 레벨 변경

앞에서 JShell은 자세한 설명을 제공하는 verbose 모드로 실행되었습니다. "__/set feedback__" 명령으로 출력 양과 형식 설정을 변경할 수 있습니다. (예 : /set feedback consice) 주로 다른 창에서 코드를 복사하여 JShell에 코드를 붙여 넣기 방식으로 사용할 경우 프롬프트가없고 오류 피드백 만을 제공하는 모드를 선호 할 것 입니다. 그렇다면 "__/set feedback silent__" 명령을 입력하십시오.

## Forward References (사전 참조)

JShell에서 메소드 정의는 아직 정의되지 않은 메서드, 변수, 클래스를 참조할 수 있습니다. 이러한 기능은 탐색적인 프로그래밍 지원과 프로그래밍의 일부 형식이 이 기능을 필요로 하기 때문에 만들어 졌습니다.

예를 들어, 구의 볼륨에 대한 메소드를 정의하려면 다음 수식을 메소드 볼륨으로 입력 할 수 있습니다.

```
jshell> double volume(double radius) {
   ...>    return 4.0 / 3.0 * PI * cube(radius);
   ...> }
|  created method volume(double), however, it cannot be invoked until variable PI, and method cube(double) are declared
```

앞 예제에서 JShell은 메소드 정의를 허용하지만, 아직은 완전히 정의된 것이 아니라는 점을 알립니다. 이 메소드 정의는 참조될 수는 있지만, 실행을 시도한다면 필요한 모든 요소가 정의 될 때까지는 실패합니다.

```
jshell> double PI = 3.1415926535
PI ==> 3.1415926535
|  created variable PI : double

jshell> volume(2)
|  attempted to call method volume(double) which cannot be invoked until method cube(double) is declared

jshell> double cube(double x) { return x * x * x; }
|  created method cube(double)
|    update modified method volume(double)

jshell> volume(2)
$5 ==> 33.510321637333334
|  created scratch variable $5 : double
```

필요한 모든 정의가 완료되면, volume 메서드는 정상적으로 작동합니다.

volume 메서드를 이용하여 호환되지 않는 교체를 설명하겠습니다. 예를 들어 PI의 정밀도를 변경하기위해서 다음 예제와 같이 새로운 값을 입력하였습니다.

```
jshell> BigDecimal PI = new BigDecimal("3.141592653589793238462643383")
PI ==> 3.141592653589793238462643383
|  replaced variable PI : BigDecimal
|    update modified method volume(double) which cannot be invoked until this error is corrected:
|      bad operand types for binary operator '*'
|        first type:  double
|        second type: java.math.BigDecimal
|          return 4.0 / 3.0 * PI * cube(radius);
|                 ^------------^
|    update overwrote variable PI : double
```

새롭게 정의된 PI는 volume 메서드 정의와 타입이 호환되지 않습니다. 현재 JShell은 verbose 모드로 동작하기 때문에, 이 변경으로 영향을 받는 다른 정의에 대한 정보를 출력합니다. 이 예제는 비호환성을 설명하는 대표적인 사례입니다. verbose 모드는 업데이트 정보를 출력하는 미리 정의된 유일한 피드백 모드입니다. 다른 피드백 모드에서는 해당 코드가 실행될때까지 경고를 출력하지 않습니다. 이러한 모드 설정은 업데이트 부하를 방지하는 목적입니다. 사전 정의 된 모든 모드에서 volume 메서드를 실행하면 에러가 출력됩니다.

```
jshell> volume(2)
|  attempted to call method volume(double) which cannot be invoked until this error is corrected:
|      bad operand types for binary operator '*'
|        first type:  double
|        second type: java.math.BigDecimal
|          return 4.0 / 3.0 * PI * cube(radius);
|                 ^------------^
```

## 예외(Exceptions)

예외 역추적(Backtrace)에서 피드백은 예외가 발생한 스니펫과 스니펫 내부의 위치를 출력합니다.

JShell에 입력된 코드의 위치코드 단편 내의 위치를 ​​식별합니다.

JShell에 입력 된 코드의 위치는 "__#ID:line-number__" 형식으로 출력됩니다. 여기서 스니펫 ID는 / list 명령으로 확인할 수 있는 숫자입니다. line-number는 스니펫의 행 번호입니다. 다음 예제에서 스니펫 1에서 예외가 발생한 위치는 devide 메서드의 두번째 행입니다.

```
jshell> int divide(int x, int y) {
   ...> return x / y;
   ...> }
|  created method divide(int,int)

jshell> divide(5, 0)
|  java.lang.ArithmeticException thrown: / by zero
|        at divide (#1:2)
|        at (#2:1)

jshell> /list

   1 : int divide(int x, int y) {
           return x / y;
       }
   2 : divide(5, 0)
```

## 스니펫 텝 자동 완성

When you enter snippets, use the Tab key to automatically complete the item. If the item can’t be determined from what was entered, then possible options are provided.

For example, if you entered the volume method from Forward References, then you can enter the first few letters of the method name, and then press the Tab key to complete the entry:

```
jshell> vol<Tab>
```

The input changes to the following:

```
jshell> volume(
```

If the item can be completed in more than one way, the set of possibilities is displayed:

```
jshell> System.c<Tab>
class                 clearProperty(        console()             currentTimeMillis()

jshell> System.c
```

Any common characters are added to what you entered, and the cursor is placed at the end of the input so that more can be entered.

When you are at a method call's open parenthesis, pressing Tab shows completion possibilities with the parameter types:

```
jshell> "hello".startsWith(<Tab>
Signatures:
boolean String.startsWith(String prefix, int toffset)
boolean String.startsWith(String prefix)

<press tab again to see documentation>

jshell> "hello".startsWith(
```

Pressing Tab again shows a plain-text version of the documentation for the first method.

```
jshell> "hello".startsWith(<Tab>
boolean String.startsWith(String prefix, int toffset)
Tests if the substring of this string beginning at the specified index starts with the
specified prefix.

Parameters:
prefix - the prefix.
toffset - where to begin looking in this string.

Returns:
true if the character sequence represented by the argument is a prefix of the substring of this
          object starting at index toffset ; false otherwise. The result is false if toffset is
          negative or greater than the length of this String object; otherwise the result is
          the same as the result of the expression
                    this.substring(toffset).startsWith(prefix)


<press tab to see next documentation>

jshell> "hello".startsWith(
```

## 스니펫 변환

JShell makes it easy to import a needed class when it is first referenced and convert an expression to a variable declaration using keyboard shortcuts.

When you enter an identifier that isn’t imported yet, press Shift+Tab i immediately after the identifier to see the options that enable you to add the import to your session:

```
jshell> new JFrame<Shift+Tab i>
0: Do nothing
1: import: javax.swing.JFrame
Choice: 1
Imported: javax.swing.JFrame

jshell> new JFrame
```

Enter the number of the option you want. More than one import option could be provided.

You can convert an expression to a variable declaration by pressing Shift+Tab v after you enter the expression. The expression becomes the initial value of the variable declaration, and the type of the expression becomes the type of the variable. After you press Shift+Tab v, the cursor, which is indicated by a vertical bar (|) in the example, is placed in the line where you need to enter the variable name:

```
jshell> new JFrame("Demo") <Shift+Tab v>
jshell> JFrame | = new JFrame("Demo")
```

> __Note__
The expression must be valid or the transformation request is ignored. In the example, the import of JFrame is required before the variable transformation.

To complete the previous example, enter the variable name frame at the cursor and press Enter:

```
jshell> JFrame frame = new JFrame("Demo")
frame ==> javax.swing.JFrame[frame0,0,0,0x0,invalid,hidden, ... tPaneCheckingEnabled=true]
|  created variable frame : JFrame

jshell>
```

Sometimes the result type of the expression isn’t imported yet. In that case, Shift+Tab v offers to both import and create the variable, as shown in the following example:

```
jshell> frame.getGraphics() <Shift+Tab v>
0: Do nothing
1: Create variable
2: import: java.awt.Graphics. Create variable
Choice: 2
Imported: java.awt.Graphics

jshell> Graphics | = frame.getGraphics()
```

To complete the previous example, enter the variable name gc at the cursor and press Enter:

jshell> Graphics gc = frame.getGraphics()
|  created variable gc : JFrame

jshell>

----
[이전 페이지](./1_introduction_to_jshell.md)
[다음 페이지](./3_comments.md)
