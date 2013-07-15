Scratching Spring
2010-07-29

스프링을 처음 보며 떠올랐던 느낌들에 관한 메모.

### 2010.07.29

3.0 와서 별거 별거 다 껴서 구색을 무자게 갖추었다. 기능 요약 동영상
<http://www.springsource.org/node/2717>

2010 년도 이클립스 서베이 리포트 보면, 서버 프레임웍으로 Spring 19.7%, EJB 18.6%, 아무것도 안 쓴다 24%, 기타 30%.
단일 제품으로는 제일 많이 쓰는데 안 쓰는 인간들이 더 많다.
나 처럼 혼자 사이트 만든다면 사실 안 쓰는 것이 정신 건강에 좋은 것 같다.
필요한 부분 있으면 가끔 함수 만들어 주고 먼가 필요할 때 모두 자바 수작업하는데 클리어하고 별로 공수도 안 들어간다.

혼자 만드는데 프래임웍 써 봤자 프레임웍 공부하는 시간과
프레임웍에서 지원하는지 안 하는지 확인하는 시간 생각하면 득과 실이 똔똔 되고
또 프레임웍 쓰면 디펜던트를 줄줄이 붙어서 톰켓 느려지고.

그렇지만 회사라면 프로그래머 10 명만 되도 프레임웍 없으면 서로 자기 방식 쓰려고 하거나
작업 방식 통일 시키려면 누군가는 어쨌든 라이브러리 만들어야 하는데,
이럴 꺼면 기존 프레임웍을 쓰는 것이 답이 아닌가 하는 생각이 든다.
프레임웍의 존재 가치는 커뮤니케이션 하는데 어떤 기반을 제공해 준다는 부분에서 무시 못할 것 같다.
프레임웍을 쓴다면 Spring MVC 3.0 이 나쁘지 않은 것 같다.
뭐 다른 더 엄청 훌륭한 것이 있는 것도 아니고. =,=.
Java EE / JSF 라인은 진짜 황이다.

자바는 웹 사이트 만드는데 너무 안 좋다.
알 것이 너무 많고 편하지도 않다.
자바에선 웹 솔루션에 아 딱이거다 하는게 없다.
그럴듯한 자바 대안이 또 있는 것도 아니고.
결국 개발자만 피곤해진다.

### 2010.07.30

고민하는거 보다 일단 써보고 아니면 돌아오는 것도 괜찮을 것 같아서 스프링 책을 보고 있다.
슬릭에 가내 수공업 코드 들어내고 스프링 써볼예정.
후딱보려고 한글판책 하나 집어 왔는데 Spring in Action, 2.0 판 기준이라 참 오래된(?) 건데
In Action 씨리즈라 그런지 내용은 좋은 거 같다.
2.0 책으로 쭉 개념잡고, 3.0 영문 레퍼런스 + What's New 보면 될 듯.

앞에 스프링에 대한 개념 챕터들 쭉 봤는데 설명과 의도는 알겠고 나름 그럴듯하나
쌩 Java 코드로 기술했을 때 보다 Xml 이 더 번잡하다.
근데 근래 와서는 Xml 대신 어노테이션 기능이 많이 추가되서.

DI 스타일은 TDD 를 쓰는 환경에서 더 설득력 있을 것 같다.
DI / TDD 개념이 머리에 들어오니 확실히 클래스 구성하는 것이 많이 이뻐졌다.
어스팩트 스타일은 뭐 주면 쓰고 그런 스타일로 직접 기능을 추가할 경우는 거의 없을 것 같다.

일단 이런 기초 개념 위에 이후 챕터에서 나올 복잡한 기능들의 벽돌 쌓기를 시작하는 것이니 한번 쭉 따라가 보려고 한다.
사실 뒤쪽에 있는 몇 가지 것들은 여럿이 일하는 회사에서나 도움이 많이 될 것 같은 것들이 있다.
직접 구현한다치면 많은 테스트 케이스를 거쳐야하거나 퍼포먼스가 잘 안 나오거나 구문이 예쁘지 않을 만한 것들.

스프링은 많은 사람들이 쓰고 쓰인지 꽤 오래되서 노가다 판에서 기능이 부족하거나 오작동하는 면은 거의 없을 것 같다.
게다가 릴리즈 주기도 매우 짧다.
단지 얼마나 실제로 간편하게 활용활 수 있을 것인가의 문제.

모두 알 겠지만 여럿이 프레임웍을 같이 쓸 때의 장점은
멀 어떻게 해야할지 몰라할 때나 구현 줄거리를 설명할 때 (패턴 처럼) 프레임웍 책의 여기를 보세요 할 수 있겠고, 
JSP 를 통으로 쓰게 했을 때 발생할 수 있는 중구난방 코드를 그나마 어느 정도 제어할 수 있을 것이란 것.
URL 라우팅 정책이라든지, 파라메터 패싱 방법, 컨트롤러 구성법, JSP 로 인자 넘기는 방법 정도만 통일 되도 괜찮을 듯 하다.
게다가 자바에서는 파일 첨부 처리도 기본으로 제공 안 해서 라이브러리 써야하지 않나. =,=

iBatis 는 어제 다시 꺼내보다 역시나 하고 다시 접었는데
Spring 은 상상하면 도움이 많이 될 듯 싶다.

Spring 끝나면 진짜 마지막으로 iBatis / Hibernate 다시 꺼내보고
이번에도 틀어지면 진짜 안녕.

### 2010.07.30 2

3 분의 1 은 읽었고, 3 분의 1 은 필요 없어서 제꼈고, 낼 볼 3 분의 1 남았다.
2.0 기준 책이지만 어쨌든 대실망이다.
스프링 기반이 DI + AOP 인데, 이거 AOP 너무 후져서 쓸 수가.
명시적이지도 않고, 디버깅도 힘들겠고, 사용법도 열라 어렵고.


### 2010.07.31

Spring in Action 다 봤는데, 우울하기만 하다.
3.0 What's new 를 좀 볼까.


### 2010.08.01

Spring 3 MVC 파트 먼저 보고 있는데 클래스간 역할 구분은 진짜 철저하게 해 놓은 것 같다.
좀 효율이 떨어지더라도 먼가 교환해서 쓸 수 있게 해 놓았다.
이전 버전에서도 그러긴 했지만 대신 엄청 난잡했는데, 
복잡도도 많이 줄어들고 장점과 단점의 수준이 납득할 정도로 밸런스가 맞아 가는 것 같다.

Spring 은 자바 서버계의 MFC 다.
꼭 쓸 필요도 없고 엄청 쉬워지는 것도 아니나 쓰면 가우가 날 것 같다.
좀 더 읽다 보면 이 사람들 사고가 좀 이해되기 시작할 듯.
하긴 tomcat 만든 사람들 사고에 적응하는데도 꽤 오래 걸렸었다. =,=

썬에서 만들다 버린 tomcat, 스프링 소스에서 주워다가 열심히 작업하고 있는데
tomcat + Spring 이 GlassFish 에 밀리지 않으니 썬 입장에서는 참 아행행할 것 같다.

GlassFish 기반 구조 진짜 잘 만들긴 했는데, 그 위에 Java EE 올려서 배포하는 바람에 쓸 수가 없다. =,=
GlassFish 가 사는 방법은 레이어 쪼개서 Java EE 떼버리고 Spring 깔끔하게 쓸 수 있게 해주는 거다.
정체성 혼란이 발생하려나?

다른건 모르겠지만 일단 Spring MVC 가 Java EE JSF 보다는 방향이 맞다.