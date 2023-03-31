# Quest 00. 형상관리 시스템

## Introduction
* git은 2021년 현재 개발 생태계에서 가장 각광받고 있는 버전 관리 시스템입니다. 이번 퀘스트를 통해 git의 기초적인 사용법을 알아볼 예정입니다.

## Topics
* git
  * `git clone`, `git add`, `git commit`, `git push`, `git pull`, `git branch`, `git stash` 명령
  * `.git` 폴더
* GitHub

## Resources
* [Resources to learn Git](https://try.github.io)
* [Learn Git Branching](https://learngitbranching.js.org/?locale=ko)
* [Inside Git: .Git directory](https://githowto.com/git_internals_git_directory)

## Checklist
* 형상관리 시스템은 왜 나오게 되었을까요? - 파일 서버 기반의 버전 관리의 문제점 때문.
// 문제점 1. 파일이 삭제될 경우 복구할 방법이 없다. 파일이 삭제되는 경우를 대비해서 백업을 해두지만 시점 차이로 인한 데이터 손실은 피할 수 없다.
2. 하나의 파일을 여러 사람이 동시에 작업할 수 없다.
3. 이전 데이터로 복구할 수 없다. 예를 들어 소스 코드 작성 중에 이전 소스 코드로 되돌아 가는 것이 불가능하다. 이런 상황을 대비해서 소스 코드를 백업하거나 소스 코드에 과거 이력 코드를 주석으로 남겨놔야한다.
* git은 어떤 형상관리 시스템이고 어떤 특징을 가지고 있을까요? 분산형 형상관리 시스템이란 무엇일까요? git은 분산 버전 관리 시스템(Distributed revision control system)임. 버전 관리 시스템은 크게 두가지로 분류할 수 있는데 첫째는 중앙집중식 버전관리 둘째는 분산 버전관리. 중앙 집중식 버전관리의 경우 central sever에서 코드를 가져오면, 그 코드의 commit(변경 기록들)은 가져오지 않고 오직 중앙 서버의 파일만 받아오는 반면 분산 버전관리 시스템은 해당 저장소를 변경 기록들과 함께 복제해 온다. 그래서 중앙 버전 관리 시스템의 경우 중앙서버에 문제가 생기면 변경 기록들을 전부 잃는 반면 분산 버전관리시스템은 중앙서버에 문제가 생겨도 clients 중 하나를 골라 변경기록들과 함께 서버를 복원시킬 수 있다.

* git은 어떻게 개발되게 되었을까요? git이 분산형 시스템을 채택한 이유는 무엇일까요? 
* git과 GitHub은 어떻게 다를까요?
git은 버전관리 툴, github은 git을 이용한 서비스라고 생각하면 될 것 같다. Github에서 제공하는 서비스를 활용하여 여러사람들이 하나의 저장소를 가지고 보다 쉽게 협업할 수 있다.
* git의 clone/add/commit/push/pull/branch/stash 명령은 무엇이며 어떨 때 이용하나요? 그리고 어떻게 사용하나요?
* clone : git clone https://github.com/Username/레포네임.git --? 원격 저장소의 데이터를 카피해서 내 pc 저장소에 복제할 때 쓰는 것.
* add : commit 하기 전 변경된 사항들을 staging area에 추가해 나가는 행위 --> git add filename 해당 파일을 staging area에 올려
* git add . 현재 디렉토리 하위에 있는 변경사항들만 staging area에 올려줌
* commit : git commit -m "commit meggage" --> staging area에 add된 파일들의 변경을 확정짓고 local repository에 올려줌
* push : git push 저장소명 브랜치명 / git push orgin master --> local area에 남긴 기록들의 history를 remote repository(원격 저장소)에 저장하는 행위
* git remote --> 저장소명 확인
* git push -u origin master --> -u 옵션은 최초 한번만 저장소명, 브랜치명을 입력하고 이후에는 git push 만 사용해도 되게 해줌
* pit push -f origin master --> 가급적 사용 x, -f옵션으로 강제로 현재 로컬 저자아소에 변경사항을 원격 저장소에 덮어 씌우는 행위
* pull : git pull --> remote repository의 변경사항들을 local area로 가져와 merge(병합)하는 행위 >>>> pull = fetch(변경사항을 가져오는 행위) + merge(가져온 변경사항을 적    용하는 행위)
*  pull은 아래 두가지로 쪼개질 수 있음
* git fetch
* git diff HEAD origin master # 이거는 fetch해서 가져온 변경사항과 현재 내 저장소를 비교해주는 명령어
* git merge
* branch : git branch --> 브랜치 목록을 불러온다
* git branch <branch_name> --> 이름이 branch_name인 브랜치를 생성한다.
* git checkout <branch_name> --> branch_name 브랜치로 작업공간을 전환해준다.
*브랜치란 독립적으로 어떤 작업을 진행하기 위한 개념임. 필요에 의해 만들어지는 각각의 브랜치는 다른 브랜치에 영향을 받지 않기 때문에, 여러 작업을 동시에 진행할 수 있음
*stash : git stash --> 현재 작업중인 변경사항을 임시 공간에 저장해두기 위한 명령어.
*git stash list # stashed된 변경사항들의 목록을 불러온다.
* git stash apply <stash_name> # stash_name stash를 불러온다. stash_name이 없다면 가장 최근의 stash를 불러온다.
 *git stash drop <name> # name의 stash를 제거한다. name이 주어지지 않으면 가장 최근의 stash를 제거한다. 
 *git stash pop # apply와 동시에 drop을 해주는 명령어
* git의 Object, Commit, Head, Branch, Tag는 어떤 개념일까요? git 시스템은 프로젝트의 히스토리를 어떻게 저장할까요?
*object : git이 파일을 관리하기 위해 만드는 파일 이는 tree, blob, commit, tag 4가지로 구성 commit의 SHA-1 값 중 앞 두자리를 폴더명으로, 뒷 38자리를 파일명으로 갖는다.
*여기서 commit object은 tree SHA-1값, parent 오브젝트의 SHA-1값, author, committer, commit message를 저장한다.
*Head는 커밋을 가르키는 포인터와 같은 역할을 하며 Branch는 작업 트리를 나타내고, Tag는 특정 커밋에 태그를 달아주는 역할을 한다.

* 리모트 git 저장소에 원하지 않는 파일이 올라갔을 때 이를 되돌리려면 어떻게 해야 할까요?
git reset을 사용해 커밋을 취소하는 방식, 두번째는 git revert를 사용하여 커밋 내용을 되돌리는 방식이다.
reset -->
git log --oneline --> 커밋기록 불러오기
git reset --hard commit_id --> 해당 커밋으로 돌아가서 원하지 않는 파일을 commit하기 전으로 돌아감
git push -f origin <branch_name> --> 강제로 푸쉬를 해야 에러가 안남.
명령을 실행하고 파일을 확인해보면 revert시킨 커밋의 변경사항이 폐지되었음을 확인할 수 있을 것임

*revert -->
*git log --oneline --> 커밋기록 불러오기
git revert 캐시값 --> 커밋을 revert 시킨다

git revert --no-commit HEAD~3.. --> 최근에 push한 3개의 커밋에 대해 revert를 해줌 이걸 사용하면 반드시 따로 커밋을 해주어야 한다.

## Quest
* GitHub에 가입한 뒤, [이 커리큘럼의 GitHub 저장소](https://github.com/KnowRe-Dev/WebDevCurriculum)의 우상단의 Fork 버튼을 눌러 자신의 저장소에 복사해 둡니다.
* Windows의 경우 같이 설치된 git shell을, MacOSX의 경우 터미널을 실행시켜 커맨드라인에 들어간 뒤, 명령어를 이용하여 복사한 저장소를 clone합니다.
  * 앞으로의 git 작업은 되도록 커맨드라인을 통해 하는 것을 권장합니다.
* 이 문서가 있는 폴더 바로 밑에 있는 sandbox 폴더에 파일을 추가한 후 커밋해 보기도 하고, 파일을 삭제해 보기도 하고, 수정해 보기도 하면서 각각의 단계에서 커밋했을 때 어떤 것들이 저장되는지를 확인합니다. ok
* `clone`/`add`/`commit`/`push`/`pull`/`branch`/`stash` 명령을 충분히 익혔다고 생각되면, 자신의 저장소에 이력을 push합니다. ok

## Advanced
* Mercurial은 어떤 형상관리 시스템일까요? 어떤 장점이 있을까요?
* 실리콘밸리의 테크 대기업들은 어떤 형상관리 시스템을 쓰고 있을까요?
