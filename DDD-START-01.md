# 1. 도메인 모델 시작





## 도메인



## 도메인 모델

### 도메인 모델 패턴

| 계층                                         | 설명                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| 사용자인터페이스(UI) 또는 표현(Presentation) | 사용자의 요청을 처리하고 사용자에게 정보를 보여준다. 여기서 사용자는 소프트웨어를 사용하는 사람붑ㄴ만 아니라 외부 시스템도 사용자가 될 수 있다. |
| 응용(Application)                            | 사용자가 요청한 기능을 실행한다. 업무 로직을 직접 구현하지 않으며 도메인 계층을 조합해서 기능을 실행한다. |
| 도메인                                       | 시스템이 제공할 도메인의 규칙을 구현한다.                    |
| 인프라스터럭쳐                               | 데이터베이스나 메시징 시스템과 같은 외부 시스템과의 연동을 처리한다. |



### 도메인 모델 도출



## 엔티티와 벨류

## 엔티티

### 엔티티의 식별자 생성



* 특정 규칙에 따라 생성

* UUID 사용

* 값을 직접 입력

* 일련번호 사용(시퀀스나 DB의 자동 증가 컬럼 사용)

  

### 벨류 타입

```java
public class ShippingInfo {
  //받는 사람
  private String receiverName;
  private String receiverPhoneNumber;
  
  //주소
  private String shippingAddress1;
  private String shippingAddress2;
  private String shippingZipCode;
}



//불변 객체로 만든다.
@AllArgConstructor
@Getter
class Receiver {
  private String name;
  private String phoneNumber;  
}
//불변 객체로 만든다.
@AllArgConstructor
@Getter
class Address {
 	private String address1;
  private String address2;
  private String zipcode;
}


@AllargConstructor
@Getter
public class ShippingInfo {
  //받는 사람
  private Receiver receiver;
  
  //주소
  private Address address;
}
```





### 엔티티 식별자와 밸류 타입



```java
public class Order{
  //orderNo 타입 자체로 id가 주문번호임을 알수 있다.
  private OrderNo id;
  
}
```



### 도메인 모델에 set 메서드 넣지 않기

```java
/*
*  습관적인 get/set 메서드 만들기. 
*/

@Getter
@Setter
public class UserInfo {
  private String id;
  private String name;  
}
```



```java
public class Order {
  public void changeShippingInfo() {} 
  -> 
  public void setShippingInfo(ShippingInfo newShipping) {...}
  
  
  public void completePayment() {}
  -> 
  public void setOrderState(OrderState orderState) {...} 
  
}
```



### 도메인 용어

```java 
public enum OrderState{
  STEP1, STEP2, STEP3, STEP4, STEP5;
}

//도메인 용어를 사용하여 가독성 및 불필요한 변환 과정을 생략 하
public enum OrderState {
  PAYMENT_WATING, PREPARING, SHIPPED, DELIVERING, DELIVERY_COMPLETE;
}
```





