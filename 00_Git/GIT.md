## GIT?

분산 버전 관리 시스템이다.

1. 코드 저장
2. 코드를 이전 상태로 돌려줌
3. 협업을 쉽게 해줌

### Github?

깃을 이용한 오픈소스 저장소

### Git-Basic

우리가 올리고 싶은 코드는,

`작업공간 - staging Area - Repository(저장소)` 세개의 공간을 거치게 된다.

__작업공간__

우리가 작업하는 공간

__staging Area__

`add` 후 머물게 되는, 저장되기전 거쳐가는 공간

__저장소__

`commit`후에 올라가는 공간 원격 저장소에 저장된다.

commit은 하나의 체크포인트로, 문제가 생기면 언제든지 돌아갈 수 있다.



## 명령어

- pwd: 현재 위치
- cd: 디렉토리 이동
- mkdir: 디렉토리 만들기
- is -al: 폴더에 있는 것을 보여줌
- clear: cmd 창 청소
- vim memo.txt: 파일 생성
- i: 쓰기모드
- wq: 저장후 나가기
- cat memo.txt: 내용을 보여준다
- status: 상태를 보여준다 (연결 된거나 안된거)
	- untracked file : 추적되고 있지 않은 파일
	- add를 통해서 추가
- cd ..: 뒤로가기



## 브랜치

다른 사람이 하고있는 것을 건들고 싶지 않을 때 따로 가지를 치면 된다

- git branch branchname

만약 다른 브랜치로 이동 하여 작업하고 싶다면,

- git checkout master



## merge

다른 브랜치와 지금 내가 있는 브랜치의 작업을 합치고 싶을 때

뒤에서 앞에꺼 머지하고, 앞에서 뒤에꺼로 역으로 머지해주면 된다. (?)



## 명령어

- `git init`을 통해 프로젝트를 관리할 것이라는 것을 알려줌. (최초 한번만)
- `git status`로 저장소 상태 체크
- `git add` staging area로 올린다.
- `git commit -m "msg"` 간단한 메모와 함꼐 저장소로 올린다.
- `.gitignore` 에 올리면 안되는 부분은 이 명령어를 통해 미리 막아두자.

[여기](gitignore.io)에 들어가서 gitignore에 안올려도 되는 것은 어떤것인지, 또 어떤 것을 올리면 안되는지 등을 봐두자.

### 협업

branch와 pull request, merge가 핵심이다.

메인(master)을 중심으로 브런치를 각각 파서 작업한후에 push를 하기 전, 마스터에게 pull request를 전송한다.

마스터가  이를 확인하고  merge를 하면 된다!



