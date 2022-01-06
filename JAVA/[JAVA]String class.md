# 문자열 클래스





## 1. 문자열 클래스의 종류

* String, StringBuffer, StringBuilder 3가지
* 상황에라 어떤 클래스를 쓰냐에 따라, 성능차이가 발생



## 2. String vs StringBuffer vs StringBuilder

| Index        | String                       | StringBuffer     | StringBuilder    |
| ------------ | ---------------------------- | ---------------- | ---------------- |
| Storage Area | Heap or Constant String Pool | Heap             | Heap             |
| Modifable    | No(**immutable**)            | Yes(**mutable**) | Yes(**mutable**) |
| Thread-Safe  | YES                          | YES              | NO               |

String과 다른 클래스(StringBuffer, StringBuilder)의 가장 큰 차이는 **String은 Immutable(불변), StringBuffer, StringBuilder는 Mutable(가변)**에 있습니다.

#### Thread

> 제어의 흐름

#### Thread-Safe

>  Multi Thread 프로그래밍에서 여러 Thread로 부터 어떤 method, variable, object에 동시에 접근이 이루어져도 프로그램의 실에에 문제가 없음





## 3. String Class

String 객체는 한번 생성되면 할당된 메모리 공간이 변하지 않음 즉, '+' 연산 또는 concat 메서드를 통해 기존에 생성된 String 객체에 다른 문자열을 붙여도 기존 문자열에 새로운 문자열을 붙이는 것이 아님

새로운 String 객체를 만든 후, 이 객체에 연결된 문자열을 저장하고, 그 객체를 참조하도록 함

- 장점
  - String Class의 객체는 Immutable(불변)
    - 단순하게 읽어가는 조회 연산에서는 타 클래스보다 빠르게 읽음
    - 멀티쓰레드 환경에서 동기화를 신경 쓸 필요가 없습니다. (Thread-Safe)
- 단점
  - 문자열 연산('+', concat 등)을 많이 일어나는 경우, 더이상 참조되지 않는 기존 객체는 Garbage Collection(이하, GC)에 의해 제거되야하기 때문에 성능이 좋지 않음
  - 또한, 문자열 연산이 많아질 때 연산 내부적으로 char 배열을 사용하고, 계속해서 객체를 만드는 오버헤드가 발생하므로 성능이 떨어질 수 밖에 없습니다.



## 3. StringBuffer와 StringBuilder Class

* StringBuffer와 StringBuilder 클래스는 String과 다르게 mutable(변경가능) 즉, 문자열 연산에 있어서 클래스를 한번만 만들고, 연산이 필요할 때 크기를 변경시켜서 문자열을 변경--> 문자열 연산이 자주 있을 때 사용하면 성능이 좋음

* StringBuffer와 StringBuilder 클래스가 제공하는 메서드 동일

* 차이점은 **동기화 여부**

  * 동기화

  * > 하나 이상의 Thread가 어떤 로직에 동시에 접근했을때 연산에 대한 값의 무결성을 보장하기 위해 수행하는 영역에 lock을 걸어주는 것

* **StringBuffer**는 각 메서드별로 Synchronized Keyword가 존재하여, Multi-Thread 환경에서도 동기화를 지원하여 Thread-Safe합니다.

* **StringBuilder**는 동기화를 보장하지 않음
  *  하지만 StringBuilder는 Single-Thread 환경에서 동기화를 고려하지 않기 때문에 StringBuffer에 비해 연산처리가 빠릅니다.

```
그렇기 때문에 Multi-Thread 환경이라면 값 동기화 보장을 위해 StringBuffer를 사용하고, Single-Thread 환경이라면 StringBuilder를 사용하는 것이 좋습니다.
```



## Conclusion

* String Class는 JDK 1.5버전 이전에 문자열연산('+', concat)을 할 때에는 조합된 문자열을 새로운 메모리에 할당하여 참조함으로 인해서 성능상의 이슈존재

*  **JDK1.5 버전 이후에는 컴파일 단계에서 String 객체를 사용하더라도 StringBuilder로 컴파일 되도록 변경**됨

  --> JDK 1.5 이후 버전에서는 String 클래스를 활용해도 StringBuilder와 성능상으로 차이가 없지만 반복 루프를 사용해서 문자열을 더할 때에는 객체를 계속 추가한다는 사실에는 변함이 없음

* String Class를 쓰는 대신, Thread와 관련이 있으면 StringBuffer를, Thread 안전 여부와 상관이 없으면 StringBuilder를 사용하는 것을 권장합니다.

```
단순히 성능만 놓고 본다면 연산이 많은 경우, StringBuilder > StringBuffer >>> String 라고 합니다.
```

## 질문

- JAVA의 3가지 문자열 클래스에 대해 간략하게 설명하세요.
- 각 문자열 클래스의 차이점에 대해 설명을 설명하세요.