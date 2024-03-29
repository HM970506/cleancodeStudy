# 클라이언트와 서버 구조
## 단일스레드
### 이벤트 폴링 루프
이벤트에서 충돌 회피/동기화 처리를 위해 다른 프로그램의 상태를 주기적으로 검사한 후 <br/>
일정한 조건을 만족할 때 자료처리를 진행하는 루프

### 단일스레드 환경에서의 속도 개선

* I/O : 소켓 사용, 데이터베이스 연결, 가상메모리 스와핑 대기 등 <br/>
   👉 동시성 이용 - 한쪽이 I/O를 기다리는 동안 다른 쪽이 CPU 사용
* 프로세서: 수치 계산, 정규표현식 처리, 가비지 컬렉션 등 <br/>
   👉 하드웨어를 추가하여 성능 높이기 (프로세스 추가x)
   
<br/>
   
## 다중스레드
>다중 스레드 프로그램을 깨끗하게 유지하려면 잘 통제된 몇 곳으로 스레드 관리를 모아야 한다!

### 스레드 관리 책임 클래스
* 스레드 관리 전략이 변해도, 전체 코드에 미치는 영향이 작음
* 다른 책임에 간섭하지 않음

### 다중 스레드 환경에서 안전하지 않은 클래스
* SimpleDataFormat
* DB연결
* java.util
* 서블릿


<br/>

## 경로 수
루프나 분기가 없는 **명령 N개를 스레드 T개가 차례로 실행**할 때 가능한 경로 수

> (NT)! / (N!)^T

<br/>

## 바이트코드와 원자적 연산
### 프레임
호출 스택(call stack)을 정의할 때 사용하는 표준 기법 <br/>
메서드 호출에 필요한 반환주소, 매개변수, 메서드 지역변수를 포함한다. <br/>

### 지역 변수
메서드 범위 내 정의되는 모든 변수 <br/>
> #### 👇 this란?
> 현재 스레드에서 **가장 최근**에 메시지를 받아 **메서드를 호출**한 객체!

### 피연산자 스택
매개변수를 저장하는 LIFO 자료구조

### 원자적 연산이 아닌 것을 다룰 때 주의해야 하는 곳
> ++ 연산은 원자적 연산이 아니다!

* 공유객체/값이 있는 곳
* 동시 읽기/수정 문제를 일으킬 소지가 있는 코드
* 동시성 문제를 방지하는 방법

<br/>

## Excutor class
> 직접 생성한 스레드풀을 생성할 때 사용하면 좋은 클래스

### 기능
* 스레드 풀 관리
* 스레드 풀 크기 자동 조정
* 스레드 재사용
* Future 지원 - 독립적인 연산 여럿을 실행한 후 모두 완료를 대기할 때 유용!

<br/>

## non-blocking
> Non-blocking하게 동기화 문제를 해결하기 위한 방법으로 Atomic 연산이 있다!

### blocking을 사용하는 이유
다중 스레드 환경에서 값을 안전하게 갱신하기 위해 동기화가 필요! <br/>
동기화를 위해 스레드 동시접속을 차단해야 함!

### 👀 가시성 문제
멀티스레드 환경에서 각 CPU는 **메인 메모리가 아닌 캐시**에서 메모리 값을 참조한다! <br/>
이때 메인 메모리에 저장된 값과 CPU 캐시에 저장된 값이 다른 경우가 있는데 이를 가시성 문제라고 한다!

### CAS(compare and swap) 연산
현재 스레드 저장값과 메인메모리 저장값(최종값)을 비교하여
* 일치하는 경우 새로운 값으로 교체하고
* 일치하지 않는다면 실패하고 재시도한다.

cas연산은 이러한 방법으로 가시성 문제를 해결하는 원시 연산방법!

>#### 😗 CAS와 동기화 버전이 뭐가 다른가요?
>CAS는 낙관적 잠금(마지막에만 정상완료인지 검사)과 유사하고
>동기화 버전은 비관적 잠금(진입 전 스레드 블로킹) 과 유사하다!


<br/>

## 메서드 사이 의존성
### 스레드 두 개가 하나의 인스턴스를 공유할 때
> 각 스레드가 같은 리스트를 공유하며 한번에 한 인덱스씩 처리한다면? <br/>
> 👉**한 스레드에서 목록 끝을 넘어설 위험성이 있다!**

### 해결 방안
* 실패 용인
* 클라이언트-기반 잠금 매커니즘
* **서버-기반 잠금 매커니즘**

>#### 서버-기반 잠금 매커니즘이 가장 적절한 이유
>* 코드 중복이 줄어든다
>* 클라이언트의 자유성이 높아진다
>* 성능이 좋아진다(오버헤드 감소)
>* 오류 발생 가능성이 줄어든다
>* 클라이언트 수만큼 정책이 존재하는 클라이언트-기반 잠금과 달리 스레드 정책이 하나다!
>* 공유 변수 범위가 서버로 한정되어 문제 발생시 찾아볼 범위가 작다

### 서버 코드에 손대지 못한다면..
* ADAPTER pattern을 사용하여 API를 변경한다
* 인터페이스가 확장된 집합 클래스를 사용한다

<br/>

## 데드락
### 데드락의 조건
#### 상호 배제
여러 스레드가 동시사용이 불가능하고 개수가 제한적인 자원을 공유한다
>DB연결, 쓰기용 파일 열기, 레코드 락, 세마포어...

#### 잠금 & 대기
스레드가 작업을 마칠 때까지 점유한 자원을 내놓지 않음

#### 선점 불가
한 스레드가 다른 스레드로부터 자원을 빼앗지 못함

#### 순환 대기 (죽음의 포옹)
![image](https://user-images.githubusercontent.com/62527898/186098948-afef2379-b7a9-4b12-a1da-8403be52b5f6.png)


### 데드락 조건 깨기
#### 상호 배제
* 동시에 사용해도 괜찮은 자원을 사용한다 (ex.AtomicInteger)
* 스레드 수 이상으로 자원 수를 늘린다
* 자원 점유 전 필요한 자원이 모두 있는지 확인한다

### 잠금 & 대기
* 필요 자원 중 하나라도 점유하지 못했다면 지금까지 점유한 자원을 모두 내놓는다
  * 문제점1: 👅 기아 상태 - 한 스레드가 계속해서 필요 자원을 점유하지 못한다 (cpu효율 저하)
  * 문제점2: 💫 라이브락 - 여러 스레드가 한꺼번에 잠금단계로 진입하여 자원점유와 내놓기를 반복한다 (cpu 과다 사용)

#### 선점 불가
* 다른 스레드로부터 자원을 빼앗는다
  * 필요 자원이 잠겼다면 해당 자원을 소유한 스레드에게 선점을 풀어줄 것을 요청한다
  * 소유한 스레드가 다른 자원 대기중이었다면 자신이 소유한 자원을 모두 내놓는다

#### 순환 대기 (죽음의 포옹)
* 일정 순서로 스레드에 자원을 할당한다
  * 문제점1: 자원할당 순서와 자원사용순서가 다르면 자원을 필요 이상으로 점유하고 있게 된다
  * 문제점2: 첫 자원 사용 이후 두번째 자원 할당이 가능한 경우는 순차 할당이 어렵다


<br/>

## 스레드 에러 찾아내기
### 몬테카를로 테스트
조율이 가능하게 유연한 테스트를 만들고 임의로 테스트값을 조율하며 반복해 돌리는 테스트 방법
* 테스트 실패 조건은 신중하게 기록한다
* 시스템을 배치할 플랫폼 전부에서 테스트를 돌린다
* 부하가 변하는 장비에서 테스트를 돌린다

## ConTest - 스레드 코드 테스트 도구
보조 코드를 추가하여 테스트를 실행시 확실한 테스트 실패를 보장해주는 도구








 
