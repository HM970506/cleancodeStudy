> JUnit은 자바 프레임워크 중에서 가자 유명하다. 이 장에서는 JUnit 프레임워크에서 가져온 코드를 평가한다.

# JUnit 프레임워크
JUnit은 단위 테스트 도구로 외부 테스트 케이스를 작성해 번거롭게 디버깅하지 않아도 된다. 프로그램 테스트시에 걸리은 시간도 관리해준다.

- 문자열 비교 오류 파악(ComparisionCompactor)
: 두 문자열을 받아서 차이를 반환한다.

1. 멤버 변수 앞의 중복되는 접두사를 없앤다.
```java
    private int fContextLength;
    private String fExpected;
    private String fActual;
    private int fPrefix;
    private int fSuffix;
```
```java
    private int contextLength;
    private String expected;
    private String actual;
    private int prefix;
    private int suffix;
```

2. 의도를 명확하게 표현하기 위해 조건문을 캡슐화한다.
```java
public String compact(String msg) {
	if(s1 == null || s2 == null || s1.equals(s2))
    	return Assert.format(msg, s1, s2);
    ...
}
```
```java
public String compact(String msg) {
	if(shouldNotCompact())
    	return Assert.format(message, expected, actual);
    ...
}

private boolean shouldNotCompact() {
	return expected == null || actual == null || areStringsEqual();
}
```

3. 부정문은 긍정문보다 이해하기 어렵기 때문에 조건문을 긍정으로 바꾼다.

4. 분석 함수와 일련의 조합 함수로 나눈다. 분석 함수가 먼저 나오고 조합 함수가 그 뒤를 이어서 나오게 한다.
