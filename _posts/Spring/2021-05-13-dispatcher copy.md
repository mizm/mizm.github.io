## Spring Framework

### 기본

- CGI는 무엇이고 Servlet API는 무엇이며, 어떤 차이가 있나요?
- Spring이란 무엇인가요?
    - Spring은 Java EJB에서 EJB에 의존된 개발을 하다보니, EJB에 의존성이 너무 높아지는 문제점을 해결하기 위해 만들어진 프레임워크로 객체지향적으로 개발할 수 있게 도와주는 프레임워크이다.
    - 스프링은 문맥에 따라 DI container로도 불린다. 객체지향의 다형성과 OCP, DIP를 지키면서 개발 할 수 있게 외부에서 의존관계를 주입하는 방법을 도와주고 빈들을 관리하는 컨테이너이다.
    - 다형성
        - 역할과 구현으로 구분해서 클라이언트는 역할만 알고 있으면 어떤 구현대상이 오더라도 상관없고, 구현 대상의 내부구조가 변경되어도 상관 없다 ( 사람 - 자동차 (역할) - k5, 아반뗴)
        - 자바에서는 인터페이스가 역할이고 구현은 인터페이스를 받아서 구현한 클래스이다.
        - 결국 클라이언트의 변경 없이 구현체의 내부구조나 구현체 자체를 변경시킬 수 있다.
    - ocp
        - 개방폐쇄원칙
        - 확장에는 열려있으나 변경에는 닫혀있어야한다.
        - interface를 사용하는 클라이언트는 인터페이스의 구현이 변해도 클라이언트의 변경은 없어야 한다.
        - 하지만 기본적인 자바 코드에서는 인터페이스에 구현체를 변경하려면 클라이언트가 직접 선택해야 한다.
        - 해결 하기 위해 객체를 생성, 연관관계를 조립하는 것이 필요하다.
    - DIP
        - 의존 관계 역전 원칙
        - 구체적인 것 보다 추상화에 의존해야한다.
        - 클라이언트가 구현클래스를 직접 선택하면 구현된 클래스에도 의존하기 때문에 DIP 위반이다.

- IoC, DI가 왜 좋은 걸까요?
    - 객체 지향의 다형성과 개방폐쇄원칙, 의존관계역전원칙을 지키며 객체지향적으로 개발이 가능하며, 객체지향적으로 개발을 했을 시 유연한 변경이 가능하며 확장이 쉽다.
- IoC Container란 무엇인가요?
    - 객체의 생성 및 의존관계를 관리해주는 빈으로써 객체가 의존하는 객체를 없애고 외부에서 주입해줄 수 있도록 해주는 컨테이너

- Spring, Spring Boot의 차이점에 대해 각각 설명해 주세요.
    - 스플
- Spring Boot가 해결하려고 했던 문제는 무엇이고 어떻게 해결하였나요?
- Spring Framework의 빈 생명 주기에 대해서 말해주세요.
    - 스프링 컨테이너 생성
    - 빈 생성
    - 빈 의존관계 주입
    - 초기화 콜백 @PostContruct
    - 사용
    - 소멸전 콜백 @PreDestroy
    - 스프링 종료
- 순환 참조는 무엇이고 어떻게 발생하나요?ㅋㅏ
    - A 객체가 B 객체를 의존해서 호출하고 B 객체에서도 A 객체를 호출할때 내부적으로 순환하면서 스택이 쌓이다가 오류가 난다.
    - 서로 다른 객체가 서로 의존관계에 있을때 발생합니다.
    - 의존관계를 생성자로 주입하게 되면 
- 생성자 주입은 빈 생성 때 사용되는 리플랙션 외에 추가적인 리플랙션을 진행하나요?
- Bean이란 무엇인가요?
    - 스프링 컨테이너를 통해 생성되고 관리되는 자바 객체 
- Bean Scope와 종류에 대해 아는 만큼 설명해주세요.
    - singleton scope
        - 기본적으로 빈이 등록된 뒤 싱글톤으로 관리되는 객체
        - 스프링 컨테이너의 시작과 함께 생성 종료될떄까지 유지 스코프
    - prototype scope
        - 빈의 생성과 의존관계 주입까지만 하고 관리하지 않음
    - request scope
        - 웹 요청이 들어오고 나갈떄까지 유지되는 스코프
    - session scope
    - application scope
- Bean Lite Mode는 무엇인가요?
- @Bean과 @Component은 각각 언제 사용되고 어떤 차이점을 가지나요?
@Component는 Class Level에서, @Bean은 Method Level에서 적용된다. @Component는 Class와 Bean이 One to One 관계를 갖는 반면 메소드는 그렇지 않다.
@Bean 은 Class에 @Component를 붙일 수 없는 외부라이브러리에 사용한다.

- Interceptor와 Filter의 차이점을 말해주세요.
필터와 인터셉터는 실행되는 시점에서 차이가 있습니다. 필터는 웹 애플리케이션에 등록을 하고, 인터셉터는 스프링의 context에 등록을 합니다. 따라서 컨트롤러에 들어가기 전 작업을 처리하기 위해 사용하는 공통점이 있지만, 호출되는 시점에서 차이가 존재합니다.
필터는 디스패처서블릿 앞에서 처리하고 interceptor는 디스패처 서블릿에서 핸들러를 호출하기전에 동작한다.
- 스프링에서 Bean으로 Filter를 구현할 수 있을까요? 혹시나 가능하다면 어떻게 할 수 있을까요?
- Message Converter 와 MV Container는 각각 어떻게 개입하고 어떤 방식으로 동작하나요?
- VO, DTO, DAO에 대해서 각각 설명해 주세요.
- Spring AOP는 어떻게 동작할까요? (프록시는 언제 생성되고 요청은 어떻게 잡아내나요?)
    - 프록시는 스프링컨테이너가 빈을 생성 한 뒤 빈후처리기를 통해 프록시를 생성하고 기존에 생성 된 빈을 대체합니다. 그 후 요청이 올때 기존의 프록시에서 기존의 빈을 reflection이나 cglib 의 바이트 코드 조작을 통해 요청합니다.
- MVC1, 2 개념에 대해서 설명해 주세요.
- Dispatcher-Servlet이란 무엇인가요?
- Spring MVC에서 HTTP 요청이 들어왔을 때의 흐름을 설명해 주세요.
    - DispatcherServlet에서 url을 기준으로 핸들러 매핑 클래스의 매핑정보를 조회하며 핸들러를 찾고 찾은 핸들러를 사용할 수 있는 핸들러 어댑터를 찾기 위해 핸들러 어댑터 매핑 클래스에서 매핑 정보를 조회하여 핸들러 어댑터를 찾습니다. 그 후에 핸들러 어댑터로 요청이 전달되고 핸들러 어댑터는 핸들러(컨트롤러)에게 요청을 전달합니다. 컨트롤러는 요청에 대한 결과값을 반환하고 핸들러 어댑터는 핸들러의 요청 결과인 MODEL AND VIEW를 디스패처서블릿에 반환합니다. 디스패처 서블릿은 위에서 받아온 논리 뷰이름을 뷰리졸버에게 전달합니다. 뷰 리졸버는 논리뷰이름을 통해 물리적인 뷰를 찾고 반환합니다. 그후 뷰객체를 통해 렌더링 됩니다.
- Spring AOP는 CTW, LTW, RTW 중에 무엇이고 Aspactj 와 비교하여 언제 사용하는 것이 좋고 언제 사용하지 않는 것이 좋을까요?
    - compile time weaving
    - load time weaving
    - runtime weaving
- Dynamic Proxy의 CTW, BTW, LTW, RTW은 각각 무엇인가요?
- @Transactional를 스프링 Bean 메서드 A에 적용하였고, 해당 Bean의 메서드 B가 호출되었을 때 메서드 내부에서 메서드 A를 호출하면 어떤 요청 흐름이 발생하게 되나요?
- A라는 Service 객체의 메서드가 존재하고 내부에서 로컬 트랜잭션이 3개가 존재한다고 할 때, @Transactional을 A 메서드에 적용하였을 때 어떠한 일이 벌어지고, 어떤 요청 흐름이 발생하게 되나요?
- Reflection API는 Runtime에서 코드를 생성해내는데 많이 사용되게 됩니다. 이는 스프링에서도 적용되는데요. 스프링 컨테이너는 이런 Reflection으로 생성된 Bean을 알고 있네요? 어떻게 알 수 있을까요?
자바에서는 JVM이 실행되면 사용자가 작성한 자바 코드가 컴파일러를 거쳐 바이트 코드로 변환되어 static 영역에 저장된다. Reflection API는 이 정보를 활용한다. 그래서 클래스 이름만 알고 있다면 언제든 static 영역을 뒤져서 정보를 가져올 수 있는 것이다.

Spring Framework에서도 Reflection API를 사용하는데 대표적으로 Spring Container의 BeanFactory가 있다. Bean은 애플리케이션이 실행한 후 런타임에 객체가 호출될 때 동적으로 객체의 인스턴스를 생성하는데 이때 Spring Container의 BeanFactory에서 리플렉션을 사용한다.

- Spring AutoConfiguration
    - Spring Boot가 spring.factories 파일에 사전에 정의한 AutoConfiguration 내용에 의해 bean 생성이 진행됩니다.
    - 우리가 설정한 bean이 먼저 생성되고 해당 AutoConfiguration은 필터링 되어 중복생성되는 상황을 막습니다. 우리가 해당 bean을 설정하지 않았다면 AutoConfiguration에서는 해당 bean을 자동 생성하게 됩니다.
    - 특정 bean들의 존재유무에 대해서 다루는 필터입니다. @ConditionalOnBean, @ConditionalOnMissingBean, @ConditionalOnSingleCandidate
    - 특정 class들의 존재유무에 대해서 다루는 필터입니다. @ConditionalOnClass, @ConditionalOnMissingClass

spring boot aop
 
jdk dynamic proxy
cglib

기존의 스프링에서는 interface를 구현한 빈을 프록시 객체로 생성할때는 jdk dynamic proxy를 통해 프록시를 생성했다.
하지만, 스프링부트에서는 cglib를 선택 특정 옵션을 주지 않으면 cglib로 모든 프록시를 생성한다.



자바 gc 동작방법

자바 jvm xms xmx
    - 자바 힙의 사이즈를 지정하는 jvm 옵션이다.
    - 힙사이즈의 최소와 최대를 다르게 주었을때 최소에 힙사이즈가 도달하면 gc + 힙사이즈 증가하는 동안 stw 가 발생한다.
    - 그래서 동일하게 주는게 좋다
자바 추상클래스 인터페이스
- 추상클래스
    - 추상클래스는 중복되는 구현코드가 많고 중복되는 필드가 많은 상황에서 특정 몇몇 구현코드가 달라질 경우에 사용한다.
    - 또한 클래스 상속이기 때문에 private 제어자를 사용할 수 있다
- 인터페이스
    - 인터페이스는 구현은 상관없고 어떤 행동을 해야하는지에 대한 설명서이다.
    - 서로 관련성이 없는 클래스들이 비슷한 행동을 사용하는 경우
    - 자바 1.8부터는 default 메서드를 통해 구현코드가 가능하다.

자바 oom 해결방법
자바 풀gc
    - Old generation이 꽉 차면 
    - System.gc() 호출
디비 조인
디비 인덱스
    - 인덱스는 where 조건을 기준으로 탄다
    - 인덱스 생성 순서가 중요한데 이때 가장 중복이 낮은 순서대로 인덱스를 만드는 것이 좋다
    - a, b 필드의 인덱스가 걸려있고 b를 search할때는 인덱스의 효과를 볼 수 없다 하지만 a는 볼 수 있다
        - 인덱스는 걸린 순서대로 찾기떄문에
    - GROUP BY 절에 명시된 컬럼이 인덱스 컬럼의 순서와 같아야 한다.
        - 아래 모든 케이스는 인덱스가 적용 안된다. (index: a,b,c)
        - group by b
        - group by b, a
        - group by a, c, b
    - 인덱스 컬럼 중 뒤에 있는 컬럼이 GROUP BY 절에 명시되지 않아도 인덱스는 사용할 수 있다.
        - 아래 모든 케이스는 인덱스가 적용된다. (index: a,b,c)
        - group by a
        - group by a, b
        - group by a, b, c
    - 반대로 인덱스 컬럼 중 앞에 있는 컬럼이 GROUP BY 절에 명시되지 않으면 인덱스를 사용할 수 없다
        - ex: (index: a,b,c), group by b, c 는 인덱스 적용안됨
    - 인덱스에 없는 컬럼이 GROUP BY 절에 포함되어 있으면 인덱스가 적용되지 않는다.
        - ex: (index: a,b,c), group by a,b,c,d 는 인덱스 적용안됨
디비 그룹인덱스??
커버링인덱스
    - 실행계획 extra 필드에 Using Index가 표기됨
    - 쿼리의 모든 항목이 인덱스 컬럼으로 이루어진 상태
    - 인덱스가 있더라도 select에 추가적인 컬럼을 찾아오기 위해서는 데이터 블록에 대한 접근이 필요한데 추가적인 컬럼 없이 인덱스만으로 쿼리를 완성하는 것
    - 아래 쿼리는 customer_id가 인덱스 이지만 select 절의 다른 필드들을 찾아오기 위해서 데이터 블록에 접근을 해야한다.
```sql
    select *
    from temp_ad_offset
    where customer_id = 7;
```
    - 아래 쿼리는 인덱스만 가져오기 떄문에 데이터 블록에 접근할 필요가 없다
```sql
    select customer_id
    from temp_ad_offset
    where customer_id = 7;
```
    -  Extra 항목에 Using index가 나오면 커버링 인덱스가 사용 된 것이다.
디비 where 절 서브쿼리
    - 서브쿼리는 임시 테이블 생성해서 데이터를 넣게 되니까 기존 인덱스가 쓸모없다.
디비 실행계획
디비 락

- 격리성 수준에 따른 발생하는 문제점
- dirty read
    - 트랜잰셩에 의해 수정되었지만 커밋되지 않은 내용을 기준으로 읽어온다.
- Non-Repeatable Read
    - 같은 키를 가진 row를 두번 읽을때 그 사이에 값이 변경되거나 삭제되어 결과가 다르게 나온다
- Panthom Read
    - 다건요청에서 두번 읽을때 처음에는 없던 레코드가 생성된다.

- 격리성 수준
- Read Uncommited
    - commit되지않은 다른 트랜잭션의 내용을 읽는 것을 허용한다.
    - dirty read, Non-Repeatable Read, Phantom Read가 발생한다
- Read Commited
    - commit이 되어 확정된 데이터만 읽도록 허용한다.
    - 커밋 되지 않은 데이터에 대해서는 실제 DB 데이터가 아닌 undo 로그에 있는 이전 데이터를 가지고 온다.
    - Non-Repeatable REad, Phantom Read가 발생한다.
- Repeatable Read
    - 트랜잭션내에서 삭제 변경에 대해서 Undo 로그에 남긴다
    - 앞서 발생한 트랜잭션에 대해서는 실제 데이터 대신에 Undo로그에 있는 백업데이터를 읽게 한다.
    - Phantom Read가 발생한다.

팬텀 리드
- MySQL에서는 REPEATABLE READ 와 READ COMMITTED level에 대해서 한 트랜잭션에서 SELECT 쿼리로 데이터를 읽어올 때 테이블에 lock을 걸지 않고, 해당 시점의 데이터 상태를 의미하는 snapshot 를 구축하여 거기서 데이터를 읽어온다.
- Repeatable Read는 한 트랜잭션에서 한 snapshot 만을 사용해 phantom read를 사용하지 않는다.
    - 하지만 update, delete 같은 경우는 출력 될수 있다.
- , READ COMMITTED 에서 각각의 SELECT 쿼리는 그때그때 최신의 snapshot을 구축하여 데이터를 읽어온다. 따라서 한 트랜잭션이지만 SELECT 쿼리의 결과가 다르기도 했다.
https://jupiny.com/2018/11/30/mysql-transaction-isolation-levels/
디비 조인

sql 실행순서
from() where() groupby() having() select() orderby()


redis failover
- master node가 죽을 경우 cluster failover takeover 명령어를 통해 slave를 master로 승격시킨다.
