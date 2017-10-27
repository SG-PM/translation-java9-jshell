# 3장. 명령

JShell 명령은 JShell 세션에서 입력되며 환경을 제어하고 정보를 표시하는 데 사용됩니다.

주제
- JShell 명령 소개
- JShell 명령의 텝 자동완성
- 명령어 약어

## JShell 명령 소개

JShell 명령은 환경을 제어하고, JShell 세션의 정보를 표시합니다.

JShell 명령은 스니펫과 구분하기 위해서 명령어 앞에 슬래쉬(/)를 붙이는 규칙을 사용합니다.
현재 변수, 메서드와 타입에 대한 정보를 확인하는 용도로 ```/var```, ```/methods```, ```/types``` 명령을 사용합니다.
__```list```__ 명령을 사용하여 입력된 스니펫 목록을 확인할 수 있습니다.
다음 예제에서 이러한 명령의 사용 예를 확인 할 수 있습니다.

```
jshell> /vars
|    int x = 45
|    int $3 = 4
|    String $5 = "OceanOcean"

jshell> /methods
|    twice (String)String

jshell> /list

   1 : System.out.println("Hi");
   2 : int x = 45;
   3 : 2 + 2
   4 : String twice(String s) {
         return s + s;
       }
   5 : twice("Ocean")
```

Notice that the types and values of variables and the type signature of methods are displayed.

JShell has a default startup script that is silently and automatically executed before JShell starts, so that you can get to work quickly. Entries from the startup script aren't listed unless you request them with the /list -start or /list -all command:


```
jshell> /list -all

  s1 : import java.util.*;
  s2 : import java.io.*;
  s3 : import java.math.*;
  s4 : import java.net.*;
  s5 : import java.util.concurrent.*;
  s6 : import java.util.prefs.*;
  s7 : import java.util.regex.*;
   1 : System.out.println("Hi");
   2 : int x = 45;
   3 : 2 + 2
   4 : String twice(String s) {
         return s + s;
       }
   5 : twice("Ocean")
```

The default startup script consists of several common imports. You can personalize your startup entries with the /set start command. For information about this command, enter /help /set start. The /save -start command saves the current startup script as a starting point for your own startup script.

Other important commands include /exit to leave JShell, /save to save your snippets, and /open to enter snippets from a file.

Enter /help for a list of the JShell commands.

## Tab Completion for Commands


Similar to snippet completion, when you enter commands and command options, use the Tab key to automatically complete the command or option. If the completion can’t be determined from what was entered, then possible choices are provided.

The following example shows the feedback when Tab is pressed after the leading slash (/) for commands:

```
jshell> /<Tab>
/!          /?          /drop       /edit       /env        /exit       /help
/history    /imports    /list       /methods    /open       /reload     /reset      
/save       /set        /types      /vars       

<press tab again to see synopsis>

jshell> /
```

Unique completions are done in-place. For example, after you enter /l and press Tab, the line is replaced with /list:

```
jshell> /l<Tab>

jshell> /list
```
