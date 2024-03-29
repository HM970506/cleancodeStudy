14장 점진적인 개선
==============
_이 장은 점진적인 개선을 보여주는 사례 연구다.  
우선, 출발은 좋았으나 확장성이 부족했던 모듈을 소개한다.  
그런 다음, 모듈을 개선하고 정리하는 단계를 살펴본다._  
<br>

### 깨끗한 코드로 개선하기
깨끗한 코드를 짜려면 먼저 지저분한 코드를 짠 뒤에 정리해야 한다.  
<br>
- #### 1차 초안의 문제점
    - 수많은 인스턴스 변수 개수
    - 'TILT'와 같은 희한한 문자열
    - HashSets, TreeSets, try-catch-catch 블록 등 지저분한 코드에 기여하는 다수의 요인들   
      <br>

- #### 2차 초안의 문제점
    - String과 Integer라는 인수 유형 두 개 추가   
      <br>

- #### 리팩터링
    - 새 인수 유형을 추가하려면 주요 지점 세 곳에다 코드를 추가해야 한다.
        1. 인수 유형에 해당하는 HashMap을 선택하기 위해 스키마 요소의 구문을 분석한다.
        2. 명령행 인수에서 인수 유형을 분석해 진짜 유형으로 변환한다.
        3. getXXX 메서드를 구현해 호출자에게 진짜 유형을 반환한다.   
           <br>
    - 인수 유형은 다양하지만 모두가 유사한 메서드를 제공하므로 클래스 하나(ArguementMarshaler)를 만들자.
    - __테스트 주도 개발(TDD)를 통해 점진적으로 개선한다.__ 테스트 케이스가 하나라도 실패하면 다음 변경으로 넘어가기 전에 오류를 수정한다.
    - 유지 및 보수를 위해 각 인수 유형을 처리하는 코드를 모두 ArgumentMarshaler 클래스에 넣고 나서 ArgumentMarshaler 파생 클래스를 만들어 코드를 분리해보자.
    - 별도의 메서드를 선언할 이유가 없다면 인라인 코드로 만들자.  
      <br>
  > 구조는 조금 개선되었지만 결과는 다소 실망스럽다.  
  > 첫머리에 나오는 변수는 그대로 남아있으며, setArgument에는 유형을 일일이 확인하는 보기 싫은 코드도 그대로 남아있다.  
  > 오류 처리 코드와 모든 set 함수는 보기에 흉하다.

<br>

- #### 추가 리팩터링
    - setArgument 함수에서 유형을 일일이 확인하는 코드를 없애고 이를 ArgumentMarshaler 파생 클래스로 내린다.
    - 예외 처리 코드를 제거한다.
    - 인수 유형을 일일이 확인하던 코드를 제거한다.
    - ArgumentMarshaler를 인터페이스로 변환한다.
    - 잡다한 오류 지원 코드를 독자적인 모듈로 만든다.  
      <br>
  > 새로운 인수 유형을 추가하기 쉽다.  
  > __변경할 코드는 아주 적으며 나머지 시스템에 영향을 미치지 않는다.__

<br>

### 결론
나쁜 코드를 깨끗한 코드로 개선할 수 있지만 엄청난 비용이 든다.  
반면 처음부터 코드를 깨끗하게 유지하기란 상대적으로 쉽다.  
__그러므로 코드는 언제나 최대한 깔끔하고 단순하게 정리하자.__ 
