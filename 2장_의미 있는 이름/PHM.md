2장 의미 있는 이름
=====================
<br/><br/>
* 의도를 분명하게 밝혀라
<br/>

* 상수를 가능한 함수로 감싸 감추어라
  * state를 직접 수정하기보다는, isTrue 등의 함수를 이용하기
<br/>

* 읽는 사람이 차이를 알도록 이름을 지어라
<br/>

* 발음하기 쉬운 이름을 사용하라
<br/>

* 검색하기 쉬운 이름을 사용하라
  * 이름의 길이는 범위 크기에 비례해야 함
  * 상수는 대문자와 언더바 조합으로 만들어 사용
<br/>

* 클래스 이름에는 명사를, 메서드 이름에는 동사를 사용하라
<br/>

* 일관성 있는 어휘를 사용하라
  * manager, controller, driver 등 뜻이 같은 명사를 반복적으로 사용하지 말 것
<br/>

* 이름에 불필요한 맥락을 추가하지 말아라
  * 의미가 분명하고 긴 이름을 만들도록 할 것
<br/>

* 함수를 가능한 작게 만들어라
  * 한 함수당 20줄이 넘어가지 않도록 쪼개기
  * if문이나 while문에 들어가는 블록은 한 줄이어야 함!
    * **중첩구조가 생길만큼 함수가 커져서는 안 됨!**
    * **함수 들여쓰기가 2단 내에서 해결되도록!**
<br/>

* 내려가기 규칙: 이야기처럼 위에서 아래로 읽어내릴 수 있도록 함수를 배치하기
  * >a가 b면 c를 한다 -> a를 찾으려면 d를 한다 -> d를 하려면 e를 한다..
