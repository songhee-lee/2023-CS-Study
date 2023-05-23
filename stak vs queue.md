## stack vs queue

![img](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/a21cf941-c0a8-4f34-9ac3-5ff9dae3ccde)

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqELv5%2Fbtsg1e2f7GN%2F0gGLjIp7uIy6tuxKqZlUjK%2Fimg.png)

---

## 스택

스택이란 '쌓아 올린다', '무더기', '쌓아서 채워놓다'는 것을 의미한다

마구잡이로 쌓여있기보다는 차곡차곡 쌓여 있는 느낌이다

### 특징

- 같은 구조와 크기의 자료를 정해진 방향으로만 쌓을 수 있음
- top을 통해 삽입하는 연산을 'push'
- top을 통해 삭제하는 연산을 'pop'
- 후입선출(LIFO, last in first out)
- 비어있는 스택에서 원소를 추출하려고 하는 것 = 'stack underflow'
- 스택이 넘치는 경우 = 'stack overflow'(https://stackoverflow.com ㅎㅎ)

### 활용 예시

- 웹 브라우저 방문기록 (뒤로 가기) : 가장 나중에 열린 페이지부터 다시 보여주기
- 역순 문자열 만들기 : 가장 나중에 입력된 문자부터 출력
- 실행 취소 (undo) : 가장 나중에 실행된 것부터 실행을 취소
- 후위 표기법 계산
- 수식의 괄호 검사 (연산자 우선순위 표현을 위한 괄호 검사)

### 파이썬으로 구현(pop, push)

<pre>
<code>
# 스택 클래스 정의
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, item):
        self.stack.append(item)

    def pop(self):
        if not self.is_empty():
            return self.stack.pop()
        else:
            raise IndexError("스택이 비어있습니다.")

    def is_empty(self):
        return len(self.stack) == 0


# 스택 사용 예시
stack = Stack()

# push 연산
stack.push(1)
stack.push(2)
stack.push(3)

# pop 연산
print(stack.pop())  # 3
print(stack.pop())  # 2
print(stack.pop())  # 1

# 스택이 비어있는 경우 pop 연산 시 에러 발생
print(stack.pop())  # IndexError: 스택이 비어있습니다.
</code>
</pre>

---

## 큐

큐란 '(무엇을 기다리는 사람, 자동차 등의) 줄', '줄을 서서 기다리다', '대기행렬'이라는 뜻이 있다

### 특징

- 한쪽에서는 삽입, 다른 한 쪽에서는 삭제 작업을 함, 양쪽으로 이루어짐
- 삽입하는 쪽을 'rear' / 가장 끝 원소이기도 함
- 삭제하는 쪽을 'front' / 가장 첫 원소이기도 함
- 삽입 연산을 인큐(enqueue)
- 삭제 연산을 디큐(dequeue)

### 활용 예시

- 우선순위가 같은 작업 예약 (프린터의 인쇄 대기열)
- 은행 업무
- 콜센터 고객 대기시간
- 프로세스 관리
- 너비 우선 탐색(BFS, Breadth-First Search) 구현
- 캐시(Cache) 구현

### collections.deque

<pre>
<code>
##deque.append = enqueue

from collections import deque

d = deque()

for i in range(3):
    d.append(i)
print(d)

# deque([0, 1, 2])
</code>
</pre>

<pre>
<code>
## deque.appendleft = 왼쪽에 enqueue

from collections import deque

d = deque()
for i in range(3):
    d.append(i)

d.appendleft(3)
print(d)

# deque([3, 0, 1, 2])
</code>
</pre>

<pre>
<code>
## deque.insert = queue 중간에 enqueue

from collections import deque

d = deque()
for i in range(3):
    d.append(i)

d.insert(3, 11)
print(d)

# deque([0, 1, 2, 11])
</code>
</pre>

<pre>
<code>
## deque.popleft = 왼쪽 데이터 제거

from collections import deque

d = deque()
for i in range(3):
    d.append(i)

print(d.popleft())

# 0
</code>
</pre>

<pre>
<code>
## deque.pop = 오른쪽 데이터 제거

from collections import deque

d = deque()
for i in range(3):
    d.append(i)

print(d.pop())

# 2
</code>
</pre>

### 파이썬으로 전체적으로 구현

<pre>
<code>
class Queue:
    def __init__(self):
        self.queue = []  # 큐를 저장할 리스트 선언

    def is_empty(self):
        return len(self.queue) == 0  # 큐가 비어있는지 여부 반환

    def enqueue(self, item):
        self.queue.append(item)  # 큐의 뒤쪽에 새로운 원소 추가

    def dequeue(self):
        if not self.is_empty():
            return self.queue.pop(0)  # 큐의 앞쪽에서 원소 제거하고 반환
        else:
            raise Exception("Queue is empty")  # 큐가 비어있을 경우 예외 발생

    def front(self):
        if not self.is_empty():
            return self.queue[0]  # 큐의 앞쪽에 위치한 원소 반환
        else:
            raise Exception("Queue is empty")  # 큐가 비어있을 경우 예외 발생

    def rear(self):
        if not self.is_empty():
            return self.queue[-1]  # 큐의 뒤쪽에 위치한 원소 반환
        else:
            raise Exception("Queue is empty")  # 큐가 비어있을 경우 예외 발생

    def size(self):
        return len(self.queue)  # 큐의 원소 개수 반환
</code>
</pre>
