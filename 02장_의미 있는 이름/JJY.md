## 의도를 분명히 밝혀라

변수(혹은 함수나 클래스)를 나타낼 때, 의도를 드러나는 이름을 사용하면 좋음

```
// 아무 의미도 드러나지 않은 변수명
int d; //경과 시간(단위: 날짜)

// 의도가 드러나는 변수명
int elapsedTimeInDays;
int daySinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

```
// 코드가 하는 일이 짐작하기 어려운 코드
// 코드의 맥락이 코드 자체에 명시적으로 드러나지 않은 코드

public List<int[]> getThem(){
	List<int[]> list1 = new ArrayList<int[]>();
    for (int[] x : theList)
    	if (x[0] == 4)
        	list1.add(x);
    return list1;
    
// 정보 제공이 충분히 드러난 코드 (예시, 지뢰찾기 게임)
// 배열에서 0은 칸 상태, 값 4는 깃발이 꽂힌 상태

public List<int[]> getFlaggedCells(){
	List<int[]> flaggledCells = new ArrayList<int[]>();
    for (int[] cell :  gameboard)
    	if (cell[STATUS_VALUE] == FLAGGED)
       		flaggedCells.add(cell)
    return flaggedCells;
    
// int 배열을 사용하는 대신 칸을 간단한 클래스로 만들어줌
// isFlagged라는 명시적인 함수를 사용해 FLAGGED라는 상수를 감춤

public List<Cell> getFlaggedCells(){
	List<Cell> flaggedCells = new ArrayList<Cell>();
    for (Cell cell : gameboard)
    	if (cell.isFlagged())
       		flaggedCells.add(cell);
    return flaggedCells;
```

## 그릇된 정보를 피하라

코드의 의미를 흐리는 그릇된 단서를 남겨서는 안됨 (예를 들어, 실제 List가 아닌데 accountList라고 명명하는 경우)

서로 흡사한 이름을 사용하지 않도록 주의 (특히 숫자 1과 영소문자 l, 숫자0과 영대문자 O)

일관성이 떨어지는 표기법 = 그릇된 정보

## 의미 있게 구분하라

동일한 범위 안에서는 다른 두 개념에 같은 이름을 사용하지 못함

이름이 달라야 한다면 의미도 달라져야 함

```
public static void copyChars(char a1[], char a2[[){
	for(int i = 0; i < a1.length; i++){
    	a2[i] = a1[i];
    }
}

// 함수 인수 이름으로 source와 destination을 사용한다면 가독성이 좋아짐
```

불용어는 중복 - 변수 이름에 variable, 표 이름에 table

NameString (String 이외의 부동소수와 같은 Name은 존재하지 X > 그러므로 그릇된 정보에 해당)

ProductData 혹은 ProductInfo와 같이 개념을 구분하지 않은 채 이름만 달리한다면 의미가 불분명한 용어가 됨

또한 Customer, Customer Object 클래스는 구분이 어려움

따라서, 읽은 사람이 차이를 알도록 이름 짓는 것이 좋음

## 발음하기 쉬운 이름을 사용하라

```
// 발음하기 어려운 경우
class DtaRcrd102{
	private Date genymdhms;
    private Date modymdhms;
    private final String pszqint = "102";
};

// 발음하기 좋은 경우
class Customer {
	private Date generationTimestamp;
    private Date modificationTimestamp;
    private final String recordId = "102";
```

## 검색하기 쉬운 이름을 사용하라

문자 하나를 사용하는 이름과 상수는 텍스트 코드에서 쉽게 눈에 띄지 않음

메서드나 로컬 변수만 한 문자를 사용 - **이름 길이는 범위 크기에 비례해야 함**

```
// 검색하기 어려운 이름
for (int j = 0; j < 34; j++){
	s += (t[j]*4)/5;
}

// 검색하기 쉬운 이름 - 상수를 찾고자할 때 매우 쉽게 찾을 수 있음, 길이는 길어짐
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for (int j = 0; j < NUMBER_OF_TRACKS; j++){
	int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
    int realTaskWeeks = (realTaskDays / int WORK_DAYS_PER_WEEK);
    sum += realTaskWeeks;
}
```

## 인코딩을 피하라

#### 멤버변수 접두어 사용 X

#### 인터페이스 클래스와 구현 클래스

인터페이스 클래스와 구현 클래스로 나누어져 있다고 했을 때,

인코딩 해야 한다면, 인터페이스 클래스보단 구현클래스 인코딩이 더 나은 선택

## 자신의 기억력을 자랑하지 마라

코드를 읽으면서 변수 이름을 자신이 아는 이름으로 변환하는 것은 바람직 하지 못함

문자 하나만 사용하는 변수 이름은 문제가 있음

\- 단, 루프 변수에서 사용하는 i, j, k는 루프 범위가 아주 작고 다른 이름과 충돌하지 않을 경우에만 괜찮음

## 클래스 이름

클래스 이름과 **객체 이름은 명사나 명사구**가 적합 ( 예 : Account, Customer )

Manager, Processor, Data, Info와 같은 단어는 피하는 것이 좋고, **동사는 사용하지 않음**

## 메서드 이름

동사나 동사구가 적합 ( 예 : postPayment, deletePage 등 )

접근자(Accessor), 변경자(Mutator), 조건자(Predicate)는 javabean 표준에 따라 값 앞에 get, set, is를 붙임

```
// get, set, is 사용
string name = employee.getName();
customer.setName("mike");
if (paycheck.isPost())
```

생성자 중복정의(오버로드)할 때는 정적 팩토리 메소드 사용

메서드는 인수를 설명하는 이름으로 사용함

```
Complex fulcrumPoint = Complex.FromRealNumber(23.0);

// 더 나은 코드
Complex fulcrumPoint = new Complex(23.0);
// 생성자 사용 제한 시 해당 생성자를 private로 선언
```

## 기발한 이름은 피하라

의도를 분명하고 솔직한 이름으로 표현해야함

## 한 개념에 한 단어를 사용하라

추상적인 개념 하나에 단어 하나를 선택해 이를 고수함

메서드 이름은 독자적이고 일관적이어야 함

## 말장난을 하지 마라

한 단어를 두 가지 목적으로 사용하지 마라

여러 클래스에 add라는 메서드가 생겼을 때, 모든 add 메서드의 매개변수와 반환값이 의미적으로 똑같다면 문제X

But, 프로그래머가 같은 맥락이 아닌데도 일관성을 고려해 add라는 단어를 선택할 때,

기존 매개변수 2개를 가지는 add 메서드가 있고, 새로운 add 매서드에 매개변수에 집합 값 하나를 추가하게 된다면 기존 메서드와 맥락이 다르기 때문에 add가 아닌 insert나 append라는 이름이 적당하다고 볼 수 있음

## 해법 영역에서 가져온 이름을 사용하라

전산용어, 알고리즘 이름, 패턴 이름, 수학 용어 등을 사용해도 좋음

기술 개념에는 기술 이름이 가장 적합한 선택

## 문제 영역에서 가져온 이름을 사용하라

적절한 프로그래머 용어가 없다면 문제 영역에서 이름을 가져옴

해법 영역과 문제 영역을 구분할 줄 알아야함 

## 의미 있는 맥락을 추가하라

스스로 의미가 분명한 이름은 있지만 대다수 이름은 그러하지 못함

이를 해결하기 위해 클래스, 함수, 이름 공간에 넣어 맥락을 부여함

모든 방법이 실패하면 마지막 수단으로 접두어를 붙임

예, firstName, lastName라는 변수가 있을 때, 주소를 나타내고 싶다면

addr 접두어를 붙이게 되면 addrfirstName과 같이 맥락이 분명해짐

Address 클래스 생성이 더 좋음

```
// 맥락이 불분명한 변수
private void printGuessStatistics(char candidate, int count){
	String number;
    String verb;
    String pluralModifier;
    if (count == 0) {
    	number = "no";
        verb = "are";
        pluraModifier = "s";
     }
     else if (count == 1) {
     	number = "1";
        verb = "is";
        pluraModifier = "";
     }
     ...
     String guessMessage = String.format(
     	"There %s %s %s%s", verb, number, candidate, pluralModifier);
     print(guessMessage);
 }	   
     
 // 맥락이 분명한 함수
 // 세 변수는 확실하게 GuessStatisticsMessage에 속함
 // 맥락을 개선하면 함수 쪼개기가 쉬워짐
 
 public class GuessStatisticsMessage {
 	private String number;
    private String verb;
    private String pluralModifier;
	
    public String make(char candidate, int count){
    	createPluralDependentMessageParts(count);
        return String.format(
        	"There %s %s %s%s",
             verb, number, candidate, pluralModifier);
}
private void createPluralDependentMessageParts(int count){
	if (count == 0){
    	thereAreNoLetters();
     }else if (count == 1) {
     	thereIsOneLetter();
     } ...
}

private void thereAreNoLetters(int count){
	...
}
private void thereIsOneLetter(int count){
	...
}
```

## 불필요한 맥락을 없애라

의미가 분명한 경우에 한해서 일반적으로 짧은 이름이 긴 이름보다 좋음

이름에 불필요한 맥락을 추가하지 않도록 주의해야함

예, accountAddress와 customerAddress는 Address 클래스 인스턴스로는 좋은 이름이나, 클래스 이름으로는 적합X

     Address 자체로는 클래스 이름으로 적합함
