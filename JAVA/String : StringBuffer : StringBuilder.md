# String / StringBuffer / StringBuilder

> Java에서 문자열을 다루는 대표적인 클래스들이다.

❗️ 연산횟수가 많아지거나 멀티쓰레드, Race condition 등의 상황이 자주 발생하는 경우  
💡 각 클래스의 특징을 이해하고 상황에 맞게 적절한 클래스를 사용하자

<br/>

## String

> String은 불변의 속성을 갖는다.

```java
String str = "Hello";
str = str + "World!";
```

- String 클래스의 참조변수 str에는 "Hello" 값이 들어가 있다.
- "Hello World!"라는 값을 가지고 있는 <b>새로운 메모리 영역</b>을 가리키도록 변경된다.
- 처음 선언했던 "Hello" 값이 할당되어 있는 메모리 영역을 Garbage로 남아있다가 가비지 컬렉션에 의해서 사라지게 된다.

💡 String 클래스는 불변이기 때문에 문자열을 수정하는 시점에 <b>새로운 String 인스턴스가 생성</b>되는 것이다.

📌 변하지 않는 문자열을 자주 읽어들이는 경우 String을 사용하면 좋은 성능을 기대할 수 있다.  
❗️ 문자열 추가/수정/삭제 등의 연산이 자주 발생하는 경우, 힙 메모리에 많은 임시 가비지가 생성되어 힙 메모리 부족으로 이어지고, 이는 어플리케이션 성능에 치명적인 영향을 끼친다.

<br>

## StringBuffer 🆚 StringBuilder

차이점

> <h3>동기화의 유무</h3>
> StringBuffer는 동기화 키워드를 지원해서 <b>멀티쓰레드 환경</b>에서 안전하다. (thread - safe)

> StringBuilder는 동기화를 지원하지 않아서, <b>단일쓰레드 성능이 좋다.</b>

<br>

## 요약

- String : 문자열 연산이 적은 멀티쓰레드 환경
- StringBuffer : 문자열 연산이 많은 멀티쓰레드 환경
- StringBuilder : 문자열 연산이 많고, 단일쓰레드 환경이거나 동기화를 고려하지 않아도 되는 경우

| ✓            | String        | StringBuffer | StringBuilder |
| ------------ | ------------- | ------------ | ------------- |
| 저장소       | String pool   | Heap         | Heap          |
| 수정         | No(Immutable) | Yes(Mutable) | Yes(Mutable)  |
| Tread-safe   | 안전          | 안전         | 안전하지 않음 |
| Synchronized | Yes           | Yes          | No            |
| Performance  | 빠르다        | 느리다       | 빠르다        |

<br>
<br>

<hr/>

### 예상 질문

📌 StringBuffer와 StringBuilder의 차이점은 무엇인가요?

> 둘 다 문자열 연산이 많은 경우 사용되지만, StringBuffer는 멀티쓰레드 환경에서 유리하고 StringBuilder는 단일쓰레드 환경이나 동기화를 고려하지 않아도 되는 경우에 사용합니다.
