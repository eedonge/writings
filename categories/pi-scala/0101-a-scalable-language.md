# A Scalable Language

2011-07-07 17:09

### A Scalable Language / 점진적으로 확장가능한 언어

스칼라라는 이름은 "Scalable Language" 라는 뜻이다.
Scalable 이란 단어는 '점진적으로' 확장해 나갈 수 있다는 의미를 가지고 있다.

다른 언어에서는 용도가 고정되어 있을 법한 문법들을 스칼라에서는 확장, 재정의 할 수 있다.
스칼라는 몇 가지 메타 원칙을 정해 두고 이것을 이용해 구문을 계속 확장해 나갈 수 있다.
라이브러리를 추가하는 것이 아니라 흡사 언어를 확장해 나가는 듯한 느낌이 들 것이다.

스칼라는 자바 플랫폼에서 동작하며 모든 자바 라이브러리와 매끄럽게 동작한다.
자바 콤포넌트를 가져다 쓰는 스크립트 작성에도 용의하지만,
큰 시스템이나 재사용 가능한 콤포넌트를 개발하는데 더 적합하다고 볼 수 있다.

스칼라는 객체 지향(object-oriented) 프로그래밍 개념과 함수형(functional) 프로그래밍 개념을
정적 타입(statically typed) 언어에 융합시켰다.
OOP 와 FP 의 융합은 스칼라의 많은 측면들에서 나타난다.
(앞으로는 object-oritented 를 OO 로 functional 을 F 로 축약하여 적겠다.)

이 두 개의 프로그래밍 스타일은 확장성(scalability)에 있어서 서로 보완적인 역할을 한다.
FP 적인 구문은 미시적인 부분에서 코드를 빠르게 작성하는데 도움을 준다.
OOP 적인 구문은 보다 큰 시스템 구조를 만들고  새로운 요구사항을 수용하는데 도움을 준다.
두 프로그래밍 스타일의 결합은 새로운 종류의 프로그래밍 패턴과 콤포넌트 추상화를 가능하게 한다.

이 챕터는 "왜 스칼라인가?" 라는 질문에 답을 하기 위해 마련했다.
이 언어의 디자인과 그렇게 디자인 해야했던 이유에 대한 개요를 제공할 것이다.


### A language that grows on you / 맞춤 언어

다른 프로그램들은 다른 프로그래밍 구조물(construct)들을 필요로 한다.

다음 작은 예제를 보자.

	var capital = Map("US" -> "Washington", "France" -> "Paris")
	capital += ("Japan" -> "Tokyo")
	println(capital("France"))

이 프로그램은 나라와 수도 이름으로 된 맵을 만들고, Japan 과 Tokyo 조합을 추가하고, France 에 연결된 수도를 프린트한다.

예제에 사용된 코드는 꽤 고수준의 표기법을 갖고 있다.
불필요한 세미콜론이나 타입 설명들로 어수선하지 않다.
구문의 느낌이 Perl, Python, Ruby 같은 현대적 '스크립팅' 언어와 비슷하다.
이 세 가지 언어들은 공통적으로 언어 레벨에서 맵(associative map) 수식을 지원한다.

맵은 프로그램을 읽기 쉽고 간결하게 만든다.
하지만, 언어에서 제공하는 것 이상의 기능이 필요할 경우 어려움에 처하거나 아예 활용을 못하는 경우가 발생할 수 있다.
스칼라의 맵은 언어 레벨에 있지 않고 단순히 확장가능한 라이브러리이기 때문에 필요할 경우 섬세한 조율이 가능하다.

위 프로그램에서는 기본 맵이 사용되고 있다.
하지만 이것은 쉽게 바꿀 수 있다.
HashMap 이라던지 TreeMap 구현 코드를 사용할 수 있다.
SynchronizedMap trait 을 섞어서(mixing in) 맵이 thread-safe 해야함을 기술할 수도 있다.
맵의 기본 값을 기술할 수도 있고, 메서드를 오버라이드할 수도 있다.

이 모든 것은 필요에 따라 선택할 수 있는 라이브러리에 기반하기 때문에
(언어 자체의 기능 추가 없이도) 항상 사용자의 필요에 따라 프로그램을 재단할 수 있다.


### Growing new type / 새로운 타입 생성

Eric Raymond 는 소프트웨어 개발을 성당과 시장 (the cathedral and bazaar) 이라는 두 개의 비유로 묘사하였다.
성당과 시장 : <http://www.catb.org/~esr/writings/cathedral-bazaar/>
성당과 시장 한글 번역본 : <http://wiki.kldp.org/wiki.php/DocbookSgml/Cathedral-Bazaar-TRANS>

성당은 짓는데 오래 걸리는 완벽한 빌딩을 뜻한다.
성당은 한번 완공이 되면 변하지 않고 오랜 시간동안 유지된다.

반대로 시장은 일하는 사람들에 의해 매일 매일 확장되고 변화한다.
레이몬드의 글에서 시장이란 오픈소스 소프트웨어 개발을 의미한다.

Guy Steele 은 "growing a language" 라는 강연에서 똑같은 개념을 언어 디자인에도 적용할 수 있다고 말했다.
스칼라는 사용자가 확장하고 수정할 수 있다는 점에서 성당보다는 시장에 가깝다.
하나의 완벽한 언어로 사용자가 필요로 할 모든 구문을 제공하는 대신에
그러한 구문을 만들 수 있는 도구를 제공한다.

예를 보자.

많은 어플리케이션들은 오버플로우가 없고 마음대로 반올림되지 않는 큰 정수 타입이 필요하다.
스칼라에서 이런 정수 타입은 scala.BigInt 클래스다.
아래는 입력된 정수 값의 팩토리얼을 계산하는 메서드다.

	def factorial(x: BigInt): BigInt =
		if (x == 0) 1 else x * factorial(x - 1)

factorial(30) 을 실행한 결과는 다음과 같다.

	265252859812191058636308480000000

정수 상수와 * , - 같은 연산자를 쓰고 있기 때문에 BigInt 는 언어의 내장 타입 같아 보인다.
하지만 BigInt 는 스칼라 기본 라이브러리에 정의되어 있는 클래스일 뿐이다.
만약 BigInt 클래스가 없었다면, 스칼라 프로그래머는 Java 의 java.math.BigInteger 를 가지고 손수 클래스를 만들었을 것이다.
(사실 스칼라의 BigInt 는 그렇게 구현되었다.)

물론, 자바 클래스를 바로 사용할 수도 있다.
하지만 자바의 타입들은 언어에 내장되어 있다는 느낌을 주지 않기 때문에 별로 산뜻하지 못하다.

	import java.math.BigInteger

	def factorial(x: BigInteger): BigInteger =
		if (x == BigInteger.ZERO)
			BigInteger.ONE
		else
			x.multiply(factorial(x.subtract(BigInteger.ONE)))

BigInt 는 다른 많은 숫자 타입들중 한 가지일 뿐이다.
big decimals, complex numbers, rational numbers, confidence intervals, polynomials 등 목록은 길다.
어떤 언어들은 이러한 타입들을 언어 차원에서 구현하고 있다.
예를 들어, List, Haskell, Python 등은 big integer 를 구현하고, Fortran, Python 은 complex number 를 구현한다.

하지만 예상할 수 있는 모든 타입을 구현한다면 언어가 너무 커져서 관리하기 어려워질 것이다.
그러한 언어가 존재한다 하더라도, 어플리케이션에 따라 언어가 제공하지 않는 또 다른 숫자 타입이 필요할 수 있다.
그러므로, 모든 것을 언어 차원에서 지원하려는 접근은 언어를 우아하게 확장시키지 못한다.

스칼라는 사용하기 편한 라이브러리를 제작할 수 있게 해준다.
라이브러리를 통해 추가되는 기능들이라도  언어 차원에서 제공되는 듯한 느낌을 줄 수 있다.
이를 통해 사용자가 원하는 방향으로 언어를 성장시켜 나갈 수 있도록 한다.


### Growing new control constructs / 새로운 컨트롤 구문 만들기

이전 예제는 내장 타입처럼 편하게 쓸 수 있는 새로운 타입을 추가하는 방법을 보였다.
똑 같은 확장 원리가 컨트롤 구문에도 적용될 수 있다.
이런 종류의 확장성은 "actor"에 기반한 병렬처리 프로그래밍용 스칼라 API 에 잘 나타나 있다.

멀티코어 프로세서들이 확산되면서 멀티 코어를 통한 예상 성능에 도달하기 위해서는 어플리케이션에서 더 높은 병렬성을 제공해야 한다.
이를 위해 동시 실행 스레드에 연산이 분산되도록 코드를 제작성해야 할 수도 있다.
기쁘지 않은 사실은 신용할 만한 다중 스레드 어플리케이션을 작성하는 것이 현실적으로 쉬운일이 아니란 것이다.

자바 스레드 모델은 시스템이 커졌을 때 추척하기 힘든 메모리 공유와 잠금 개념에 기반한다.
자원에 대한 경쟁 상태나 잠복된 데드락 문제점이 없다는 것을 증명하기가 어렵다.
이는 테스팅 과정에서는 나타나지 않다가 실서비스에서 나타날 수 있다.
확실히 안전한 대안은 Erlang 프로그래밍 언어에서 사용하는 "actors" 같은 메시지 패싱 아키텍쳐이다.

자바는 스레드 기반의 병렬처리 라이브러리를 가지고 있다.
스칼라 프로그램은 다른 자바 API 처럼 스레드 라이브러리를 바로 쓸 수도 있다.
하지만, 스칼라는 Erlang 의 액터(actor) 모델을 구현한 라이브러리를 추가로 제공하고 이를 권장한다.

액터는 스레드를 가지고 병렬처리를 추상화한 것이다.
액터들은 서로 메시지를 주고 받으며 통신한다.
액터는 메시지 전송과 수신의 두 가지 기본 작업을 한다.
느낌표로 표시되는 전송 작업은 엑터에 메시지를 전송한다.
아래는 recipient 라는 엑터에 메시지를 전달하는 예다.

	recipient ! msg

전송은 비동기적이다.
즉, 전송하는 액터는 메시지가 수신되고 처리되고 답이 돌아오는 것을 기다리지 않고 메시지 전송 직후 다음 행으로 진행한다.
모든 액터는 수신되는 메시지가 들어갈 메일박스를 가지고 있다.
액터는 수신 블럭 (receive block) 을 통해 메일박스에 도착한 메시지를 처리한다.

	receive {
		case Msg1 => ... // handle Msg1
		case Msg2 => ... // handle Msg2
		// ...
	}

수신 블럭은 메시지 패턴으로 메일 박스를 조회하는 몇 개의 case 문들로 구성된다.
case 에 부합하는 첫 번째 메일박스 메시지가 선택되면 메시지를 가지고 해당하는 코드를 실행한다.
메일박스가 case 에 부합하는 메시지를 가지고 있지 않을 경우 액터는 실행을 중지하고 새로 수신되는 메시지를 기다린다.

다음은 간단한 체크섬 계산기 서비스를 구현한 스칼라 액터의 예다.

	actor {
		var sum = 0
		loop {
			receive {
				case Data(bytes)			=> sum += hash(bytes)
				case GetSum(requester)	=> requester ! sum
			}
		}
	}

먼저 지역 변수 sum 을 0 으로 초기화한다.
loop 문은 안의 receive 문을 반복 실행한다.
receive 문은 메시지를 수신한다.
Data 메시지를 수신하면 수신된 bytes 의 해쉬를 sum 변수에 더한다.
GetSum 메시지를 수신하면 현재 sum 변수의 값을 requester 에게 전송한다.
requester 필드는 GetSum 메시지에 포함되어 있는데 일반적으로 요청한 액터를 가리킨다.

지금 시점에서 이 액터 예제를 완벽히 이해할 필요는 없다.
확장성의 주제에 대해 이 예제가 보여주는 중요한 점은 actor, loop, receive, message send (!) 등의 어휘가 스칼라 언어에 내장된 것이 아니라는 것이다.
actor, loop, receive 가 언어에 내장된 while 이나 for 루프 처럼 보이고 동작하지만 실제로는 스칼라 액터 라이브러리에 정의되어 있는 메서드들일 뿐이다.
'!' 또한 내장 연산자 같아 보이지만 액터 라이브러리에 정의되어 있는 메서드이다.
이 네 가지 어휘들은 모두 스칼라 프로그래밍 언어로 부터 독립되어 있다.

스칼라의 receive 블럭과 send (!) 문법은 Erlang 에서의 그것들과 흡사하다.
하지만, Erlang 에서는 이 어휘들이 언어에 내장되어 있다.

스칼라는 수행 실패한 액터나 시간 초과 모니터링과 같은 Erlang 의 다른 병렬처리 프로그래밍 구조들 또한 구현하고 있다.
액터는 동시 실행되는 분산된 연산을 표현하기 위한 매우 쾌적한 수단인 것으로 인정되고 있다.
라이브러리에 정의되어 있지만 언어의 한 부분인것 처럼 사용할 수 있다.

이 예는 스칼라를 병렬처리 프로그래밍과 같은 매우 특수한 새로운 방향으로도 확장시켜 나갈 수 있다는 것을 보여준다.
이런 일을 하기 위해서는 확실히 좋은 아키텍트와 프로그래머가 필요하다.
하지만 중요한 점은 이것이 실현 가능하다는 것이다.
스칼라에서는 급진적으로 새로운 응용 영역을 다루는 개념들을 디자인하고 구현할 수 있다.
동시에 언어 차원에서 이를 지원하고 있다는 느낌 또한 줄 수 있다.


참고, 병렬처리와 관련해 액터에서 핵심적인 것은 메시지 패싱이나 패턴 매칭이 아니라 비동기적으로 동작한다는 부분이다.
메시지 패싱은 비동기 컨트롤을 구현하기 위한 수단중 하나이다.