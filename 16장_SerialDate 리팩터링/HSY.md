> SerialDate는 날짜를 표현하는 자바 클래스이다. 이 클래스를 리팩터링 해보자

# 첫째, 돌려보자
SerialDateTests라는 클래스는 단위 테스트 케이스 몇개를 포함한다. 하짐나 모든 경우를 점검하지 않는다는 것을 알 수 있다.
SerialDate가 통과해야 하는 테스트 케이스인데 통과하지 못하는 경우가 존재한다.
=> 모든 테스트 케이스를 통과할 수 있게 알고리즘을 올바르게 고친다.

# 둘째, 고쳐보자
1. 라이선스 정보과 저작권은 보존하지만, 변경 이력은 삭제한다.
2. import 문에서 java.text.* java.util.\*로 줄인다.
3. Month(달)은 enum으로 정의한다.
4. 정적 변수와 정적 메서드를 새 클래스로 옮긴다.
5. 추상 메서드를 클래스로 올린다.
