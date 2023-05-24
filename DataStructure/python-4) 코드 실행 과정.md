# 파이썬 
## 하이브리드 언어 (인터프리터 언어+ 컴파일 언어)
파이썬은 부분 컴파일 언어이자, 인터프리터 언어이다.
컴파일 언어처럼 하드웨어를 직접 제어하는 작업은 불가능

|인터프리터 언어|컴파일 언어|
|-------|--------|
|기계어 변환 과정 없음|모두 기계어로 변환|
|한줄 한줄 해석해서 바로 명령어 실행|기계에 넣고 기계어 코드를 실행|
|빌드 과정 없음| 빌드 과정(소스 파일->실행 파일)에서 시간 소요|
|런타임 상황에서 한줄씩 읽음|런타임 상황에서 이미 소스코드가 변환되어 있음|
|속도 느림|속도 빠름|
|프로그램 수정 간단|수정 후 다시 컴파일 필요|

![image](https://github.com/0sun-creater/2023-CS-Study/assets/54173210/bc5e1aef-f390-46f4-af98-e10eb77789e4)

</br>

</br>

## 파이썬 코드 실행 과정
`.py` 로 작성된 파이썬 코드는 제일 먼저 **바이트 코드** 로 컴파일 되고, 바이트 코드는 **인터프리터**를 통해 실행된다.
- 바이트 코드는 하드 디스크의 `.pyc' 파일에 저장  (__pycache__ 폴더 안에 생성)
- PVM (Python Virtual Machine) : 인터프리터, 가상 머신
  - VM을 통해 '플랫폼에 독립적'인 장점을 가짐
  - 플랫폼에 독립적 : python, java(JVM), c#(.NET의 CLR) / 윈도우, 맥, 리눅스 어디서나 번역 및 실행이 가능
  - 플랫폼에 의존적 : c 언어 / 소스 코드자체는 다르지 않지만, 최종 결과물이 윈도우에서는 `.exe` 파일 리눅스에서는 `.out` 파일

![image](https://github.com/0sun-creater/2023-CS-Study/assets/54173210/85c48b3c-cb14-4c5a-b43d-be0905030e79)

</br>

</br>

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
</br>
</br>
## 파이썬 작동 방식
![image](https://github.com/0sun-creater/2023-CS-Study/assets/54173210/39f26a30-6803-4dcd-a724-09d1a9b3c00c)

### Step 1. 소스코드
> 파이썬 컴파일러가 소스 코드를 읽는다.  
> 소스코드가 잘 작성 되었는지를 판단하기 위한 문법 오류 검사를 진행한다.  
> 만약 문법 오류가 발견되었다면, 그 즉시 컴파일 과정을 멈추고 에러 메시지 출력  

</br>

### Step 2. 컴파일러
> 에러가 발생하지 않았다면 컴파일러가 소스 코드를 바이트 코드로 변환한다.
>> **1. Lexing**  
>> 전달된 코드를 가지고 라인을 쪼개 코드를 Token으로 일반화 한다.  
>> 토큰 : 어휘 분석의 단위를 의미하는 컴퓨터 용어  
>> </br>
>> **2. Parsing**
>> 토큰들이 parser에게 전달되어 데이터를 구조적으로 나타냄    
>> 데이터를 구조적으로 바꾸는 과정에서 데이터가 올바른지 검증하는 역할도 수행함
>> parser에 의해 도출된 결과가 AST의 모습을 보인다.
>> AST (Abstract Syntax Tree) : 프로그래밍 언어로 쓰여진 소스코드의 Abstract Syntatic 구조를 표현하기 위해 사용되는 자료구조  
>>  특정 프로그래밍 언어로 작성된 프로그램 소스를 각각 의미별로 분리하여 컴퓨터가 이해할 수 있는 구조로 변경시킨 트리  
>> AST를 제어 흐름 그래프(Control FlowGraph)로 변환한다.     
>> https://en.wikipedia.org/wiki/Abstract_syntax_tree  
>>  </br> 
>> **3. Compiling**  
>> AST가 컴파일러에게 전달되고, 컴파일러가 AST를 이용하여 ByteCode 라는 `.pyc` 형태의 `intermediate language code`를 생성한다.  
>> 대화형 프롬프트(REPL) 환경에서 입력한 코드에 대해서는 `.pyc` 파일 생성 안함


</br>

### Step 3. PVM (Python Virual Machine)
> 바이트 코드(`.pyc`)가 전달되어져서 python 코드가 실행되며 파이썬의 런타임 엔진이다.   
> PVM은 바이트 코드를 컴퓨터가 실행할 수 있는 기계어로 한 줄 한 줄 (line by line) 번역한다.  
> 실제 interpreting 작업을 담당하며, byte code를 기계어로 변환하여 실행되는 곳이다.  
> Row 단위로 해석하며 프로그램을 구동하는 방식   
> 만약 이 과정에서 에러가 발생하면 모든 것을 멈추고 에러 메시지 출력   

</br>

- 해당 과정에 대해 더 깊게 알고 싶으면 ? https://www.cs.columbia.edu/~suman/secure_sw_devel/Basic_Program_Analysis_CF.pdf 

- 자바 소스코드와의 차이점?  
  - 자바코드는 인터프리터에 소스가 전달되기 전에 컴파일러에 의해 컴파일됨. 
  - 컴파일러가 인터프리터 밖에 존재함
  - 파이썬은 인터프리터/컴파일러가 인터프리터 안에 함께 존재해서 performance lag을 줄임

- Lexer->Parser의 간단한 예시
```PYTHON
입력값 : [1, [2,[3]], "he is tall"]


토크나이저 결과 
[ "1", "[2,[3]]", "['he', 'is', 'tall']"]

렉서 결과 
[
	{type: 'number', value:"1" },
	{type: 'array', value: "[2, [3]]"},
	{type: 'array', value: "['he', 'is', 'tall']"},
]

파서 결과  
{
	type: 'array',
	child: [
		{type: 'number', value:'1', child:[] },
		{type: 'array', 
			child: [
			{ type: 'number', value: '2', child:[] },
			{ type: 'array', 
				child:[ {type:'number', value:'3', child:[]}
			]
		}]
		},
		{type: 'array', 
			child:[
			{ type: 'string', value: 'he', child:[] },
			{ type: 'string', value: 'is', child:[] },
			{ type: 'string', value: 'tall', child:[] },
			]
		}]
}
```

--------
--------
# Reference
https://velog.io/@chldppwls12/python-%EB%8F%99%EC%9E%91-%EB%B0%A9%EC%8B%9D
https://st-lab.tistory.com/176
https://shrtorznzl.tistory.com/82
https://ko.wikipedia.org/wiki/JIT_%EC%BB%B4%ED%8C%8C%EC%9D%BC
http://www.aistudy.co.kr/linguistics/natural/parsing.htm
