> 오류 처리는 프로그램에서 반드시 필요한 요소이다. 프로그램이 잘못되면 바로 잡을 책임은 프로그래머에게 있다.

# 오류 코드보다 예외를 사용하라
: 오류를 발견하면 예외를 던진다.

# Try-Catch-Finally 문부터 작성하라
try 블록은 트랜잭션과 비슷하다. try 안에서 문제가 생기면 예외를 던지게 된다. 예외를 일으키는 테스트 케이스를 작성해 테스트 케이스를 통과할 수 있게 코드를 작성하도록 한다.

# 미확인 예외를 사용하라
확인된 예외보다는 확인되지 않은 예외를 던져야 한다.

# 예외에 의미를 제공하라
예외를 던지는 오류 메시지에 오류가 발생한 정보를 담아서 던진다.

# 호출자를 고려해 예외 클래스를 정의하라
오류를 분류하는 기준은 여려가지가 있다. 가장 중요한 것은 오류를 어떻게 잡아낼지 이다. 중복되는 예외를 던지지 않도록 조심해야 한다.

# 정상 흐름을 정의하라
때로는 예외처리로 프로그램이 중단되는 것이 적합하지 않은 경우도 있다.
예외적인 상황을 처리하지 않아도 되는 상황에서는 예외처리를 하지 않아도 된다.

# null을 반환하지 마라
한 줄에 하나씩 계속해서 null을 확인하는 코드는 좋지 않다.
최대한 NullPointerException이 발생하지 않도록 해야한다.

# null을 전달하지 마라
method에서 null을 전달하는 것은 무조건 피해야 한다.

- 두 지점 사이의 거리를 계산하는 코드
```java
public class MetricsCalculator {
	public double xProjection(Point p1, Point p2) {
    	return (p2.x - p1.x) * 1.5;
    }
    ...
}
```
여기에서 누군가 인수로 null을 전달하게 되면 NullPointerException이 발생한다.
```java
calculator.xProjection(null, new Point(12, 13));
```

이렇게 결과로 null이 전달되면 안된다.

- 대안
: null이 인수로 전달되었는지 먼저 확인한다.
```java
public class MetricsCalculator {
	public double xProjection(Point p1, Point p2) {
    	if (p1 == null || p2 == null) {
        	throws InvalidArgumentException(
            	"Invalid argument for MetricsCalculator.xProjection");
        }
        return (p2.x - p1.x) * 1.5;
    }
}
```