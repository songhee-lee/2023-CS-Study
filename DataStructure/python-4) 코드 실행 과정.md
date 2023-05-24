# 파이썬 
## 코드 실행 과정
`.py` 로 작성된 파이썬 코드는 제일 먼저 **바이트 코드** 로 컴파일 되고, 바이트 코드는 인터프리터를 통해 실행된다.
![image](https://github.com/0sun-creater/2023-CS-Study/assets/54173210/978532a2-dc23-4638-8639-74365af5c5c0)

인터프리터 종류  
- CPython은 일반적인 인터프리터
- PyPy는 JIT(Just In Time)를 겸비한 인터프리터
  - JIT는 인터프리터의 단점을 보완하기 위해 기계어 코드를 생성하면서 그 코드를 캐싱하여, 같은 함수가 여러 번 불릴 때 매번 기계어 코드를 생성하는 것을 방지
  - PyPy 가 Cpython 보다 빠름




## 인터프리터 작동 과정
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
![image](https://github.com/songhee-lee/2023-CS-Study/assets/54173210/4f4dab9a-367b-4449-90eb-51d7f04aedb0)



--------
--------
# Reference
1. 2023 파이썬 intervew top 10 : https://intellipaat.com/blog/interview-question/python-interview-questions/?US
2. https://heehehe-ds.tistory.com/142
3. https://velog.io/@jean1042/Back-to-the-basic-Python-interpreter%EC%9D%98-%EC%9E%91%EB%8F%99%EB%B0%A9%EC%8B%9D
