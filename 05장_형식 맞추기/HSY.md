> 개발자라면 코드를 짤 때 규칙을 정하고 그 규칙에 따라서 깔끔하게 코드를 짜야 한다.

# 형식을 맞추는 목적
코드의 형식은 의사소통의 일환이다. 코드가 바뀌더라도 코드의 형식은 유지보수와 확장성에 영향을 미친다. 
원활한 의사소통을 위해서는 코드 형식을 잘 정해야 한다.
# 적절한 행 길이를 유지하라
코드의 길이가 길지 않더라도 충분히 복잡한 시스템을 구축할 수 있다. 일반적으로는 코드의 길이가 긴 것보다 짧은 것이 낫다.
## 신문 기사처럼 작성하라
표제를 보고 기사를 읽을지 정하는 것처럼 소스 파일의 이름만 보고도 사용할 수 있는 코드인지 확인할 수 있게 정해야 한다.
소스코드의 처음부터 밑으로 내려갈수록 의도를 세세하게 적는다.
## 개념은 빈 행으로 분리하라
코드는 왼쪽에서 오른쪽, 위에서 아래로 읽는다. 여러 행들이 묶여서 완성된 생각 하나를 나타낸다. 생각 사이에는 빈 행을 넣어서 분리해야 한다.
- 잘못된 예시
```java
package fitnesse.wikitext.widgets;
import java.util.regex.*;
public class BoldWidget extends ParentWidget {
	...
}
```
- 올바른 예시
```java
package fitnesse.wikitext.widgets;

import java.util.regex.*;

public class BoldWidget extends ParentWidget {
	...
}
```
## 세로 밀집도
서로 연관이 있는 코드 행은 세로로 가까이 배치해야 한다.
## 수직 거리
서로 밀접한 개념은 세로로 가까이 배치해야 한다. 같은 개념인데 다른 파일에 존재하면 확인하기 위해 계속 옮겨다녀야 한다.

## 변수 선언
사용하는 위치와 가깝게 선언한다.

지역 변수 : 함수의 맨 처음에 선언한다.
루프문 제어 변수 : 루프문 내부

### 인스턴스 변수
: 클래스 맨 처음에 선언한다.

### 종속 함수
: 한 함수가 다른 함수를 호출하는 경우, 두 함수는 세로로 가깝게 배치해야 한다. 호출하는 함수가 호출되는 함수 위에 배치되게 한다.
```java
public Response makeResponse(FitNesseContext context, Request request) {
	...
    loadPage(pageName, context);
    ...
}

protected void loadPage(String resource, FitNesseContext context) {
	...
}
```
### 개념적 유사성
: 개념적인 친화도가 높을수록 가까이 배치한다.
- 친화도가 높은 요인
	- 한 함수가 다른 함수를 호출 하는 경우
   	- 변수와 그 변수를 사용하는 함수
   	- 비슷한 동작을 수행하는 함수
    
#### 세로 순서
: 중요한 개념을 가장 먼저 표현하고 아래로 내려갈수록 자세하게 기술한다.
# 가로 형식 맞추기
한 행의 길이는 짧을수록 바람직하다. 120자 정도가 적당하다.
## 가로 공백과 밀집도
: 공백을 추가하면 한 개념이 아니라 다른 개념으로 여겨진다.
- 할당 연산자 사이에 공백을 추가한다. 
```java
int lineSize = line.length();
totalChars += lineSize;
```
- 함수 이름과 이어지는 괄호 사이에는 공백을 넣지 않는다.
괄호 안의 인수는 쉼표와 공백으로 분리해 별개라는 사실을 보여준다.
```java
public static double root1(double a, double b, double c) {
	...
}
```
- 연산자 우선순위 강조
```java
public static double root2(int a, int b, int c) {
	double determinant = determinant(a, b, c);
    return (-b - Math.sqrt(determinant)) / (2*a);
```
## 가로 정렬
: 사용 X
## 들여쓰기
들여쓰기가 없다면 코드를 읽는 것은 거의 불가능하다.
파일의 구조를 한 눈에 보기 위해 들여쓰기는 필수이다.
## 들여쓰기 무시하기
들여쓰기를 무시해서는 안된다.
# 팀 규칙
: 팀에서 한 가지의 규칙을 정하고 모든 팀원은 그 규칙을 따라야 한다. 개인이 선호하는 규칙을 사용해서는 안된다.