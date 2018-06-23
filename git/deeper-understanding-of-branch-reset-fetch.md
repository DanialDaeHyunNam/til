## Deeper understanding of branch, reset, fetch

브랜치를 나누는 것은 현재 버젼이 문제없다는 가정하에 유지보존한 상태로 다음 작업을 진행하는데 필요한 요소다. 새로 브랜치를 열고 작업을 시작한 후에 commit을 하고 checkout을 통해 origin으로 돌아가면 브랜치를 열어서 한 작업이 없던 시기로 돌아갈 수 있다는 점에서 그렇다.
<br>
오늘 작업을 하면서 팀원들과 **Conflit** 되는 파일들이 존재했을 때, pull이 안되고, fetch 후에 diff를 통해서 확인하는 것까지는 했지만 더 진행하는 방법을 알아내는 것은 상당히 힘든일이었다. 그래서 조사해보며 알게된 점을 정리하자면
- local에서만 바라볼 때, git은 총 세가지 단계가있다. **Working Directory(이후 WD), index, HEAD** 이다. WD는 현재 작업하는 사람이 보고 있는 현재 상황이며, index는 WD에서 최근 커밋에서 변경된 사항 중에 원하는 것들을 add한 경우에 갱신되는 공간이다. **HEAD** 는 **add** 된 수정된 사항을 **commit** 하고 나면 변경되며, 그 전까지는 가장 최근 **commit** 상태를 가리키고있다.
- git reset에는 세가지 방법이 있는데,
  + 첫 번째는 **git reset --soft HEAD~** 이다. 이 명령은 HEAD를 다시 최근 커밋상태를 바라보게한다. 즉 가장 최근에 **commit** 한 내용을 내리는 것을 의미한다.
  + 두 번째는 **git reset [--mixied] HEAD~** 이 명령은 중앙의 옵션은 default로 들어가므로 **git reset HEAD** 와 같은 의미이며, **git reset HEAD** 를 하면 최근에 올린 모든 파일을 **index** 에서 내릴 수 있고, 특정 파일만 내리고 싶은 경우에는 뒤에 파일명을 붙이면 된다.
  + 세 번째는 **git reset --hard HEAD** 이다. 이 경우에는 가장 최근 커밋 상태(HEAD가 가르키고 있는 커밋 상태)로 **HEAD, index, WD** 를 다 되돌린다. 이 경우는 WD를 다시 수정한 상태(reset 명령을 내려서 다시 최근 커밋 상태로 되돌리기 전 상태)를 만들려면 reflog를 사용해야된다고 하는데, 아직 그 방법까지는 잘 모르겠다. **포인트** 는 위험하다. WD의 수정한 부분을 수정전(정확히는 최근 커밋상태)으로 되돌리기 때문이다.
- pull이나 fetch를 시도한 후 실패한 경우엔 **git status** 를 통해서 unmerged 파일 정보들을 확인할 수 있다. 그럼 고친 후에 다음 행동을 결정할 수 있다.
```git
git reset --hard (remote)/(branch)
```
- 위의 명령을 실행하게되면 위에서 알아보았듯 우리의 remote/branch의 커밋 시점으로 현재 로컬의 HEAD, index, WD를 다 변경시킨다.
```git
git status
git add (파일명)
```
- 어쨋든 자신이 원하는 모양이 remote상의 모 branch의 가장 최근 커밋 상태라면 그 방향으로 **git reset --hard remote/origin** 을 실행하여 **HEAD, index, WD** 까지 다 갱신시키면 된다.
<br>
**reset vs checkout**
Checkout과 reset의 차이는 상당히 헷갈린다.
- checkout은 HEAD가 가리키는 commit pointer를 옮긴다. 하지만 옮기기 이전 branch는 여전히 독립적으로 존재하므로 다시 checkout을 하면 HEAD까지 다 정보를 변경시켜주므로 안전하다.
- 하지만 reset은 branch가 커밋한 정보를 날리고 전부 옮긴 방향으로 갱신한다.

```
git -D (branch name) # 이 방법을 통해서 강제로 브랜치를 지울 수 있다.
```
||HEAD|index|WD|WD Safe?|
|:-:|:-:|:-:|:-:|:-:|
|**reset --soft [commit]**|Ref|No|No|Yes|
|**reset [commit]**|Ref|Yes|No|Yes|
|**reset --hard [commit]**|Ref|Yes|Yes|**No**|
|**checkout [commit]**   |HEAD|Yes|Yes|Yes|
|**reset (commit) [file]**|No|Yes|No|Yes|
|**checkout (commit) [file]**|Ref|Yes|Yes|**No**|

HEAD가 가리키는 브랜치를 움직인다면 "Ref", HEAD자체가 움직인다면 "HEAD"라고 표기했다. WD Safe? 열이 중요하다. No라고 적혀있으면 안전하지 않다는 뜻이다.
<br>
더 자세한 글은 아래 링크에서 확인!
<br>
## Reference
[What does "git reset" do?](https://git-scm.com/book/ko/v2/Git-도구-Reset-명확히-알고-가기)
