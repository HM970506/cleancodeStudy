> 깨끗한 클래스를 만드는 방법을 설명한다.🐑

# 클래스 체계
클래스를 정의할 때 순서

1. 변수 목록
: 공개 변수는 거의 필요하지 않다.
- static public 상수
- private 변수
- private instance 변수

2. 공개 함수
- 비공개 함수는 자신을 호출하는 공개 함수 직후에 넣는다.

## 캡슐화
변수와 유틸리티 함수는 숨기는 것이 좋지만 반드시 숨겨야 하는 것은 아니다.
때로는 protected로 선언해 테스트 코드에 접근을 허용하기도 한다.

그래도, 캡슐화를 풀어주는 것은 가장 최후의 방법이다.
> **protected**
: 같은 package인 경우 사용이 가능하다. 다른 package인 경우, 상속 관계에 있으면 사용이 가능하다.

# 클래스는 작아야 한다
클래스를 만들 때 첫 번째 규칙은 **크기**이다. 클래스는 최대한 작아야 한다.
클래스가 맡은 책임으로 크기를 판단한다.
클래스 이름에는 해당 클래스의 책임을 기술해야 한다. 간결한 이름이 떠오르지 않는다면 클래스의 책임이 많은 것이다.

## 단일 책임 원칙(Single Responsibility Principle)
: 클래스나 모듈을 변경할 이유가 단 하나뿐이어야 한다는 원칙

많은 개발자가 프로그램이 돌아가면 일이 끝났다고 여긴다. '깨끗하고 체계적인 소프트웨어'를 만들기 위해 노력해야 한다.

규모가 큰 시스템을 관리하기 위해서는 체계적인 정리가 필수이다. 개발자가 무엇이 어디에 있는지 쉽게 찾을 수 있다.

> 큰 클래스 몇 개 보다 작은 클래스 여럿으로 이루어진 시스템이 바람직하다.

## 응집도
: 모듈의 독립성을 나타내는 개념으로, 모듈 내부 구성요소 간 연관 정도를 나타낸다.

응집도가 높다는 것은 클래스에 속한 메서드와 변수가 서로 의존하며 논리적인 의미로 묶인다는 의미이다.
클래스의 메서드에서 인스턴스 변수를 더 많이 사용할 수록 응집도가 높다고 할 수 있다.

- 응집도가 높은 클래스
```java
public class Stack {
	private int topOfStack = 0;
    List<Integer> elemnets = new LinkedList<Integer>();
    
    public int size() {
    	return topOfStack;
    }
    
    public void push(int element) {
    	topOfStack++;
        elements.add(element);
    }
    
    public int pop() throws PoppedWhenEmpty {
    	if (topOfStack == 0)
        	throw new PoppedWhenEmpty();
        int element = elements.get(--topOfStack);
        elements.remove(topOfStack);
        return element;
    }
}
```
: size()를 제외한 모든 메서드가 두 변수를 사용하고 있다.

> 응집도가 높아지도록 변수와 메서드를 적절히 분리해 클래스를 쪼개준다.

> 응집도를 유지하면 작은 클래스 여럿이 나온다

# 변경하기 쉬운 클래스
대부분은 시스템은 지속적으로 변경된다. 클래스를 깨끗하게 만들어 변경에 따르는 위험을 낮추도록 해야 한다.
클래스들을 분리 시켜서 시스템이 변경되더라도 기존 코드는 변경하지 않아도 되게 한다.

## 변경으로부터 격리
클래스는 구체적인 클래스와 추상 클래스로 나눌 수 있다. 구체적인 클래스는 상세한 구현을 포함하고 있고, 추상 클래스는 개념만 포함한다.
구체적인 클래스는 테스트가 어렵다. 
=> 테스트가 가능할 정도로 시스템의 결합도를 낮춘다.
=> 추상 클래스로 구현