# First Steps, Function

2011-07-08 23:17

펑션은 아래 와 같이 만들 수 있다.

	scala>  def max(x: Int, y: Int): Int = {
				if (x > y) x
				else y
			}

	max: (x: Int,y: Int)Int

펑션 정의는 def 로 시작한다.
예에서 펑션 이름은 max 이고 괄호 안에 콤마로 구분된 인자 리스트를 적는다.
모든 펑션 인자 다음에는 콜론을 붙이고 타입을 기술해야 한다.
컴파일러가 펑션 인자의 타입을 추론할 수 없기 때문이다.
예에서는 max 라는 펑션이 Int 타입의 인자 x, y 를 받고 있다.
인자목록을 닫는 괄호 다음에는 또 다른 Int 가 있다.
이것은 펑션의 결과 타입을 정의한다.

책, 73p Figure 2.1 참조

펑션 결과 타입 다음에는 등호와 펑션 몸체를 담는 중괄호가 나온다.
이 경우에는 펑션의 결과로 무엇이 더 큰지에 따라 x 와 y 중 하나를 선택하는 if 수식이 몸체다.
스칼라의 if 수식은 자바의 삼항연산자처럼 값이 될 수 있다.
if (x > y) x else y 은 자바의 (x > y) ? x : y 와 비슷하다.
F 세계의 관점에서 펑션은 값을 만드는 수식을 정의하는 것이다.
펑션이 값이란 관점은 펑션 몸체 전에 나오는 등호가 암시하고 있다.

(등호가 등장했고, if 가 문장이 아니라 수식이고, return 문이 없어도 마지막 수식의 결과가 펑션의 결과값이 된다)

때때로 스칼라 컴파일러는 펑션 결과 타입을 요구한다.
재귀호출 펑션의 경우 결과 타입을 반드시 적어주어야 한다.
하지만 위의 max 에서는 결과 타입을 생략할 수 있다. 컴파일러는 이것을 추론해 낸다.
더해서 펑션이 한 문장으로만 구성된다면 중괄호도 생략할 수 있다.
그래서 max 를 다음과 같이 짧게 적을 수도 있다.

	scala> def max2(x: Int, y: Int) = if (x > y) x else y
	max2: (x: Int,y: Int)Int

하지만, 컴파일러가 요구하지 않는다고 해도 펑션 결과 타입을 명시적으로 기술하는 것은 좋은 습관이다.
이렇게 함으로써 코드를 읽기 쉽게 만들 수 있다.

펑션을 정의했으면 다음과 같이 호출한다.

	scala> max(3, 5)
	res4: Int = 5

다음 예의 펑션은 인자도 받지 않고 의미있는 값도 돌려주지 않는다.

	scala> def greet() = println("Hello, world!")
	greet: ()Unit

greet() 펑션을 정의했을 때 인터프리터는 greet: ()Unit 으로 응답한다.
Unit 은 greet 의 결과 타입이다.
의미있는 값을 리턴하지 않는 펑션의 리턴 타입은 Unit 이다.
스칼라의 Unit 타입은 자바의 void 타입과 비슷하다.
사실 void 를 리턴하는 모든 Java 메서드는 스칼라에서 Unit 을 리턴하는 메서드로 투사된다.

Unit 을 리턴하는 함수는 항상 사이드 이펙트를 발생시키기 위해 사용한다고 보면 된다.
greet() 에서 이 사이드 이펙트는 stdio 에  "Hello, world!" 를 출력하는 것이다.


### 참고

펑션 정의에서 몸체 { } 를 생략할 수 있는 경우 = 가 유용해 보인다.
하지만 { } 를 써야하는 경우 자바 프로그래머들에게는 = 가 밉상으로 보일 수 있겠다.
머리를 긁적거리게 만드는 것은 나중에 보게 되겠지만 = 를 빼버릴 수 있는 상황도 존재한다는 것이다. =,=

