# git add
git add는 아래 2가지 역할을 한다.
- 새로운 파일을 추가
- 변경된 파일을 스테이징 영역으로 추가

## -i --interactive
- 대화형 모드
- 파일 단위, 파일의 일부분(Hunk)별로 선택적으로 커밋 가능
```
git add -i

*** Commands ***
  1: status   2: update   3: revert   4: add untracked
  5: patch    6: diff     7: quit     8: help
What now>
```
- 1: status
  - 처음 시작할때와 동일한 상태 정보를 보여줌
- 2: update
  - 파일을 스테이징에 추가
- 3: revert
  - 스테이징한 변경 사항을 취소
- 4: add untracted
  - 아직 추적되고 있지 않은 파일을 스테이징에 추가
- 5: patch
  - 패치모드
  - 파일을 하나 이상 선택할 수 있음
  - 변경된 파일간의 차이를 표시
  - 해당 변경 사항들(hunk)마다 추가 여부를 묻는 옵션 표시
  - 연속된 변경사항은 하나의 hunk로 취급
  - 파일 안에서 차이가 있는 각 영역이 하나의 hunk가 됨
  - y: 변경사항 스테이징, n: 건너뜀, a: 파일에 있는 모든 hunk를 추가, d: 파일에 있는 모든 hunk를 무시, ?: 도움말
  - git add -p로 바로 실행 가능 (diff 까지 해줌)
  

> git diff 해서 변경한 코드를 확인하고 git add "파일명" 해서 commit 할 파일들을 stage에 올렸는데 앞으로는 add -p 를 쓰면 좋을 것 같다.
