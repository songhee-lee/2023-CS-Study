## Hash Table 실사용 예시

### 표로 정리

![img](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/3eefeefb-d14b-488b-a793-849e90358ad9)

### 노래방 책

![img](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/9b4636ab-e3c6-459c-9b07-3b6ef7168783)
당신은 노래방이다

책만 있다면 번호를 찾기 위해서 노래방 책에서 하나하나 목차를 넘겨가며 찾아야 한다

하지만, 원하는 노래가 있다면 검색을 통해서 빠르게 찾는 방법이 더 효율적이라는 것을 직관적으로 알 수 있다

### 피자 메뉴

![img](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/18377805-40bb-489c-881b-02441c2a4483)
당신은 레스토랑에 피자를 먹으려고 들어왔다

만약 피자의 가격이 얼마인지 알려면

왼쪽은 coffee부터 juice까지 선형검색을 해야 한다(오래 걸린다)

하지만, 오른쪽처럼 정리를 하면 pizza가 key, 가격인 10이 value가 되어서 더 빠르다

왼쪽의 시간복잡도는 (처음부터 차례로 확인해야 하므로) O(n)이고, 오른쪽은 상수시간인 O(1)이 된다

즉, 해시테이블의 시간복잡도는 삽입, 삭제, 검색모두 O(1)이라는 놀라운 점을 발견할 수 있다

(물론 평균적인 경우 한정, 물론 선형검색할 수 있고 나중에 나올 해시충돌의 경우에는 O(n) 가능)

### 블록체인

![img](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/ff9b9da1-0595-42a6-a16c-bc1db9776cd7)

서비스 거래 기록을 모두 저장해야 하므로 큰 용량이 필요하다

원본 보관이 어렵기 때문에(보완상의 이유도 있고) 해시코드로 보관하고 이를 검증하여 처리한다

### 그 외

- 변조 탐지/에러 검출

- 연관배열: 여러 유형의 메모리 내 테이블을 구현하는 데 사용, 루비, 파이썬 등에서 연간배열(지표가 임이의 문자열 또는 기타 복잡한 객체인 배열)을 구현하는데 사용

- 데이터베이스 색인화: 디스크 기반 데이터 구조 및 데이터베이스 인덱스에 사용

- 캐시: 캐시, 보조 데이터 테이블을 구현하는데 사용

- 세트 데이터 구조 구현: 특정 키가 특정 키 집합에 속하는지 여부를 기록하는 세트 데이터 구조 구현, 정적 집합과 동적 집합 구현

- 개체 표현: 펄, 파이썬, js, 루아, 루비에서는 해시테이블을 사용하여 개체를 구현

---

## 프로그래밍 언어에서의 Hash Table

이미 수많은 프로그로그래밍 언어에 이미 내재되어 있다

![img](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/d87fa0fc-0355-4870-ad6d-441b337e4f36)

### 자스로 해시테이블 구현

<code>
<pre>
// 해시 테이블 생성
let hashTable = {};

// 요소 추가
hashTable["apple"] = 1;
hashTable["banana"] = 2;
hashTable["orange"] = 3;

// 요소 조회
console.log(hashTable["apple"]); // 1
console.log(hashTable["banana"]); // 2
console.log(hashTable["orange"]); // 3

// 요소 수정
hashTable["apple"] = 4;
console.log(hashTable["apple"]); // 4

// 요소 삭제
delete hashTable["banana"];
console.log(hashTable["banana"]); // undefined (존재하지 않는 키의 경우 undefined 반환)
</code>

</pre>

### 파이썬으로 해시테이블 구현

<code>
<pre>

// 해시 테이블 생성
hash_table = {}

// 요소 추가
hash_table["apple"] = 1
hash_table["banana"] = 2
hash_table["orange"] = 3

// 요소 조회
print(hash_table["apple"]) # 1
print(hash_table["banana"]) # 2
print(hash_table["orange"]) # 3

// 요소 수정
hash_table["apple"] = 4
print(hash_table["apple"]) # 4

// 요소 삭제
del hash_table["banana"]
print(hash_table.get("banana")) # None
</code>

</pre>

### GO로 해시테이블 구현

<code>
<pre>
package main

import "fmt"

func main() {
// 해시 테이블 생성
hashTable := make(map[string]int)

    // 요소 추가
    hashTable["apple"] = 1
    hashTable["banana"] = 2
    hashTable["orange"] = 3

    // 요소 조회
    fmt.Println(hashTable["apple"])   // 1
    fmt.Println(hashTable["banana"])  // 2
    fmt.Println(hashTable["orange"])  // 3

    // 요소 수정
    hashTable["apple"] = 4
    fmt.Println(hashTable["apple"])   // 4

    // 요소 삭제
    delete(hashTable, "banana")
    fmt.Println(hashTable["banana"])  // 0 (존재하지 않는 키의 경우 기본값인 0 반환)

}
</code>

</pre>

---

## 그래서 Hash란?

해시는 해시함수와 같은 말이다(짧게 말하면 Hash, 길게 말하면 Hash fuction)

이는 임의의 길이를 갖는 임의의 데이터를 고정된 길이의 데이터로 매핑하는 단방향 함수를 말한다

아무리 큰 숫자를 넣어도 정해진 크기의 숫자가 나오는 함수를 말한다

이러한 해시함수를 적용하여 나온 고정된 길이의 값을

해시값, 해시코드, 해시섬(sum), 체크섬이라고 부른다

### 대표적인 해시 함수의 종류

1. MD5 (Message Digest Algorithm 5):
   - MD5는 입력 데이터의 메시지 다이제스트를 생성하는 알고리즘
   - 원래는 메시지 무결성을 검증하는 데 사용되었으나, 현재는 주로 데이터의 무결성 검사와 비밀번호 등의 저장에 사용
   - 입력 데이터의 임의의 길이를 가진다면, MD5는 128비트 고정 길이의 다이제스트를 생성
   - MD5 알고리즘은 충돌 저항성이 낮기 때문에 보안 목적으로 사용되는 데에는 적합하지 않음
2. SHA (Secure Hash Algorithm):
   - SHA는 안전한 해시 알고리즘으로, 데이터의 무결성을 보장하기 위해 사용
   - 원래는 SHA-0라고 알려진 알고리즘 이후, SHA-1, SHA-2, SHA-3 등의 버전이 개발
   - SHA-1은 160비트 다이제스트를 생성하며, 보안상의 약점이 발견되어 현재는 권장되지 않음
   - SHA-2는 SHA-256, SHA-384, SHA-512 등 다양한 비트 수의 다이제스트를 생성할 수 있는 알고리즘으로, 널리 사용
   - SHA-3는 미국 국립표준기술연구소(NIST)에 의해 선택된 최신 SHA 알고리즘으로, 다이제스트의 길이를 자유롭게 선택 가능

---

## Hash Table 구조

위 실사용예시에서 Hash Table과 array가 마치 다른 것처럼 말했지만

Hash Table에는 array를 내부 구조로 갖고 있다

array의 index를 통해서 값에 접근하는 방식을 array와 동일하게 갖고 있다

그런데 어떻게 더 빠를 수 있을까 답은 Hash function에 있다

## 구현 원리

![img](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/ef3d379e-f0a2-4c62-ba78-e22eab638d47)
해시테이블이란 검색하고자 하는 key값을 해시함수를 돌려서 나온 hashcode를 인덱스로 환산해서 데이터(value)에 접근한다

예시를 통해 알아보자
![img](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/a13e1142-d286-4fd4-b386-088e9da5858e)
모니카는 다이어트를 시작했다

그래서 먹을 수 있는 음식 리스트를 만들려고 한다

현재 egg, apple, tomato, pizza 네 가지 종류를 정리하려고 한다

egg를 저장하기 위해서 알파벳 수자를 세어보았다

3이라는 숫자가 도출되어, 이를 기준으로 index에 넣는다

value에는 egg의 가격을 적었다

![img](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/c85fe332-4242-47e7-a8e3-13e0844d5025)
나중에 egg의 가격이 궁금하면 egg의 key를 Hash Function에게 주면

Hash Function은 3이라는 숫자를 준다

그럼 index 3을 찾으면 $4라는 가격을 알 수 있다

마찬가지로 apple의 값과 tomato의 값도 입력을 했다
![img](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/e0c0604b-1cf0-4b72-82b3-2615eaf879c3)
<b>근데 문제발생

치팅데이 때 먹으려고 억지로 메뉴에 넣었던 pizza가 apple과 똑같은 index 5를 갖는다

피자의 가격은 $11이라 이를 입력하고자 했는데

이미 인덱스 5에 apple의 가격인 $7을 저장해 두어서 Collision(해시 충돌)이 일어난다

<b>대표적인 해결법

겹치는 리스트 공간에 또 다른 배열을 넣는 방법, 즉 2개의 쌍을 넣는 방법
![img](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/da6b2279-60cb-4322-b2ac-3f4b71179fe9)
key와 value를 해시함수에 넣고(여기서는 apple= key, $7= value)

Hash fuction이 '5'라는 숫자를 줄 것이고, 리스트의 5로 이동하여 거기서 선형검색을 진행한다

apple 또는 pizza의 가격을 찾을 때까지 찾는다

### 해시 충돌을 해결하는 방법

![image](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/8b420437-0a36-4b39-94ea-c38ecdc2dfce)

충돌이 발생하면 해당 버킷(해시 테이블의 총 칸)을 링크드리스트로 연결함
c++이나 자바와 같은 언어에서 주로 사용
<code>

<pre>
//자바 예시 코드
import java.util.LinkedList;

class Node {
    String key;
    int value;

    public Node(String key, int value) {
        this.key = key;
        this.value = value;
    }
}

class HashTable {
    private int size;
    private LinkedList<Node>[] table;

    public HashTable(int size) {
        this.size = size;
        this.table = new LinkedList[size];
        for (int i = 0; i < size; i++) {
            table[i] = new LinkedList<>();
        }
    }

    private int hashFunction(String key) {
        // 간단한 해시 함수 예시: 문자열의 각 문자의 아스키 값을 더한 후, 크기로 나눈 나머지 반환
        int hash = 0;
        for (char c : key.toCharArray()) {
            hash += (int) c;
        }
        return hash % size;
    }

    public void put(String key, int value) {
        int index = hashFunction(key);
        LinkedList<Node> list = table[index];
        for (Node node : list) {
            if (node.key.equals(key)) {
                node.value = value;
                return;
            }
        }
        list.add(new Node(key, value));
    }

    public Integer get(String key) {
        int index = hashFunction(key);
        LinkedList<Node> list = table[index];
        for (Node node : list) {
            if (node.key.equals(key)) {
                return node.value;
            }
        }
        return null;
    }
}

public class Main {
    public static void main(String[] args) {
        HashTable hashTable = new HashTable(10);

        // 데이터 추가
        hashTable.put("apple", 5);
        hashTable.put("banana", 10);
        hashTable.put("orange", 7);

        // 데이터 조회
        System.out.println(hashTable.get("apple"));   // 5
        System.out.println(hashTable.get("banana"));  // 10
        System.out.println(hashTable.get("orange"));  // 7
        System.out.println(hashTable.get("grape"));   // null (존재하지 않는 키)

        // 데이터 업데이트
        hashTable.put("apple", 3);
        System.out.println(hashTable.get("apple"));   // 3
    }
}

</code>
</pre>

![image](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/3b9841d4-2e67-4274-b2d4-3090a00cab1d)

<code>
<pre>
//파이썬 예시 코드
class HashTable:
    def __init__(self, size):
        self.size = size
        self.keys = [None] * size
        self.values = [None] * size

    def hash_function(self, key):
        # 간단한 해시 함수 예시: 문자열의 각 문자의 아스키 값을 더한 후, 크기로 나눈 나머지 반환
        return sum(ord(c) for c in key) % self.size

    def put(self, key, value):
        index = self.hash_function(key)
        while self.keys[index] is not None:
            if self.keys[index] == key:
                self.values[index] = value
                return
            index = (index + 1) % self.size
        self.keys[index] = key
        self.values[index] = value

    def get(self, key):
        index = self.hash_function(key)
        while self.keys[index] is not None:
            if self.keys[index] == key:
                return self.values[index]
            index = (index + 1) % self.size
        return None

</code>
</pre>

![image](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/28da95e2-a666-43ec-a260-6d98038166e9)

![image](https://github.com/songhee-lee/2023-CS-Study/assets/104298444/cfacdb69-d5ad-4de7-b8ce-4ecfa09950c2)

### 파이썬 딕셔너리에서 사용하는 해시 함수는 무엇인가?

- hash()함수를 사용함

- 정수타입은 정수로 반환, 문자열 타입은 내용을 해시하여 정수 값 반환, 튜플타입은 순서대로 해시하여 정수값으로 계산

- 사용자가 만든 클래스의 인스턴스같이 해시 불가능한 객체는 'TypeError'발생, 사용하려면 직접 hash매서드를 구현해야 함
