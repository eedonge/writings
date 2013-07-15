# Natural Key vs Surrogate Key

2010-09-28

당장 ORM 을 쓰지 않고 JDBC 나 iBatis 를 쓰더라도
신규 디비 스키마를 만드시는 과정에서 아래 몇 가지만 지켜 주시면
추후 ORM 시스템으로 마이그레이션 하는 작업이 쉬워집니다.

먼저 모든 테이블에 숫자형태의 id 필드를 생성하고 값이 자동 생성되게 합니다.
필드명은 `user_id`, `order_id` 말고 그냥 `id` 입니다.
그리고 이것이 프라이머리 키가 됩니다.

콤포지트 키를 많이 쓰는 예전 Codd 방식으로 디비 디자인을 하는 것과 심리적으로 큰 차이가 있습니다.
처음에 받아들이기 힘든데요, 이렇게 하면 ORM 도입하는데 많은 문제가 해결됩니다.

RDB (MySql) 와 OOP (Java) 의 가장 큰 차이는 데이터를 가리키는 방법입니다.
자바에서는 레퍼런스 하나가지고 오브젝트를 찾을 수 있지만,
RDB 에서는 콤포지트 키가 자주 등장하므로 해당 행을 찾거나 동등 비교를 하려면 여러 값을 합쳐야 합니다.
이 문제를 `id` 필드로 해결하고자 하는 것입니다.
`id` 필드가 도입되면 Java 에서도 RDB 에서도 비슷한 방식으로 동등 비교를 할 수 있게 됩니다.
데이터를 ORM 의 오브젝트 케쉬에 올리는 과정도 퍼포먼스가 급상승합니다.

데이터는 어플리케이션보다 생명주기가 깁니다.
어플리케이션을 위해 신성한 데이터베이스에 불필요한 필드를 추가할 필요가 있을까요?
데이터도 어플리케이션이 없으면 쓸 수 없습니다.
어플리케이션을 위해 적당한 서비스가 필요합니다.

외래키들만 있는 릴레이션 테이블에도 id 를 넣을 필요가 있을까요?
이런 테이블에도 모두 넣어야 합니다.
외래키만 있는 테이블을 Java 스페이스에 올리는데 id 필드가 없으면
콤포지트 키들을 매번 시리얼라이제이션 해야하는 오버헤드가 상당해 집니다.
그리고 릴레이션 테이블은 숙명적으로 컬럼이 추가되어 엔터티로 재탄생할 확률이 높습니다.

기존에 프라이머리 키 기능을 행하던 콤포지트 키들은 어떻게하나요?
별도의 유니크 인덱스로 묶어줍니다.
네, 오버헤드가 있을 수 있습니다만 기계에 일을 좀 더 주고 사람이 좀더 편해지자면 감수할만 하다고 봅니다.
기계 부족 보다는 인력란이 심각하니까 인간 위주로 정책을 많이 도입할 필요가 있어 보입니다.