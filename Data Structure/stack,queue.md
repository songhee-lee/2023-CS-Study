## stack vs queue

![img](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/a21cf941-c0a8-4f34-9ac3-5ff9dae3ccde)

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqELv5%2Fbtsg1e2f7GN%2F0gGLjIp7uIy6tuxKqZlUjK%2Fimg.png)

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRkNKD%2FbtshiibvnZt%2FEEsTxjA29KsUfA6TPAChG0%2Fimg.png)

---

## 스택

- 스택이란 '쌓아 올린다', '무더기', '쌓아서 채워놓다'는 것을 의미한다
- 마구잡이로 쌓여있기보다는 차곡차곡 쌓여 있는 느낌이다

### 특징

- 같은 구조와 크기의 자료를 정해진 방향으로만 쌓기 가능
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

### 파이썬으로 구현

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

### c언어로 구현(pop, push)

<pre>
<code>
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

// 스택 구조체 정의
typedef struct {
    int data[MAX_SIZE];
    int top;
} Stack;

// 스택 초기화 함수
void initializeStack(Stack* stack) {
    stack->top = -1;
}

// 스택이 비어있는지 확인하는 함수
int isStackEmpty(Stack* stack) {
    return (stack->top == -1);
}

// 스택이 가득 차 있는지 확인하는 함수
int isStackFull(Stack* stack) {
    return (stack->top == MAX_SIZE - 1);
}

// 스택에 데이터를 추가하는 함수
void push(Stack* stack, int value) {
    if (isStackFull(stack)) {
        printf("Stack overflow!\n");
        return;
    }
    stack->data[++stack->top] = value;
}

// 스택에서 데이터를 제거하고 반환하는 함수
int pop(Stack* stack) {
    if (isStackEmpty(stack)) {
        printf("Stack underflow!\n");
        return -1;
    }
    return stack->data[stack->top--];
}

int main() {
    // 스택 변수 선언
    Stack stack;

    // 스택 초기화
    initializeStack(&stack);

    // 스택에 데이터 추가
    push(&stack, 1);
    push(&stack, 2);
    push(&stack, 3);

    // 스택에서 데이터 제거 및 출력
    printf("Stack: ");
    while (!isStackEmpty(&stack)) {
        printf("%d ", pop(&stack));
    }
    printf("\n");

    return 0;
}
</pre>
</code>

### 스택을 배열로 구현

스택은 후입선출(LIFO)의 구조를 가지므로, 배열을 이용하여 구현 가능

일반적으로 배열의 끝을 스택의 상단(top)으로 사용

배열에서 스택에 새로운 요소를 추가할 때는 상단(top) 인덱스를 증가

요소를 제거할 때는 상단(top) 인덱스를 감소

### 스택 두 개를 이용해 큐 구현하는 방법은?

"이중 스택"이라고도 불리며, 스택 두 개를 사용하여 큐의 동작을 모방하는 방식

이중 스택을 이용하여 큐를 구현하기 위해서는 두 개의 스택을 준비

하나는 요소를 추가하는 스택(push 스택)으로 사용하고, 다른 하나는 요소를 제거하는 스택(pop 스택)으로 사용

요소를 큐에 추가할 때는 push 스택에 요소를 push

요소를 제거할 때는 pop 스택에서 요소를 pop하는데, 이때 pop 스택이 비어있으면 push 스택의 모든 요소를 pop하여 pop 스택으로 옮긴 후 pop 스택에서 요소를 pop

이렇게 하면 스택의 후입선출(LIFO) 특성을 이용하여 큐의 선입선출(FIFO) 동작을 구현할 수 있음

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

### C언어로 큐 구현

<pre>
<code>
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

// 큐 구조체 정의
typedef struct {
    int data[MAX_SIZE];
    int front;
    int rear;
} Queue;

// 큐 초기화 함수
void initializeQueue(Queue* queue) {
    queue->front = -1;
    queue->rear = -1;
}

// 큐가 비어있는지 확인하는 함수
int isQueueEmpty(Queue* queue) {
    return (queue->front == -1);
}

// 큐가 가득 차 있는지 확인하는 함수
int isQueueFull(Queue* queue) {
    return ((queue->rear + 1) % MAX_SIZE == queue->front);
}

// 큐에 데이터를 추가하는 함수
void enqueue(Queue* queue, int value) {
    if (isQueueFull(queue)) {
        printf("Queue overflow!\n");
        return;
    }
    if (isQueueEmpty(queue)) {
        queue->front = 0;
    }
    queue->rear = (queue->rear + 1) % MAX_SIZE;
    queue->data[queue->rear] = value;
}

// 큐에서 데이터를 제거하고 반환하는 함수
int dequeue(Queue* queue) {
    if (isQueueEmpty(queue)) {
        printf("Queue underflow!\n");
        return -1;
    }
    int value = queue->data[queue->front];
    if (queue->front == queue->rear) {
        initializeQueue(queue);
    } else {
        queue->front = (queue->front + 1) % MAX_SIZE;
    }
    return value;
}

int main() {
    // 큐 변수 선언
    Queue queue;

    // 큐 초기화
    initializeQueue(&queue);

    // 큐에 데이터 추가
    enqueue(&queue, 1);
    enqueue(&queue, 2);
    enqueue(&queue, 3);

    // 큐에서 데이터 제거 및 출력
    printf("Queue: ");
    while (!isQueueEmpty(&queue)) {
        printf("%d ", dequeue(&queue));
    }
    printf("\n");

    return 0;
}
</pre>
</code>

---

## 우선순위 큐

### 큐와의 차이점

들어간 순서와 상관있는 큐와 달리, 들어간 순서는 상관없고 우선순위가 높은 데이터가 먼저 나오는 것

### 속성

1. 모든 항목에는 우선순위 부여
2. 우선 순위가 높은 요소는 우선 순위가 낮은 요소보다 먼저 queue에서 제외
3. 두 요소이 우선 순위가 같으면 queue의 순서에 따라 제공

### 파이썬 구현

<pre>
<code>
import heapq

# 우선순위 큐 초기화
priority_queue = []

# 데이터 삽입
heapq.heappush(priority_queue, 3)
heapq.heappush(priority_queue, 1)
heapq.heappush(priority_queue, 4)
heapq.heappush(priority_queue, 2)

# 데이터 삭제 (우선순위가 가장 낮은 값부터 삭제됨)
while priority_queue:
    item = heapq.heappop(priority_queue)
    print("Dequeued item:", item)
</pre>
</code>

- 위 코드에서는 heapq 모듈의 heappush() 함수를 사용하여 데이터를 우선순위 큐에 삽입
- heappop() 함수를 사용하여 우선순위가 가장 낮은 값을 삭제하고 출력
- 파이썬의 heapq 모듈은 내부적으로 최소 힙(Min Heap)을 사용하여 우선순위 큐를 구현
