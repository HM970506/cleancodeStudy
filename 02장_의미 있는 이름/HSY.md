> 우리는 코드를 작성할 때 항상 이름을 붙인다.
이름을 알아 보기 쉽게 정하면 매우 편리하다. 해당 장에서는 이름을 잘 짓는 방법에 대해서 설명한다.

# 의도를 분명히 밝혀라
변수나 함수의 이름을 정할 때는 존재 이유, 수행하는 기능, 사용 방법이 드러나게 정해야 한다.
- 잘못된 예시
```
int d;  // 경과된 시간(단위: 날짜)
```
- 올바른 예시
: 코드를 읽는 사람이 어떤 변수인지 알 수 있게 정해야 한다.
```
int daySinceCreation;
```

**지뢰 찾기 게임을 만든다고 할 때, 깃발이 꽂힌 칸을 반환하는 함수를 만든다. 배열(게임판)에서 0번째 값에는 칸의 상태가 적혀있다. 4는 깃발이 꽂혀 있는 상태를 의미한다.**

- 잘못된 예시
: theList에 어떤 정보가 들어있는지, 0번째 값을 4와 왜 비교하는지, 리턴하는 list1은 어떻게 쓰이는지 등의 정보를 알 수 없다.
```
public List<int[]> getThem(){
	List<int[]> list1 = new ArrayList<int[]>();
    
    for(int[] x : theList)
    	if (x[0] == 4)
        	list1.add(x);
    return list1;
}
```
- 올바른 예시
: 똑같은 코드이지만 이름을 다르게 하여 가독성을 높인다.
```
public List<int[]> getFlaggedCells(){
	List<int[]> flaggedCells = new ArrayList<int[]>();
    
    for(int[] cell : gameBoard)
    	if(cell[STATUS_VALUE] == FLAGGED)
        	flaggedCells.add(cell);
    return flaggedCells;
}
```
# 그릇된 정보를 피하라
- 널리 쓰이고 있는 단어를 사용하면 안된다.
: accountList라는 이름보다는 accountGroup과 같이 지어주어야 한다.
(List는 특수 의미로 사용하고 있기 때문이다.)

- 비슷한 이름을 사용하면 안된다.

# 의미 있게 구분하라
연속된 숫자를 붙이거나 불용어(큰 의미가 없는 단어)를 추가해서는 안된다. 읽는 사람이 차이를 알 수 있게 정해야 한다.
- 잘못된 예시(연속된 숫자)
```
public static void copyChars(char a1[], char a2[]){
	for(int i = 0; i < a1.length; i++)
    	a2[i] = a1[i];
}
```
- 올바른 예시(연속된 숫자)
```
public static void copyChars(char source[], char destination[]){
	for(int i = 0; i < source.length; i++)
    	destination[i] = source[i];
}
```
- 잘못된 예시(불용어)
```
// class 이름
CustomerObject
CustomerString
```
- 올바른 예시(불용어)
: 불용어는 모두 제거하고 붙인다.
```
// class 이름
Customer
```
# 발음하기 쉬운 이름을 사용하라
발음하기 어렵게 변수 이름을 정하면 코드 리뷰처럼 토론을 할 때 사용하기 어렵다.
# 검색하기 쉬운 이름을 사용하라
이름을 너무 짧게('e',7) 설정하면 코드에서 검색을 할 때 찾아내기 어려워진다. 이름을 의미 있게 지어서 코드에서 바로 검색될 수 있게 해야 한다.

간단한 메소드 안의 로컬 변수는 한 글자로 설정해도 괜찮다.
# 자신의 기억력을 자랑하지 마라
코드를 읽는 사람이 자신이 짠 코드 속의 변수 이름을 자신이 알 수 있게 바꾸는 일이 생겨서는 안된다.
# 클래스 이름
- 명사나 명사구가 좋다.
# 메서드 이름
- 동사나 동사구가 좋다.
- 접근자, 변경자, 조건자 앞에는 get, set, is를 붙여준다.
# 기발한 이름은 피하라
기발한 이름보다는 명료한 이름으로 정해야 한다. 의도를 정확하게 표현해야 한다.
# 한 개념에 한 단어를 사용하라
fetch, retrieve, get과 같이 비슷한 뜻의 단어를 함께 사용하면 혼동이 생긴다. 일관성 있게 단어를 사용해야 한다.

한 개념에 한 단어를 사용하게 위해 다른 기능을 하는데 같은 단어를 사용하는 것은 바람직하지 않다.
# 해법 영역에서 가져온 이름을 사용하라
개발자라면 당연히 알고 있을 용어를 사용해도 괜찮다.
# 문제 영역에서 가져온 이름을 사용하라
해법 영역에서 사용할 적절한 용어가 없다면 문제 영역에서 용어를 사용해도 된다.
# 의미 있는 맥락을 추가하라
각각의 변수가 어떠한 큰 맥락에 포함되는지를 알려줘야 한다.
- 잘못된 예시
```
firstName, lastName, street, houseNumber, city, state, zipcode
```
- 올바른 예시
: addr을 접두어로 추가하여 주소를 나타내는 것임이 분명해진다.
```
addrfirstName, addrlastName, addrstreet, 
addrhouseNumber, addrcity, addrstate, addrzipcode
```