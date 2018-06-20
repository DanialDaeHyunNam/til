## Git fetch and undo git fetch

Remote의 데이터를 받기전에 먼저 git fatch origin을 통해서 먼저 merge이전 단계를 진행할 수 있다. **(git pull origin master은 사실 git fetch 이후 git merge를 실행하는 것을 의미한다.)**

```
git fetch origin
```

그리고
```
git diff master origin/master
```
를 실행하여, 차이점을 미리 확인할 수 있다.

그 후에 문제가 없을 때,
```
git merge origin/master
```
를 실행한다.
<br>
아래에 참조한 링크에 의하면, 먼저 fetch 이후에 merge를 하는 것을 추천하고있다.
<br>

---

그럼 fetch한 것을 다시 날릴려면 어떡해야될까?<br>
일단 간단한 방법은.. 해당 remote를
```
git remote rm {해당remote에 대해 설정한 이름}
```
을 이용하여 날리고 다시 add하는 것을 할 수 있다. 다른 방법은 추후에 좀 더 살펴보도록 하자.. 일단은 이게 가장 쉬워 보인다.

## Reference
- [How to check the differences between local and github before the pull](https://stackoverflow.com/questions/6000919/how-to-check-the-differences-between-local-and-github-before-the-pull)
- [How to undo 'git fetch'](https://stackoverflow.com/questions/35591887/how-to-undo-git-fetch)
