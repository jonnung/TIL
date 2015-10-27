# git revert
릴리즈 항목에서 제외 시키기 위해서 이미 push 된 merge commit 을 되돌려야 한다면?  

```
git revert -m 1 <merge-commit>
```
'-m 1' 옵션은 merge commit 의 바로 전 커밋으로 revert 한다.   


