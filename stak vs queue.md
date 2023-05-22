## stack vs queue

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

### pop, push

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
