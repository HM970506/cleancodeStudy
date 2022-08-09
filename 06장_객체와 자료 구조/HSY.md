> Java에서는 field를 private으로 설정하여 밖에서 맘대로 바꿀 수 없게 설정한다.
그렇다면 get 함수와 set 함수를 public으로 설정해 비공개 field를 왜 외부에 노출할까?

# 자료 추상화
: 단순히 private을 사용해서 변수를 감추는 것은 좋지 않다. <mark style='background-color: #fff5b1'> 추상 인터페이스</mark>를 사용하여야 한다. 자료를 자세하게 공개하지 않고, 추상적인 개념을 표현하여야 한다.
아무 생각 없이 조회/설정 함수를 추가해서는 안된다.

- 구체적인 Point 클래스
: 확실하게 직교 좌표계를 사용한다는 것을 알 수 있다.
```java
public class Point {
	public double x;
    public double y;
}
```
- 추상적인 Point 클래스
: interface로 나타내면 구현하는 것에 따라 달라지기 때문에 어떤 종류의 좌표계를 사용하는지 알 수 없게 된다.
```java
public interface Point {
	double getX();
    double getY();
    void setCartesian(double x, double y);
    double getR();
    double getTheta();
    void setPolar(double r, double theta);
}
```
# 자료 / 객체 비대칭
객체 - 추상화 뒤로 자료를 숨긴 채, 자료를 다루는 함수만 공개한다.
자료구조 - 자료는 그대로 공개하고, 별다른 함수를 제공하지는 않는다.

- 절차적인 코드
: 기존 자료 구조를 변경하지 않고도 새 함수를 추가하기가 쉽다.

- 객체지향 코드
: 기존 함수를 변경하지 않으면서 새 클래스를 추가하는 것이 쉽다.

새로운 자료 타입이 필요한 경우에는 객체지향 코드가, 새로운 함수가 필요한 경우에는 절차적인 코드가 좀 더 적합하다.

# 디미터 법칙
: 객체는 조회 함수로 내부 구조를 공개해서는 안된다.

class C가 존재할 때 그 안의 method f는 아래 객체의 method만 호출해야 한다.
- class C
- f가 생성한 객체
- f 인수로 넘어온 객체
- C instance 변수에 저장된 객체

> 낯선 사람은 경계하고 친한 친구랑만 놀아라👯‍♀️

## 기차 충돌
```java
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```
위와 같이 함수가 반환한 객체의 함수를 다시 호출하는 코드는 좋지 않다.
아래와 같이 나누는 것이 좋다.
```java
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```

## 잡종 구조
: 절반은 객체, 절반은 자료구조
사용해서는 안된다.

## 구조체 감추기
: 무언가를 하라고 명령하고, 내부 구조를 드러내서는 안된다.

# 자료 전달 객체
> **자료 구조체 / 자료 전달 객체(DTO, Data Transfer Object)**
: 공개 변수만 존재하고 함수는 없는 클래스

데이터베이스와 통신하거나 소켓에서 받은 메시지 구문을 분석할 때 유용하게 사용된다.

> **빈 구조**
: 자료 전달 객체의 조금 더 일반적인 형태로, 비공개 변수(private)를 조회/설정 함수로 조작한다.
ex) Getter, Setter

## 활성 레코드
: DTO의 특수한 형태
공개변수가 있거나, 비공개 변수에 조회/설정 함수가 있거나, save/find 같은 탐색 함수를 제공한다. 활성 레코드는 자료구조로 취급한다.