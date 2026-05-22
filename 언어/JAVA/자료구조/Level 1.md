# 1. 배열 (Array)

배열은:

> 같은 타입 데이터를 연속된 메모리에 저장하는 자료구조

야.

---

## 특징

| 특징    | 설명         |
| ----- | ---------- |
| 크기 고정 | 생성 후 변경 불가 |
| 빠른 접근 | index 사용   |
| 순서 있음 | 0부터 시작     |

---

## 생성

```java
int[] arr = new int[5];
```

메모리:

```text
[0][0][0][0][0]
```

---

## 값 저장

```java
arr[0] = 10;
arr[1] = 20;
```

---

## 출력

```java
System.out.println(arr[0]);
```

---

## 전체 코드

```java
public class Main {
    public static void main(String[] args) {

        int[] arr = new int[3];

        arr[0] = 10;
        arr[1] = 20;
        arr[2] = 30;

        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    }
}
```

---

## 시간복잡도

| 동작 | 시간   |
| -- | ---- |
| 접근 | O(1) |
| 탐색 | O(n) |

---

# 2. 문자열 (String)

문자들의 집합.

Java에서는:

```java
String s = "hello";
```

처럼 사용.

---

## 특징

* immutable(불변)
* 수정 시 새 객체 생성

---

## 주요 메서드

## 길이

```java
s.length();
```

---

## 문자 가져오기

```java
s.charAt(0);
```

---

## 포함 여부

```java
s.contains("he");
```

---

## 부분 문자열

```java
s.substring(0, 2);
```

---

## 예제

```java
public class Main {
    public static void main(String[] args) {

        String s = "hello";

        System.out.println(s.length());
        System.out.println(s.charAt(1));
        System.out.println(s.substring(0, 2));
    }
}
```

---

# 3. 리스트 (List)

배열의 단점:

```text
크기 변경 불가
```

를 해결한 동적 배열.

Java에서는 보통:

```java
ArrayList
```

사용.

---

## 선언

```java
List<Integer> list = new ArrayList<>();
```

---

## 추가

```java
list.add(10);
```

---

## 조회

```java
list.get(0);
```

---

## 삭제

```java
list.remove(0);
```

---

## 전체 코드

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        List<Integer> list = new ArrayList<>();

        list.add(10);
        list.add(20);
        list.add(30);

        System.out.println(list.get(1));

        for (int num : list) {
            System.out.println(num);
        }
    }
}
```

---

## 배열 vs 리스트

| 배열    | 리스트      |
| ----- | -------- |
| 크기 고정 | 크기 변경 가능 |
| 빠름    | 조금 느림    |
| 단순    | 기능 많음    |

---

# 4. 스택 (Stack)

> 마지막에 넣은 데이터를 먼저 꺼내는 구조

LIFO:

```text
Last In First Out
```

---

## 예시

```text
1 넣기
2 넣기
3 넣기

꺼내면:
3
2
1
```

---

## 사용처

* 괄호 검사
* 뒤로가기
* DFS

---

## 주요 메서드

| 메서드  | 설명     |
| ---- | ------ |
| push | 넣기     |
| pop  | 꺼내기    |
| peek | 맨 위 확인 |

---

## 코드

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        Stack<Integer> stack = new Stack<>();

        stack.push(10);
        stack.push(20);
        stack.push(30);

        System.out.println(stack.pop());

        System.out.println(stack.peek());
    }
}
```

---

## 동작 과정

```text
push(10)
[10]

push(20)
[10, 20]

pop()
20 제거
```

---

# 5. 큐 (Queue)

> 먼저 넣은 데이터를 먼저 꺼냄

FIFO:

```text
First In First Out
```

---

## 예시

```text
1 넣기
2 넣기
3 넣기

꺼내면:
1
2
3
```

---

## 사용처

* BFS
* 작업 처리
* 대기열

---

## Queue 선언

보통 LinkedList 사용.

```java
Queue<Integer> queue = new LinkedList<>();
```

---

## 주요 메서드

| 메서드   | 설명   |
| ----- | ---- |
| offer | 넣기   |
| poll  | 꺼내기  |
| peek  | 앞 확인 |

---

## 코드

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        Queue<Integer> queue = new LinkedList<>();

        queue.offer(10);
        queue.offer(20);
        queue.offer(30);

        System.out.println(queue.poll());

        System.out.println(queue.peek());
    }
}
```

---

## 동작 과정

```text
offer(10)
[10]

offer(20)
[10, 20]

poll()
10 제거
```
