# 1장. JShell 소개

Java Shell(JShell)은 Java 프로그래밍 언어를 학습과 Java 코드를 프로토 타이핑하기위한 대화식 도구입니다. JShell은 선언, 명령문 및 표현식을 입력 할 때이를 평가하고 결과를 즉시 표시하는 REPL (Read-Evaluate-Print Loop)입니다. 이 도구는 명령 행에서 실행됩니다.

- 주제
  - JShell는 왜 필요한가?
  - JShell 시작하고 종료하기

JShell의 추가 정보는 __Java Platform, Standard Edition Tool Reference__ 문서의 [jshell](https://docs.oracle.com/javase/9/tools/jshell.htm#JSWOR-GUID-C337353B-074A-431C-993F-60C226163F00) 절을 참조하시기 바랍니다.

## JShell는 왜 필요한가?

JShell을 사용하면 한 번에 프로그램 요소 하나를 입력하고, 즉시 실행 결과를 확인할 수 있습니다. 필요할 경우에 프로그램 요소를 수정할 수 있습니다.

자바 프로그램은 일반적으로 다음 프로세스를 통해서 개발됩니다.

- 완전한 프로그램 개발
- 프로그램 컴파일 및 에러 수정
- 프로그래 실행
- 프로그램 실행 중 오류 파악
- 프로그램 수정
- 지금까지 개발 절차 반복

자바 프로그램을 개발할 때, JShell 사용하면 코드 실행과 옵션 탐색이 매우 편리해집니다. JSShell의 세션에서 개별적인 문(Statement)을 실행하고 테스트할 수 있고, 메서드의 다양한 옵션을 시험해볼 수 있으며, 익숙하지 않은 API로 실험할 수 있습니다. JShell이 IDE를 대체하지는 않습니다. 프로그램을 개발할 때, JShell에 코드를 붙여넣고 시험할 수 있습니다. JShell에서 정상적으로 동작하는 코드가 완성되면, JShell의 코드를 복사하여 프로그램 편집기 및 IDE에 붙여넣는 방식으로 작업합니다.

## JShell 시작 및 종료

JShell은 JDK 9에 포함되어 있습니다. JShell을 시작하기 위해서는 터미널에 jshell 명령을 입력해야 합니다.

JShell을 사용하기 위해서는, 사용중인 컴퓨터에 JDK 9이 설치되어 있어야 합니다. __java-home/jdk-9/bin__ 디렉터리가 PATH 환경 변수에 설정되어 있다면, 디렉터리 위치와 상관없이 jshell을 실행할 수 있습니다.

다음 예제 코드는 jshell를 실행하고 JShell로 부터 결과를 받는 상태를 설명합니다. __%__ 다음에 코드가 사용자가 입력한 명령입니다.

```
% jshell
|  Welcome to JShell -- Version 9
|  For an introduction type: /help intro

jshell>
```

이 문서의 모든 예제는 verbose 모드(상세정보 출력 모드)로 실행한 결과입니다. 이 문서를 실습할 때 Verbose 모드를 사용하는 것을 추천합니다. Verbose 모드를 사용하면 예제와 동일한 결과를 확인할 수 있습니다. jshell에 익숙해지면 일반 모드 혹은 간결 모드로 전환하여 jshell을 실행하는 것이 좋습니다.

JShell을 Verbose 모드로 실행하는 용도로 -v 옵션을 사용합니다.

```
% jshell -v
```

JShell 세션을 종료할 때는 ```/exit```을 입력합니다.

```
jshell> /exit
|  Goodbye
```
