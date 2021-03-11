# SourceTree
[Git] Merge 이해하기 (Merge / Squash and Merge / Rebase and Merge)

회사에서 Git을 사용해서 형상 관리를 하고 있다. 그 동안 내가 개인 repository branch에 commit, push등을 해본 적은 많지만 다른 사람과 협업을 하면서 branch를 생성하고 master에 merge를 해본 적은 없어서 처음에 매우 당황했었다. 그래서 오늘은 많이 비교가 되는 merge와 rebase에 대해서 알아보려고 한다!

먼저 Merge와 Rebase는 다음과 같은 상황에서 사용된다.

여러 명이 공동으로 작업하는 repository를 clone 받아 작업을 한다고 생각해보자. master라는 공동의 브랜치가 존재하고 나는 my-branch라는 이름의 브랜치를 만들어서 코드 작업을 한다.

- $ git checkout -b my-branch

위 명령어는 아래 명령어를 한 줄로 축약한 것이다.

- $ git branch my-branch
- $ git checkout my-branch

작업을 다 끝내고 master 브랜치에 merge를 하려고 했는데, 내가 merge하기 전에 누군가가 master 브랜치에 다른 작업을 한 후 commit하고 push했다. 그렇다면 이런 모양이 될 것이다.

이 경우에 my-branch를 master에 병합하는 방법에는 다음과 같은 것들이 있다.


## Merge
하나의 브랜치와 다른 브랜치의 변경 이력 전체를 합치는 방법이다.
commit a, b, c를 refer하는 m이 생성되고 m을 통해 a + b + c가 master에 추가된다.
m은 2개의 parent를 가진다.

- $ git checkout master
- $ git merge develop
- $ git branch -D develop


## Squash and Merge
commit a + b + c를 합쳐서 새로운 commit, abc를 만들어지고 master에 추가된다.
abc는 1개의 parent를 가진다.
feature 브랜치의 commit history를 합쳐서 깔끔하게 만들기 위해 사용한다.

- $ git checkout master
- $ git merge --squash develop
- $ git commit -m "squash develop"
- $ git branch -D develop


## Rebase and Merge
모든 commit들이 합쳐지지 않고 각각 master 브랜치에 추가된다.
각 commit은 모두 하나의 parent를 가진다.

- $ git checkout develop
- $ git rebase master
- $ git checkout master
- $ git merge develop
- $ git pull develop
- $ git branch -D develop

Merge는 Merge commit 기록이 추가로 남게 되지만 Rebase의 경우에는 branch 병합 시 Merge commit 기록이 남지 않는다. 따라서 마치 하나의 브랜치에서 작업한 것처럼 보여진다.


## Reference
- https://meetup.toast.com/posts/122
- https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-request-merges
- https://velog.io/@godori/Git-Rebase


출처: https://im-developer.tistory.com/182 [Code Playground]