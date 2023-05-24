# 파이썬

## 요약 및 속도 비교 코드

|언어|타이핑 방식|장점|단점|
|:------:|:-----:|:-----:|:-----|
|C, Fortran|정적 </br>타이핑|컴파일된 코드로 </br>빠른 실행|1. 변수를 선언하는 데 많은 개발 오버헤드 발생</br> 2. 대화형 프롬프트 없음|
|Python, R, Matlab|동적 </br>타이핑|인터프리터 실행으로 </br>빠른 개발|동적 유형 검사 등에서 많은 실행 오버헤드 발생|

**개발 시간이 일반적으로 실행 시간보다 더 중요하기 때문에 python을 자주 쓰지만, 때로는 속도가 문제가 된다.**

### 컴파일된 언어와 비교
동일한 함수를 포트란에 작성하고 도구 `f2py`(NumPy에 포함됨)를 사용하여 컴파일 해보기
1. 파이썬
```python
# A silly function implemented in Python

def func_python(N):
    d = 0.0
    for i in range(N):
        d += (i % 3 - 1) * i
    return d
```
```python
# Use IPython timeit magic to time the execution
%timeit func_python(10000)
```
> 1000 loops, best of 3: 1.81 ms per loop

 2. 포트란
```python
%%file func_fortran.f

      subroutine func_fort(n, d)
           integer, intent(in) :: n
           double precision, intent(out) :: d
           integer :: i
           d = 0
           do i = 0, n - 1
                d = d + (mod(i, 3) - 1) * i
           end do
      end subroutine func_fort
```
> Overwriting func_fortran.f

```python
!f2py -c func_fortran.f -m func_fortran > /dev/null
```
```python
from func_fortran import func_fort
%timeit func_fort(10000)
```
> 100000 loops, best of 3: 20.3 µs per loop

-> 결과 : 포트란이 100 배 빠름

</br>

</br>

--------
--------

</br>

## 1. 파이썬은 정적이 아닌 동적 타입 이다.

    
|정적 타입|동적 타입|
|:------:|:-------:|
|타입(자료형) 지정|타입 지정x|
|자료형이 맞지 않으면 컴파일 에러(형변환 필요)|자유로움,편리, 빠르게 개발|
|런타임이 아닌 컴파일시 TypeError 발견->안전|런타임 시 TypeError 발생 가능성 존재|
|컴파일시 타입 정보 결정하기 때문에 속도 빠름|속도 느림|
|C, C++, java, ...|Python, Ruby, SmallTalk, JavaScript, ...|
    
    
프로그램 실행 시, '인터프리터는 정의된 변수의 유형을 알고 있지 않다' 는 것을 의미한다.   
C언어(컴파일 된 언어의 표준) 변수의 경우, 컴파일러는 단지 그 정의만으로도 변수의 유형을 알고 있다.  
파이썬 변수의 경우, 프로그램 실행시의 변수는 파이썬 개체의 일부 종류이다.  

![image](https://github.com/0sun-creater/2023-CS-Study/assets/54173210/0496931e-b363-4487-8f1b-a56abfef6a3f)

**1. C**
```C
int a=1;
int b=2;
int c=a+b;
```
C 컴파일러는 시작할 때부터 a와 b는 정수형이라는 것을 알고 있다.  
정수형을 아는 것으로 메모리 상의 단순한 값에 두 개의 정수를 더하고, 이를 다른 정수로 반환하는 루틴 호출이 가능하다.  

> (1) <int> 1을 a에 할당  
> 
> (2) <int> 2를 b에 할당  
> 
> (3) binary_add<int, int>(a,b) 호출  
> 
> (4) 결과를 c에 할당  


  
**2. Python**
```python
a=1
b=2
c=a+b
```

인터프리터는 1과 2는 개체라는 것만 알고 있고, 타입을 알지 못한다.
타입 정보를 찾기 위해 각 변수의 PyObject_HEAD를 검사한 후, 두 타입의 적적할 덧셈 루틴을 호출한다.
반환 값을 보관 유지하는 새로운 python 개체를 만들고 초기화해야한다.   
> (1) a에 1을 할당   
>   - a->PyObject_HEAD->typecode 정수 설정   
>   - a->val = 1 설정  
  
> (2) b에 2를 할당   
>   - b->PyObject_HEAD->typecode 정수 설정      
>   - b->val = 2 설정     
  
> (3) binary_add(a,b) 호출    
>   - a->PyObject_HEAD->typecode 찾기    
>   - a는 정수형; 값 a->val    
>   - b->PyObject_HEAD->typecode 찾기    
>   - b는 정수형; 값 b->val   
>   - binary_add<int,int>(a->val, b->val) 호출    
>   - 정수형 결과값 result    
  
> (4) 파이썬 개체 c 생성   
>   - c->PyObject_HEAD->typecode 정수 설정    
>   - c->val에 result 설정   


**동적 타이핑은 모든 작업에 더 많은 단계가 포함되있음을 의미한다.**   
**이것이 숫자 데이터에 관한 연산에서 C언어와 비교했을 때 파이썬이 느린 가장 큰 이유이다.**  

</br>

</br>

## 2. 파이썬은 컴파일 형식이 아닌 인터프리터 형식이다.

스마트한 컴파일러는 결과의 속도를 높일 수 있도록, 반복되거나 불필요한 연산을 미리 내다보고 최적화할 수 있다.  
컴파일러 최적화는 컴파일러만의 특성이기에 그것에 대해 자세한 설명이 어렵다.  
이에 대한 몇가지 예제들 링크
http://jakevdp.github.io/blog/2013/06/15/numba-vs-cython-take-2/

</br>

</br>

## 3. 파이썬의 개체모델은 비효율적인 메모리 액세스가 발생할 수 있다.

C에서는 어떤 종류의 버퍼 기반의 배열을 사용하는 동안,
파이썬에서는 표준 List 개체를 사용할 수 있다.
    

가장 간단한 형태의 Numpy 배열은 C의 배열과 유사한 파이썬 개체이다.
1. Numpy 배열은 값들의 연속되는 데이터 버퍼를 위한 포인터를 가지고 있다.
2. 파이썬 리스트는 포인터의 연속되는 버퍼를 위한 포인터를 가지고 있다.  
각각의 포인터들은 그것들의 데이터 주소를 가지고 있고 주소를 가르키고 있다.
![image](https://github.com/0sun-creater/2023-CS-Study/assets/54173210/2505bd10-e796-4744-9280-11545507dc8e)

    
**따라서 파이썬 내에서 연속되는 데이터로 여러 단계를 통한 어떠한 작업을 해야한다면, Numpy 레이아웃이 저장과 액세스 측면에서 파이썬의 레이아웃보다 훨씬 더 효율적이다.**
    

--------
--------

## 파이썬을 빠르게 만들기 위한 전략
1. Numpy ufunces를 유리하게 사용
2. Numpy 집계를 유리하게 사용
3. Numpy 브로드캐스팅을 유리하게 사용
4. Numpy 슬라이싱 및 마스킹 활용
5. SWIG, cython 또는 f2py와 같은 도구를 사용하여 컴파일된 코드에 인터페이스 하기

예시 코드 참조 https://nbviewer.org/github/jakevdp/2013_fall_ASTR599/blob/master/notebooks/11_EfficientNumpy.ipynb



## Reference
https://medium.com/@cookatrice/7126baf936d7
