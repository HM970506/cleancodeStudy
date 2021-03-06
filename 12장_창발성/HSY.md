# 창발적 설계로 깔끔한 코드를 구현하자
아래의 네 가지 규칙을 따르면 소프트웨어 설계 품질을 크게 높여줄수 있다.

1. 모든 테스트를 실행한다.
2. 중복을 없앤다.
3. 프로그래머 의도를 표현한다.
4. 클래스와 메서드 수를 최소로 줄인다.

# 단순한 설계 원칙 1: 모든 테스트를 실행하라
가장 먼저, 설계는 의도한 대로 돌아가는 시스템을 만들어야 한다. 테스트 케이스를 항상 통과하는 시스템은 '테스트가 가능한 시스템'이다. 검증이 불가능한 시스템은 절대로 출시해서는 안된다.

테스트 케이스가 많아질수록 테스트가 쉬운 코드가 만들어진다. 결합도가 높으면 테스트 케이스 작성이 어려워진다. 따라서 결합도를 낮추기 위해 노력하면서 설계 품질이 높아진다.

# 단순한 설계 원칙 2: 리팩터링
테스트 케이스를 모두 작성한 후에 코드와 클래스를 정리한다.

점진적으로 코드를 리팩터링 한다. 다양한 기법을 이용하여 리팩터링한다. 코드를 정리하면서 시스템이 깨질 걱정은 하지 않아도 된다. 테스트 케이스가 있기 때문이다.

# 중복을 없애라
우수한 설계에서 중복은 커다란 적이다. 단 몇줄이라도 중복을 제거하려는 의지가 필요하다.

# 표현하라
자신이 짠 코드는 쉽게 이해할 수 있지만, 다른 사람이 내 코드를 이해할 가능성은 낮다.

시스템이 복잡해지면서 유지보수 개발자는 코드를 오해할 가능성이 생긴다. 따라서 자신의 의도를 코드에 분명히 표현해야 한다. 

1. 좋은 이름을 선택하라
2. 함수와 클래스 크기를 가능한 줄인다.
3. 표준 명칭을 사용한다.
4. 단위 테스트 케이스를 꼼꼼히 작성한다.

# 클래스와 메서드 수를 최소로 줄여라
무조건 클래스와 메서드 수를 줄이면 작은 클래스와 메서드를 수없이 만드는 사례도 생긴다. 
클래스와 메서드 수를 줄이는 것도 좋지만 테스트 케이스를 만들고 중복을 제거하고 의도를 표현하는 작업이 더 중요하다.