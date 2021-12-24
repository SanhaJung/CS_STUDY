# Dirty Checking

### **Dirty Checking이란?**

---

<br>

> Dirty Checking이란 Entity의 변경이 일어나면, 변경 내용을 자동으로 데이터베이스에 반영하는 JPA의 특징이다. 여기서 Dirty는 상태의 변화가 생겼다는 뜻으로 이해하면 편하다.

<br>

※ JPA(Java Persistence API)는 자바 진영에서 ORM(Object-Relational Mapping) 기술 표준으로 사용되는 인터페이스의 모음이다.
<br>
참고 : https://skyblue300a.tistory.com/7

<br>

### **Dirty Checking의 예시**

---

<br>

```
// 주문을 취소하는 메소드
@Transactional
public void cancelOrder(Long orderId) {
    //주문 엔티티 조회
    Order order = orderRepository.findOne(orderId);

    //주문 취소
    order.cancel();
}
```

해당 메소드를 그대로 해석해보면 orderId로 주문내역을 찾고, cancel() 메소드를 통해 주문을 취소한다는 뜻인데, Dirty Checking으로 인해 JPA가 해당 트랜잭션이 종료될 때 자동으로 변경된 내역을 탐지하고, 변경된 내역이 있으면 해당 Entity를 데이터베이스에 update 해준다.

#### **구체적인 진행 과정**

```
1. JPA에서 Entity를 조회한다.
2. 조회한 Entity의 스냅샷을 생성한다.
3. 트랙잭션이 끝나는 시점에 해당 스냅샷과 Entity를 비교한다.
4. 만약 다른 점이 있다면 Entity를 update한다.
```

이러한 Dirty Checking은 영속성 컨텍스트가 관리하는 Entity들을 대상으로 적용된다.

<br>

※영속성 컨텍스트는 Entity를 영구 저장 하는 환경 이라는 뜻으로, 애플리케이션이 데이터베이스에서 꺼내온 객체를 보관하는 역할을 한다. Entity Manager를 통해 Entity를 조회하거나 저장할 때 Entity를 보관하고 관리한다.
<br>
(Entity Manager에서 detach된 Entity를 준영속, DB에 반영되기 전 처음으로 생성된 Entity를 비영속이라고 한다.)
<br>

### **@DynamicUpdate**

---

<br>

Dirty Checking에서 실행하는 update문의 경우 Entity의 모든 내용을 update해 필드가 많을 경우 부담이 갈 수 있기 때문에, 이 경우 해당 Entity의 클래스에 @DynamicUpdate 어노테이션을 추가하면 변경된 필드만 update할 수 있다.

<br>

### **예상 질문**

---

📌 Dirty Checking이란 무엇인가요?

> Dirty Checking이란 Entity의 변경이 일어나면, 변경 내용을 자동으로 데이터베이스에 반영하는 JPA의 특징입니다.

 <br>
