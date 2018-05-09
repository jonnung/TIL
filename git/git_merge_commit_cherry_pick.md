# Git - Merge commit cherry-pick
## git cherry-pick?
체리-픽은 변경사항(changeset)의 비교 결과를 현재 브랜치에 적용하는 기능이다.   
여기서 비교 결과는 체리-픽 하고자 하는 워킹 트리의 한 지점과 그 지점의 부모와의 차이를 말하는 것이다.

만약 해당 커밋의 부모가 2개 이상이라면 어떤 부모 커밋과의 변경사항을 적용해야 할지 결정해야 한다.

이때 ```-m``` 옵션을 사용해서 부모를 지정할 수 있다. 이 숫자는 ```1```부터 시작한다.
이 숫자는 해당 merge commit의 revision 값으로 ```git show``` 했을때 나오는 revision 순서에 따라 ```1``` 그리고 ```2```가 된다.

```bash
$ git show e161219

commit e161219c3c89d4dffbd88665e5539395865dbdaf
Merge: 85f82de 3244247
Author: 조은우 <jonnung@gmail.com>
Date:   Tue Feb 13 17:04:50 2018 +0900

    Merge branch 'foo' into 'master'
```

## Command
```bash
$ git cherry-pick -m 1 e161219
```

