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

```
% jshell -v
|  Welcome to JShell -- Version 9
|  For an introduction type: /help intro
```

```
jshell> int x = 45
x ==> 45
|  created variable x : int
```

> __주의__
> 완료된 스니펫이 끝에 세미콜론이 
Terminating semicolons are automatically added to the end of a complete snippet if not entered.
