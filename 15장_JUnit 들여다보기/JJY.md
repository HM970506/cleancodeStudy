# ✔️ JUnit 프레임워크
JUnit은 독립된 단위테스트 (Unit test)를 지원해주는 프레임워크이다.

## ✅ ComparisonCompactor
두 문자열을 받아 차이를 반환하는 모듈이다.

위 모듈을 깨끗한 코드로 바꾼 후 테스트를 돌려본다.

- 멤버 변수 앞에 붙은 접두어 f를 모두 제거한다.
```java
private int fContextLength;
private String fExpected;
private String fActual;
private int fPrefix;
private int fSuffix;

/* 접두어 f 제거 */  
private int contextLength;
private String expected;
private String actual;
private int prefix;
private int suffix;
```
- 의도를 명확하게 하기 위해 조건문을 캡슐화 한다.
```java
public String compact(String message){
	if (expected == null || actual == null || areStringsEqual())
    	return Assert.format(message, expected, actual);
    ...
```
```java
public String compact(String message){
	if(shouldNotCompat())
    	return Assert.format(message, expected, actual);
    ...
}

private boolean shouldNotCompat(){
	return expected == null || actual == null || areStringEqual();
}
      
```
- 지역변수, 멤버변수, 함수 이름을 명확하게 변환한다.
- 부정문은 긍정문보다 이해하기 어려우므로 조건문을 긍정문으로 바꾼다.
- 모듈은 일련의 분석 함수와 일련의 조합 함수로 나뉘므로 분석 함수가 먼저 나오고 조합 함수가 그 뒤를 이어서 나오게 한다.
