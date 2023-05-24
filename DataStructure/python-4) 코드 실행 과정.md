# 파이썬 
## 인터프리터 언어, 컴파일 언어
파이썬은 부분 컴파일 언어이자, 인터프리터 언어이다.

|인터프리터 언어|컴파일 언어|
|-------|--------|
|기계어 변환 과정 없음|모두 기계어로 변환|
|한줄 한줄 해석해서 바로 명령어 실행|기계에 넣고 기계어 코드를 실행|
|빌드 과정 없음| 빌드 과정(소스 파일->실행 파일)에서 시간 소요|
|런타임 상황에서 한줄씩 읽음|런타임 상황에서 이미 소스코드가 변환되어 있음|
|속도 느림|속도 빠름|
|프로그램 수정 간단|수정 후 다시 컴파일 필요|

![image](https://github.com/0sun-creater/2023-CS-Study/assets/54173210/bc5e1aef-f390-46f4-af98-e10eb77789e4)


## 파이썬 코드 실행 과정
`.py` 로 작성된 파이썬 코드는 제일 먼저 **바이트 코드** 로 컴파일 되고, 바이트 코드는 **인터프리터**를 통해 실행된다.
- 바이트 코드는 하드 디스크의 `.pyc' 파일에 저장  (__pycache__ 폴더 안에 생성)
- PVM (Python Virtual Machine) : 인터프리터, 가상 머신
  - VM을 통해 '플랫폼에 독립적'인 장점을 가짐
  - 플랫폼에 독립적 : python, java / 윈도우, 맥, 리눅스 어디서나 번역 및 실행이 가능
  - 플랫폼에 의존적 : c 언어 / 소스 코드자체는 다르지 않지만, 최종 결과물이 윈도우에서는 `.exe` 파일 리눅스에서는 `.out` 파일

![image](https://github.com/0sun-creater/2023-CS-Study/assets/54173210/85c48b3c-cb14-4c5a-b43d-be0905030e79)

## 파이썬의 구현체
파이썬 구현체는 인터프리터 안에 컴파일러를 내장하고 있다.
- CPython
  - 파이썬을 C언어로 구현한 구현체
  - 인터프리터이면서 컴파일러
  - 파이썬 코드를 컴파일해서 bytecode로 바꾸고 인터프리터가 실행
  - `.py` 파일을 실행하면 `.pyc` 파일이 생성 : cpython이 컴파일한 bytecode 가 들어있음
  - GIL(Global interprter lock) 사용
</br>

- PyPy3
  - python 자체로 구현 
  - JIT(Just In Time) 컴파일을 겸비한 인터프리터 : 프로그램을 실행하는 시점에서 필요한 부분을 즉석으로 컴하일하는 방식
  - JIT는 기계어 코드를 생성하면서 그 코드를 캐싱하여, 같은 함수가 여러 번 불릴 때 매번 기계어 코드를 생성하는 것을 방지
  - PyPy 가 Cpython 보다 빠름
</br>

- Jython
  - 파이썬 코드를 java bytecode로 만들어서 JVM 에서 실행될 수 있도록함
  - `.py` 파일을 `.class` 파일로 컴파일

## 파이썬 작동 방식
- Step 1. 파이썬 컴파일러가 소스 코드를 읽는다. 소스코드가 잘 작성 되었는지를 판단하기 위한 문법 오류 검사를 진행한다.
   만약 문법 오류가 발견되었다면, 그 즉시 컴파일 과정을 멈추고 에러 메시지 출력
- Step 2. 에러가 발생하지 않았다면 컴파일러가 소스 코드를 바이트 코드로 변환한다.
- Step 3. 바이트 코드는 PVM에 보내진다. PVM은 바이트 코드를 컴퓨터가 실행할 수 있는 기계어로 한 줄 한 줄 (line by line) 번역한다.
   만약 이 과정에서 에러가 발생하면 모든 것을 멈추고 에러 메시지 출력
python 명령자를 전달함으로써 python interpreter가 trigger되고, source code가 전달된다.  
Python interpreter의 작동 stages는   
> **1. Lexing**
> 전달된 code를 가지고 line을 쪼개 코드를 Token으로 generate  

> **2. Parsing**
Generated token이 parser에게 전달되어 파싱됨  
token을 가지고 Abstract Syntax Tree라는 token(code들)사이의 관계를 나타내는 트리 구조를 만듦  

> **3. Compiling**
Parsed code(Abstract Syntax tree)가 compiler에게 전달되고, compiler가 이 Abstract Syntax Tree를 가지고 Byte code 라는 .pyc 형태의 intermediate language code를 생성됨

  - 자바 소스코드와의 차이점?  
  - 자바코드는 interpreter에게 소스가 전달되기 전에 컴파일러에 의해 컴파일됨. 
  - (compiler가 interpreter outside에 존재함. 파이썬은 인터프리터/컴파일러가 인터프리터 안에 함께 존재해서 performance lag를 줄임)

4) Virtual Machine으로 .pyc가 전달되어 Interpreting 작업 수행  
실제로 interpreting하는 stage. operating system을 simulate함.  
byte code를 machine code로 변환함  
![image](https://github.com/0sun-creater/2023-CS-Study/assets/54173210/046bc01d-e10c-48d3-bc7e-c785b07b3d7c)


### Exception이 raised되면 일어나는 일

1. exception이 handled되기 전까지는 현재 block의 어떤 statements나 코드도 실행되지 않는다.  
2. interpreter는 print-loop를 return 시켜주며, file argument로 파이썬이 시작된 경우에는? terminate한다.  
3. python interpreter는 stack backtrace를 출력한다.
stack-backtrace는 explanation이 담긴 텍스트 블록 집합으로, 예외가 발생한 실행분기에서 활성화되었던 function들의 call을 나타내는 branch 텍스트 블록 집합이다.  

### 출력 방법
traceback 이라는 python의 모듈이 있음.   
파이썬 프로그램의 StackTrace를 추출, format, print하는 표준 인터페이스를 정의  

traceback module은 traceback이라는 Object를 사용하는데, sys.last_traceback이라는 변수에 저장되고 sys.exc_info()라는 함수의 인자로 사용된다고 한다.  

### sys module
파이썬 런타임에 interpreter의 구성을 확인하고, 변경할 수 있는 서비스를 제공하는 모듈  
프로그램 외부의 작업환경과 상호작용할 수 있는 서비스를 제공  

ex) build time 버전 정보를 설정, 인터프리터를 빌드하는데 사용되는 운영체제 플랫폼을 정의  

### 결론 => Traceback 로그가 출력되는 과정
런타임환경 외부의 작업환경인 콘솔의 print와 상호작용하기 위해 sys.exc_info() 라는 함수의 인자에다가 traceback object로 생성된 객체를 전달해 로그가 전달   



--------
--------
# Reference
https://velog.io/@chldppwls12/python-%EB%8F%99%EC%9E%91-%EB%B0%A9%EC%8B%9D
https://st-lab.tistory.com/176
