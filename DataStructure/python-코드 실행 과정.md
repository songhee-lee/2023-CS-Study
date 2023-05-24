# 파이썬 
## 코드 실행 과정
`.py` 로 작성된 파이썬 코드는 제일 먼저 **바이트 코드** 로 컴파일 되고, 바이트 코드는 인터프리터를 통해 실행된다.
![image](https://github.com/0sun-creater/2023-CS-Study/assets/54173210/978532a2-dc23-4638-8639-74365af5c5c0)

인터프리터 종류  

PyPy가 CPython 보다 빠른 이유
- CPython은 일반적인 인터프리터
- PyPy는 JIT(Just In Time)를 겸비한 인터프리터
- JIT는 인터프리터의 단점을 보완하기 위해 기계어 코드를 생성하면서 그 코드를 캐싱하여, 같은 함수가 여러 번 불릴 때 매번 기계어 코드를 생성하는 것을 방지

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
#### .pyc
- .py 파일의 컴파일된 버전
- 성능향상을 위해 자동으로 생성
- PVM(Python Virual Machine)에 의해 실행되고, 지워도 되지만 성능 저하 가능성 있음
  
    
#### 파이썬 사용 사례
- 시스템 스크립팅
- 웹 개발
- 게임 개발
- 소프트웨어 개발
- 복잡한 수학
- 데이터 분석

#### 파이썬의 혜택
- 객체지향 프로그래밍
- 고급 언어
- 동적 언어
- 방대한 라이브러리 지원
- 써드파티 모듈의 존재
- 오픈소스이자 커뮤니티 개발
- 기종간 사용할 수 있고 상호교환적
- 모든 운영체제에서 사용 가능

#### PEP 8
- 파이썬 스타일 가이드, 문서
- 파이썬 코드를 잘 작성하기 위한 가이드라인과 모범 사례 제공
- 읽기 쉽고 눈에 보기 좋은 코딩 스타일 장려


---------
---------

### 주요 특징
- interpreted language : 실행 전 컴파일 필요 없음
- dynamically typed : 변수 사용 전 선언 필요 없음
- 객체지향적 프로그래밍 : 상송 등과 함께 class(객체) 정의 허용
- 함수가 first-class object : 변수에 할당 가능, 다른 함수에서 반환 및 전달 가능

- Scripting : 자동화 가능 / 주어진 데이터에서 정보 제공
- Programming : script 또는 다른 상위 코드 내에서 실행

- Python은 대소문자를 구별하는 case-sensitive한 언어

- 자바스크립트나 C++과 달리 삼향 연산자(ternary operator)가 없음
  - 비슷한 역할을 하는 다른 기능은 존재

Multithreading
- 멀티스레딩 패키지가 있음
- 하지만 Python은 GIL(Global Intervirator Lock) 구조로 되어있기 때문에 멀티스레딩을 하더라도 같은 CPU가 교대로 작업됨

Compilation & Linking
- 새로운 확장자를 오류 없이 적절하게 컴파일하도록 함
- Linking은 컴파일된 절차 통과해야 수행됨
- 새로운 확장자 파일을 Modules/ 경로에 넣고 Setup.local 파일에 행을 추가하고 spam file.o를 이용하여 실행 후 make 명령어로 재빌드

데코레이터
- 강력하고 유용한 파이썬 툴
- 함수를 감싸줌으로써, 함수를 영구적으로 수정하지 않고 함수의 행위를 확장 

동적타이핑 언어
- 덕타이핑(Duck-typing) 사용
- 런타임 에러 발생 가능성 

Generator
- 이터레이터를 생성해 주는 함수
- 이터레이터는 next()함수를 이용해 데이터에 순차적으로 접근이 가능
- 제네레이터 함수가 실행 중 yield 를 만날 경우 함수는 그 상태로 정지 되며 반환 값을 next()를 호출한 쪽으로 전달
- 이후 다시 제네레이터 함수가 실행되면 종료된 시점에서 다음 yield까지 실행

클래스를 상속했을 때 메서드 실행 방식
- 인스턴스의 메서드를 실행한다고 가정할 때 __getattribute__()로 bound 된 method 를 가져온 후 메서드를 실행
- 상속할때 왼쪽에 가까운 순서대로 우선순위가 높음

GIL(Global Interpreter Lock)과 성능 문제
- 여러 스레드가 동시에 실행되는 걸 막는다.
- 덕분에 구현이 간단하고 레퍼런스 카운팅 오버헤드가 적음
- 수행시간에 CPU의 영향이 큰 작업(압축, 정렬, 인코딩)을 멀티 스레드로 수행하면 GIL로 인하여 싱글 스레드일 때와 차이 X
- CPU의 영향이 큰 작업(CPU Bound)을 진행할 경우에는 멀티 프로세스를 활용하는 것을 권장
- 파일 입출력, 네트워크 같은 입출력이 많은 작업(IO Bound)에 멀티 스레드를 사용하는 것이 적합



메모리 누수가 발생할 수 있는 경우
- 메서드 기본 인자 값으로 mutable 객체를 사용하고 있는 경우
클래스 내 __del__ 메서드를 재정의 하는 경우
Duck Typing
Duck typing이란 특히 동적 타입을 가지는 프로그래밍 언어에서 많이 사용되는 개념으로, 객체의 실제 타입보다는 객체의 변수와 메소드가 그 객체의 적합성을 결정하는 것을 의미한다. 하나의 외부 메서드를 통해서 서로 다른 객체의 인자의 같은 이름의 메서드를 호출할 수 있다.






### 그 외 참고사항
![image](https://github.com/songhee-lee/2023-CS-Study/assets/54173210/77333e85-d494-46cd-8c7b-5916d1452dbb)
![image](https://github.com/songhee-lee/2023-CS-Study/assets/54173210/6f43e1c2-5868-4738-9cc0-c144fd24af0d)
![image](https://github.com/songhee-lee/2023-CS-Study/assets/54173210/8f7d4faa-4e31-4749-840f-dc8aeafe4dbb)
![image](https://github.com/songhee-lee/2023-CS-Study/assets/54173210/a0d2a172-7f28-4422-b539-cd1c224495fb)
![image](https://github.com/songhee-lee/2023-CS-Study/assets/54173210/923dfee1-66fa-4647-b567-2e51d363cacd)
![image](https://github.com/songhee-lee/2023-CS-Study/assets/54173210/9a7f85f6-043f-4150-9d97-cb5928062649)
![image](https://github.com/songhee-lee/2023-CS-Study/assets/54173210/ae188612-1e09-43d2-a1ab-10df46f72dec)
![image](https://github.com/songhee-lee/2023-CS-Study/assets/54173210/14d1bc25-c639-4a67-8c48-9e3a9fb55e7c)

namespace
- 이름 충돌 피하기 위해 고유한 이름인지 확인하는 이름 지정 시스템

list 와 tuple 의 차이
- list : 가변성, 더 많은 메모리 소모(더 느림)
- tuple : 불변성(수정 불가), 더 적은 메모리 소모(더 빠름)

Array와 List 차이
- array : 요소의 data type이 동일해야 함 (import array)
- list : 요소의 data type 상관 없음

__init__
- method or constructor 
- 새로운 객체나 class가 생성됐을 때 메모리 할당

lambda 함수
- 이름이 정해져 있지 않은 함수로, 여러 parameter 받아 결과 return 
- a = lambda x,y : x+y

PYTHONPATH
- 모듈이 import되는 환경변수

self
- class의 인스턴스 또는 객체

range와 xrange 차이
- 둘 다 일정 간격 정수 반환
- xrange == generator의 yield : range보다 더 적은 메모리 사용하며, type이 다름 (range는 list / xrange는 xrange)

sort() & sorted() 함수에서 사용되는 분류 처리방식 
Time Sort 알고리즘 사용 https://www.geeksforgeeks.org/timsort/
Time Sort 방식은 최악의 상황일 때가 0인(N log N)매우 안정적인 분류 방식이다. Tim Sort는 하이브리드 정렬 알고리즘으로써, 
병합정렬과 삽입정렬로 부터 파생되었고, 많은 종류의 실제 세계 데이터에서 잘 작동하도록 설계되었다.


--------
--------
# Reference
1. 2023 파이썬 intervew top 10 : https://intellipaat.com/blog/interview-question/python-interview-questions/?US
2. https://heehehe-ds.tistory.com/142
3. https://velog.io/@jean1042/Back-to-the-basic-Python-interpreter%EC%9D%98-%EC%9E%91%EB%8F%99%EB%B0%A9%EC%8B%9D
