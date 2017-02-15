# git stash
(네이버) 사전에 stash 의 뜻을 찾아보면 "(안전한 곳에) 넣어두다" 라고 나오는데 git 을 사용하면서 정말 고마운 기능중에 하나이다.

## 주요 역할
수정한 파일만(modified)과 Staging Area (staged) 상태인 파일만 저장한다. 즉 tracked 상태인 파일만 해당되는 것이다.  
기본 적인 기능(추가, 보기, 제거)은 ``` git stash --help ```  에서 친절하고 자세한 설명을 볼 수 있다.

## 새로 알게된 특징들
- Stash한 파일을 다시 워킹 디렉토리에 적용할 때 과거 Staged 상태였던 파일을 자동으로 다시 Staged 상태로 만들어 주지는 않는다.
그래서 git stash apply 명령을 실행할 때 --index 옵션을 주면 Staged 상태까지 복원한다.
- branch 옵션을 함께 사용하면 새로운 브랜치를 만들고 stash 를 적용한다. 그리고 적용이 성공하면 해당 stash 는 제거 된다.

## 실무에서 유용할 팁
- 일부 파일을 제외하고 stash 하는 방법
  - ``` -p ``` 또는 ``` --patch ``` 옵션을 사용하면 hunk 단위로 확인하면서 stash 에 추가할지 결정할 수 있다.  
   hunk 는 변경된 사항들을 어느.. 범위 단위로 구분 짓는 식인데 ``` git add -p ``` 과 사용법이 동일하다.
```
$ git stash save -p "ISSUE-123 이차저차삼차까지 작업한 부분 "

# ... 이러쿵 저러쿵 나올테고~
# ... 아래와 같이 Interactive 모드로 표시됨

Stash this hunk [y,n,q,a,d,/,e,?]? y
```
- stash 들을 쉽게 구분하고 적용하는 방법
  - stash 를 사용하면서 가장 불편했던 부분중에 하나가 적용할 시점에서 stash 마다 어떤 상황/어떤 작업이였는지 알기가 어렵다는 것이다. (기억이 잘 안남)  
이때는 ``` save "[남기고 싶은 메시지]" ``` 를 남기면 된다. 그리고 ``` git stash list ``` 를 통해 해시값을 갖고 적용할 수 있다.  
```
$ git stash apply stash@{0}

# 또는

$ git stash pop stash@{1}
```