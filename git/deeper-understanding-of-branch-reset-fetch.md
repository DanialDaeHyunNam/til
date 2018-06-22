## Deeper understanding of branch, reset, fetch

브랜치를 나누는 것은 현재 버젼이 문제없다는 가정하에 유지보존한 상태로 다음 작업을 진행하는데 필요한 요소다. 새로 브랜치를 열고 작업을 시작한 후에 commit을 하고 checkout을 통해 origin으로 돌아가면 브랜치를 열어서 한 작업이 없던 시기로 돌아갈 수 있다는 점에서 그렇다.
<br>
오늘 작업을 하면서 팀원들과 Conflit되는 파일들이 존재했을 때, pull이 안되고, fetch 후에 diff를 통해서 확인하는 것까지는 했지만 더 진행하는 방법을 알아내는 것은 상당히 힘든일이었다. 그래서 조사해보며 알게된 점을 정리하자면
- pull이나 fetch를 시도한 후 실패한 경우엔 git status를 통해서 unmerged 파일 정보들을 확인할 수 있다. 그럼 고친 후에 다음 행동을 결정할 수 있다.
- fetch를 통해서 local storage에 올라온 파일들의 시점에 workspace를 동기화하는 방법은 아래와 같다.
```git
git reset --hard (remote)/(branch)
```
- 위의 명령을 실행한 후에는 우리가 되고자 결정한 remote repo의 모습을 workspace에서 확인할 수 있고, 바꾸고자 결정했다면 다시 아래와 같이 평소의 방법으로 remote환경을 변경하면된다.(이 경우는 remote repo가 여러개있는경우이기에 이런 일이 발생하는 것. 평소에는 발생하지않는 것이 맞을 것이다.)
```git
git status
git add (파일명)
```
<br>
또한 새롭게 배운 사실은 **HEAD** 의 의미는 지금 내가 바라보고 있는 branch(master도 당연히 브랜치 중 하나다.)를 의미한다. 즉, checkout을 할 때마다 HEAD의 위치는 변한다.

```
git -D (branch name) # 이 방법을 통해서 강제로 브랜치를 지울 수 있다.
```
아직 헷갈리는 부분들도 있지만, 더 작업하면서 생기는 문제에대한 해결법들은 다시 작성하도록 한다.
