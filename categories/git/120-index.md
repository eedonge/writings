# Git Indexing


### 인덱스에 파일 추가

커밋하려는 새 파일이나 커밋후 수정한 파일은 `git add` 명령으로 인덱스에 등록한다.

	$ git add <file>

특정 서브 디렉토리의 전체를 인덱싱할 수도 있다.

	$ git add <directory>

프로젝트 디렉토리의 전체를 인덱싱할 수도 있다.

	$ git add .


### 인덱싱 취소

인덱스에 스테이징한 것을 취소 하려면.

	$ git reset HEAD <file>

워킹 디렉토리의 파일은 그대로 두고 인덱스에서만 삭제하려면, 

	$ git rm --cached <file>
	 

### 인덱스 확인

인덱스의 상태는 `git status` 명령으로 볼 수 있다.

	$ git status

인덱스에 등록된 파일 목록을 볼 수 있다.

	$ git ls-files -s

오브젝트 스토어의 파일을 꺼내 볼 수도 있다.

	$ git cat-file -p <object id>


### 파일 삭제

워킹 디렉토리 파일을 삭제하면서 인덱스에도 파일 삭제 명령을 스테이징한다.

	$ git rm <file>

기본 `git rm` 명령은 커밋 안 된 파일이 삭제되는 것을 막기 위해
지우려는 파일이 HEAD 내용과 일치하지 않으면 오류를 낸다.
이때 수정하던 파일을 강제삭제하려면 `-f` 를 붙여주어야 한다.

	$ git rm -f <file>

물론 `git rm` 을 실행하고 `git commit` 해야 오브젝트 스토어가 업데이트 된다.


### 파일 이동

이렇게 할 수도 있고,

	$ mv foo.html bar.html
	$ git rm foo.html
	$ git add bar.html

다음 명령으로 간단히 할 수도 있다.

	$ git mv foo.html bar.html
