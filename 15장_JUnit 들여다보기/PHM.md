# JUnit 들여다보기

## JUnit이란?
* 단위 테스트를 수행하기 위해 사용하는 프레임워크
* 구현한 함수가 제대로 작동하는지, 결과값과 예상값이 일치하는지 확인

## 코드 커버리지 분석
### 코드 커버리지란?
* 소프트웨어의 테스트케이스가 얼마나 충족되었는지를 나타내는 지표
* 테스트를 진행하였을 때 코드 자체가 얼마나 실행되었는지에 대한 수치

### 코드 커버리지 측정 방법
* 블랙박스 테스트 (사용자 관점)
* 화이트박스 테스트 (개발자 관점)

## 보이 스카우트 규칙
> 언제나 처음 왔을 때보다 깨끗하게 해놓고 캠프장을 떠날 것

### 변수 이름에 범위를 명시하지 않는다
* 현재의 IDE에서 범위, 변수 타입 등은 중복되는 정보!
### 조건문은 메서드로 캡슐화하여 의도를 명확히 표현하라
```java
  ❌
  if ( option_1==null || option_2==null || ... )  
  
  ⭕
  if ( AlloptionsFalse() == null )
  private boolean isAnimal(){ return option_1==null || option_2==null... }
 
```

### 부정문 if는 긍정문으로 반전하라
```java
  ❌
  if ( AlloptionsFalse() == null )
  private boolean isAnimal(){ return option_1==null || option_2==null... }
  
  ⭕
  if ( AlloptionsTrue() )
  private boolean isAnimal(){ return option_1 != null && option_2 != null... }
 
```

### 같은 목적을 가진 일련의 작업은 다른 함수로 분리하라
```java
  ❌
  private void MakeSandwich(){
    Baking();
    CuttingEdge();
    StackHam();
    StackTomato();
    StackCheese();
    ...
  }
  
  ⭕
  private void MakeSandwich(){
    ReadyBread();
    StackMaterials();
    ...
  }
  
  private void ReadyBread(){
    Baking();
    CuttingEdge();
   }
   
  private void StackMaterials(){
    StackHam();
    StackTomato();
    StackCheese();
    ...
  }
 
```

### return과 같은 함수 사용방식을 일관되게 지정하라
```java
  ❌
  private void MyFunction(){
    MyFunction_1();
    int two = MyFunction_2();
  }
  
  ⭕
  private void MyFunction(){
    int one = MyFunction_1();
    int two = MyFunction_2();
  }
 
```

### 시간적 결합을 외부에 노출하라
* 시간적 결합이 있는 요소를 인수로 넘기는 방법
  > 😦 해당 인자가 필요한 이유를 설명하지 못하므로 자의적, 부적절!
* 시간적 결합에 따라 적절한 변수명을 붙이고 실행순서를 강제하는 방법

#### 시간적 결합이란?
> B는 반드시 A다음에 발생해야 한다!

실행순서에 따라 다른 결과를 발생시킬 위험이 있는 일련의 함수들을 시간적으로 결합되었다고 설명한다. <br/>
👉 개발자는 순서에 의존이 없는, **동시성을 보장**하는 프로그램을 만들어야 한다!

### 동의어는 하나로 통일하라
ex) stringlength, allindex ...     👉     stringLenght, allLength ...

### 전체 함수를 위상적으로 정렬하라
* 각 함수는 사용된 직후 정의되어야 한다
* 분석 함수가 먼저 나오고 조합 함수가 이후에 나온다

> 리팩터링은 코드가 어느 수준에 이를 떄까지 수많은 시행착오를 반복하는 작업!
