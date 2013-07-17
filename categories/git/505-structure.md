# 리포지터리의 구조

인덱싱과 커밋 명령으로 넘어가기 전에 리포지터리를 구조를 잠시 살펴볼 필요가 있다.
서두에 이런 졸린 기술을 하는 것이 
이 구조를 이해하고 나면 괴상해 보이는 Git 명령들을 스스로에게 납득시키기가 수월해 진다.

Git 리포지터리에는 오브젝트 스토어와 인덱스 두 개의 주요 데이터가 있다.
오브젝트 스토어는 리포지터리의 핵심이고
오브젝트 스토어에 커밋할 내용을 임시로 저장하는 곳이 인덱스다.

Git 는 파일 내용의 SHA1 해쉬를 파일의 이름으로 사용한다.
리포지터리 구조를 보기 전에 이 특징을 보고 넘어 간다.


새로 트래킹할 파일이나 커밋 후 수정한 파일은 `git add` 명령으로 인덱스에 등록한다.
`git add`  는 오브젝트 스토어에 파일에 대한 블롭을 생성하고 인덱스를 업데이트 한다.
인덱스 파일이 파일명과 블롭의 연결을 관리한다.
트리는 아직 생성되지 않는다. 


`git add, rm, mv` 명령을 내릴 때마다 인덱스가 업데이트된다.



코딩작업의 한 단위가 끝났으면 `git commit` 명령으로 커밋한다.
커밋은 새로운 트리 오브젝트와 커밋 오브젝트를 만드는 일이다.
블롭들의 변화에 따라 트리들이 추가될 수도 있고 기존 것들이 재사용될 수도 있다.
새 커밋 오브젝트는 바로 이전 커밋에 대한 링크를 갖고 브랜치는 새로 생성된 커밋의 링크를 갖도록 업데이트된다.


### SHA1 파일명

오브젝트 스토어에 저장되는 모든 파일들은 내용의 SHA1 해쉬가 이름이 된다.
SHA1 해쉬는 20 byte 또는 40 문자로 구성되는 16 진수 숫자열이다.
블롭, 트리, 커밋, 태그 파일 모두 SHA1 해쉬를 이름으로 갖는다.

원래 파일명과 해쉬 생성 기계에 상관 없이 파일 내용이 같으면 SHA1 해쉬값은 같다.
SHA1 해쉬가 같은 파일들은 한 벌만 저장된다.

이름 대신 SHA1 해쉬를 쓰므로 커밋이 겹겹이 쌓인 상태에서도 SHA1 해쉬만 가지고 특정 버전의 파일을 쉽게 가리킬 수 있다.
해쉬만으로 동일여부를 판단하므로 매우 큰 오브젝트들의 존재 유무를 데이터 전송없이 알아낼 수 있다. 
트리 오브젝트의 해쉬가 같다면 서브 디렉토리 모든 파일을 비교하지 않고도 두 디렉토리 내용이 같다는 보장을 얻을 수 있다.
파일 내용이 파일명에 드러나고 그러한 파일명이 트리 오브젝트에도 저장되기 때문에
트리 오브젝트의 해쉬는 서브 디렉토리 전체의 내용을 반영한다.

내용이 다른 파일간 SHA1 해쉬가 충돌할 가능성은 있다. 하지만 엄청나게 낮다.
충돌나면 어떻게 되는지에 대한 말은 안 보인다. =,=

Git 리포지터리는 오브젝트 스토어와 인덱스로 구성된다.


### 오브젝트 스토어

기록에 관해 상상할 수 있는 모든 것은 여기에 저장된다.
파일 시스템상의 평범한 디렉토리다.
오브젝트 스토어 구조는 리포지터리를 효율적으로 클론할 수 있도록 만들어졌다.
오브젝트 스토어에 저장되는 오브젝트는 딱 네 종류다.

블롭,

파일의 버젼들은 블롭으로 저장된다.
블롭에는 파일 데이터만 저장된다. 파일 이름은 저장되지 않는다.
Git 는 diff 결과를 저장하지 않는다. 모든 파일의 모든 버전들을 원본 그대로 저장한다.
diff 는 필요할 때마다 계산해서 표시한다.
블롭은 데이터 구조의 최하단에 있으며 다른 오브젝트에 대한 링크를 갖지 않는다.

트리,

블롭의 해쉬, 패스, 기타 메타 정보가 기록된다.
트리 오브젝트는 다른 트리나 블롭에 대한 링크를 갖는다.

커밋,

커밋 오브젝트에는 커밋 메타 데이터와 커밋 과정에서 만들어진 루트 트리의 링크가 저장된다.
커밋은 이전 커밋에 대한 링크를 가진다.
머지의 결과로 만들어진 커밋은 여러 부모 커밋을 갖는다.
서로 다른 커밋 오브젝트가 같은 트리에 대한 링크를 가질 수 있다.

태그,

커밋에 사람이 읽기 쉬운 이름을 달기 위해 사용한다.


### 인덱스

인덱스는 커밋할 내용을 임시 저장하는 비공개 스토리지다.
좀더 구체적으로 표현하면 커밋시 트리 오브젝트를 만드는데 필요한 정보를 임시 저장하는 버퍼다.
커밋시 변경된 파일 중 어떤 파일을 저장할 것인지 지정하기위해 인덱싱 절차가 필요하다.

파일에 대한 블롭 오브젝트는 파일이 인덱스에 등록될 때 미리 생성하고 
트리 오브젝트는 인덱스를 가지고 커밋시 생성한다.
클론시 인덱스는 복사되지 않는다.

참고로 커밋 전에 한 파일을 여러번 인덱싱하면 고아 노드가 발생한다.
<http://stackoverflow.com/questions/1341675/multiple-git-add-before-git-commit>