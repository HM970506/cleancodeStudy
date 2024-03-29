## 창발적 설계로 깔끔한 코드를 구현하자
### 단순한 설계 규칙 4가지
* 모든 테스트 실행
* 중복 X
* 프로그래머 의도 표현
* 클래스와 메서드 수 최소로 줄임

***
### 단순한 설계 규칙1: 모든 테스트를 실행하라
   테스트 케이스 많을수록 쉽게 코드 작성 -> 더 나은 설계
   결합도 낮추기 (DIP 원칙, 의존성 주입, 인터페이스, 추상화)
> 테스트 케이스를 만들고 계속 돌려라 

***
### 단순한 설계 규칙2~4: 리팩터링
> 코드를 정리하면서 시스템이 깨질까 걱정할 필요가 없다. 테스트 케이스가 있으니까! 
  
   리팩터링 단계에서는 소프트웨어 설계 품질을 높이는 기법이라면 뭐든 ㄱㅊ   
   응집도 높이고, 결합도 낮추고, 관심사 분리하고, 시스템 관심사 모듈로 나누고   
   함수와 클래스 크기 줄이고, 더 나은 이름 선택    
   중복 제거, 프로그래머 의도 표현, 클래스와 메서드 수 최소로 줄임   

***
## 중복을 없애라
> 우수한 설계에서 중복은 커다란 적 (추가 작업, 추가 위험, 불필요한 복잡도)   
> 비슷한 코드는 더 비슷하게 고쳐주자.   
> 구현 중복도 중복의 한 형태   

***
## 표현하라
> 소프트웨어 프로젝트 비용 중 대다수는 장기적인 유지보수   
> 코드는 개발자 의도 분명히 => 다른 사람 코드 이해 높임 => 결함, 유지보수 비용 감소   
* 좋은 이름 선택
* 함수와 클래스 크기 가능한 줄이기
* 표준 명칭 사용 
* 단위 테스트 케이스 꼼꼼히 작성
* 노력!

***
## 클래스와 메서드 수 최소로 줄여라
> 함수와 클래스 크기 작게 유지하면서 동시에 시스템 크기도 작게 유지   
> BUT, 간단한 설계 규칙 네 개 중 우선순위 가장 낮음   
> 테스트 케이스 만들고 중복 제거, 의도 표현 >>> 클래스와 함수 수 줄이기   

***
## 결론
> 경험을 대신할 단순한 개발 기법은 없다. 
