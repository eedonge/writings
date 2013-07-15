XHTML 을 버리자
2011-02-08 19:08
*

HTML 계는 총체적으로 카오스 상태인데 태깅 방향을 정하는데 몇 가지 중요하게 고려할 사항들이 있습니다.

XHTML 을 지원하는 브라우저의 XHTML 랜더링 엔진을 기동하려면
웹 서버에서 Content-Type 헤더필드에 application/xhtml-xml 을 박아서 보내야합니다.
태거가 지정할 수 있는 것은 아니고 서버 관리자나 프로그래머가 서버설정에 손을 봐야합니다.

웹 페이지를 XHTML 표준으로 코딩한다고 해도
웹 서버에서 Content-Type 헤더필드에 일반 웹 페이지와 동일한 text/html 을 박아서 보내면
브라우저는 HTML 랜더링 엔진을 사용합니다.
믿거나 말거나.

그러니, 태거들이 아무리 XHTML 방식으로 태깅한다고 해도,
페이지 첫머리에 아무리 DOCTYPE 을 줄줄이 준다고 해도,
실제 발생하는 페이지 랜더링은 브라우저는 종류에 상관없이 모두 HTML 렌더링엔진이  한다고 보시면 됩니다.
믿거나 말거나(2).

더 큰 문제는 XHTML 문서를 현재 처럼 HTML 타입으로 전송하면 위험하다고 합니다.
자세한 내용은 아래 (영어 =,=)
<http://hsivonen.iki.fi/doctype/>
<http://hixie.ch/advocacy/xhtml>

그래서 몇몇 전문가들은 (국내외 사이비 전문가 말고 W3C 표준 제정에 참여하는 전문가들) XHTML 을
사용하지 말기를 권고하고 있습니다.

현재 XHTML 2.0 그룹은 해체되어 XHTML 은 앞으로 더 나오기가 어렵게 되었고,
기업들과 W3C 는 HTML 5 에 올인하고 있는 형국입니다.

그리고, XHTML 사용불가의 종결자 M$ 가 있습니다.
IE 는 전 버전에 걸쳐서 Content-Type : application/xhtml+xml 을 지원하지 않습니다.
믿거나 말거나(3).

그러니, 이 세상이 멸망한 후 다시 만들어지기 전까지
XHTML 은 현실적으로 사용이 불가능하며 곧 사라질 스펙입니다.

그럼, HTML 5 은 아직 오지 않았고, 브라우저는 버전마다 엉망 진창인데 우린 뭘 써야하나요?
걍 HTML 을 쓰시면 됩니다. (이게 뭔 말?)

이제 HTML 의 버전 언급은 무의미하게 되어가고 있습니다.
HTML 그룹도 버전 붙이기를 포기했고요.
앞으로 먼가 웹 페이지 태깅 스러운 것들의 스펙을 지칭할 때는 버전 빼고 걍 HTML 이라 부르게 됩니다.

그럼 DOCTYPE 뒤에 복잡한 것들과 기타 등등 XHTML 에서 지키라고 했던 잡스러운 것들은?
다 무시하시고, XHTML 책들은 다 버리시면 됩니다.

JSF 2.0 등이나 XHTML 기반으로 한 기술들이 계속 나오고 있잔아요?
네, 그분들도 다 망했다고 보시면 됩니다.

그럼 페이지 코딩할때 상단엔 뭘 적나요?
이렇게 하시면 끝입니다.

	<!DOCTYPE html>
	<html>
	<head> </head>
	<body> </body>
	</html>

진짜로요?
네. =,=

저렇게 하면 브라우저 비호환 문제가 사라지나요?
아니죠. =,=

그럼, 그건 누가 어떻게 해결?
여러분이, 손가락과 눈으로 확인하면서, 무한 Reload, =,=

HTML 의 세계로 다시 잘 오셨습니다.