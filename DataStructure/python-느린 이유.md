# 파이썬

## 동적인 타이핑과 인터프리트 언어

- C, Fortran : 정적 타이핑 및 컴파일된 코드로 빠른 실행   
               변수를 선언하는 데 많은 개발 오버헤드가 발생하고 대화형 프롬프트가 없음   
               
               
- Python, R, Matlab, IDL : 동적 타이핑과 인터프리터 실행으로 빠른 개발 가능    
                           동적 유형 검사 등에서 많은 실행 오버헤드가 발생

개발 시간이 일반적으로 실행 시간보다 더 중요하기 때문에 python을 자주 쓰지만, 때로는 속도가 문제가 된다.

컴파일된 언어와 비교하기 위해 동일한 함수를 포트란에 작성하고 도구 `f2py`(NumPy에 포함됨)를 사용하여 컴파일 해보기   
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
1000 loops, best of 3: 1.81 ms per loop

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
Overwriting func_fortran.f

```python
!f2py -c func_fortran.f -m func_fortran > /dev/null
```
```python
from func_fortran import func_fort
%timeit func_fort(10000)
```
100000 loops, best of 3: 20.3 µs per loop

==>결과 포트란이 100 배 빠름



--------
--------

## 파이썬을 빠르게 만들기 위한 전략
1. Numpy ufunces를 유리하게 사용
2. Numpy 집계를 유리하게 사용
3. Numpy 브로드캐스팅을 유리하게 사용
4. Numpy 슬라이싱 및 마스킹 활용
5. SWIG, cython 또는 f2py와 같은 도구를 사용하여 컴파일된 코드에 인터페이스 하기

예시 코드 참조 https://nbviewer.org/github/jakevdp/2013_fall_ASTR599/blob/master/notebooks/11_EfficientNumpy.ipynb





