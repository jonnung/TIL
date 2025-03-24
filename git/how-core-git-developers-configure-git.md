# Git 코어 개발자는 Git을 어떻게 설정하고 사용할까?

> 원문: [How Core Git Developers Configure Git](https://blog.gitbutler.com/how-git-core-devs-configure-git/)

## 1. 브랜치 관리 및 표시 설정

### 브랜치 표시 및 정렬
```bash
git config --global column.ui auto
git config --global branch.sort -committerdate
```
- **`column.ui auto`**: Git 출력을 자동으로 컬럼 형식으로 정돈하여 표시
- **`branch.sort -committerdate`**: 브랜치 목록을 마지막 커밋 날짜를 기준으로 내림차순(최신순) 정렬
- **변화**: 
  - 브랜치 목록이 알파벳순이 아닌 최신 활동순으로 정렬됨
  - 여러 브랜치가 화면 너비에 맞게 여러 컬럼으로 깔끔하게 표시됨
  - 활성/비활성 브랜치 구분이 용이해짐

## 2. Diff 및 변경사항 표시 개선

### 차이점 표시 알고리즘 및 스타일
```bash
git config --global diff.algorithm histogram
git config --global diff.colorMoved plain
git config --global diff.mnemonicPrefix true
git config --global diff.renames true
git config --global merge.conflictstyle zdiff3
```
- **`diff.algorithm histogram`**: 더 정확한 차이점 계산을 위해 histogram 알고리즘 사용
- **`diff.colorMoved plain`**: 이동된 코드 블록을 색상으로 구분하여 표시
- **`diff.mnemonicPrefix true`**: a/, b/ 대신 의미있는 접두사(c/, i/, w/)로 컨텍스트 표시
- **`diff.renames true`**: 파일 이름 변경을 자동으로 감지하고 표시
- **`merge.conflictstyle zdiff3`**: 더 정확한 충돌 표시와 최소화된 충돌 범위 제공
- **변화**:
  - 대규모 리팩토링에서 더 논리적인 diff 출력
  - 이동된 코드를 추가/삭제가 아닌 '이동됨'으로 정확히 표시
  - 비교 컨텍스트(커밋 간, 작업 디렉토리, 인덱스)를 명확히 구분
  - 파일 이름 변경이 명확하게 표시됨
  - 충돌 해결이 더 쉬워짐

## 3. Push 동작 최적화

### 원격 저장소 푸시 설정
```bash
git config --global push.default simple
git config --global push.autoSetupRemote true
git config --global push.followTags true
```
- **`push.default simple`**: 현재 브랜치를 동일한 이름의 원격 브랜치로만 푸시
- **`push.autoSetupRemote true`**: 원격 브랜치가 없을 때 자동으로 생성하고 추적 관계 설정
- **`push.followTags true`**: 커밋 푸시 시 해당 커밋을 가리키는 태그도 함께 푸시
- **변화**:
  - 잘못된 브랜치에 푸시하는 실수 방지
  - 새 브랜치 첫 푸시 시 `-u origin branch-name` 옵션 불필요
  - 태그를 따로 푸시할 필요 없이 자동으로 함께 푸시됨

## 4. Fetch 동작 최적화

### 원격 저장소 동기화 설정
```bash
git config --global fetch.prune true
git config --global fetch.pruneTags true
git config --global fetch.all true
```
- **`fetch.prune true`**: 원격에서 삭제된 브랜치를 로컬 참조에서도 자동으로 제거
- **`fetch.pruneTags true`**: 원격에서 삭제된 태그를 로컬에서도 자동으로 제거
- **`fetch.all true`**: 모든 원격 저장소에서 데이터를 가져오도록 설정
- **변화**:
  - 로컬 저장소의 브랜치와 태그 참조가 원격과 자동 동기화됨
  - 여러 원격 저장소가 설정된 경우 한 번에 모든 원격 데이터 업데이트
  - `git branch -a`와 `git tag -l` 목록이 더 깔끔하게 유지됨

## 5. 리베이스 및 병합 워크플로우 개선

### 리베이스 자동화 설정
```bash
git config --global rebase.autoSquash true
git config --global rebase.autoStash true
git config --global rebase.updateRefs true
git config --global pull.rebase true
```
- **`rebase.autoSquash true`**: fixup/squash 커밋을 자동으로 원본 커밋에 통합
- **`rebase.autoStash true`**: 리베이스 전 변경사항 자동 스태시 및 복원
- **`rebase.updateRefs true`**: 리베이스 중 관련 참조도 함께 업데이트
- **`pull.rebase true`**: pull 시 병합 대신 리베이스 사용
- **변화**:
  - 수정 커밋 관리가 간소화됨
  - 커밋되지 않은 변경사항이 있어도 리베이스 가능
  - 복잡한 브랜치 구조에서도 안정적인 리베이스
  - 깔끔한 선형 커밋 히스토리 유지

### 병합 충돌 처리 개선
```bash
git config --global rerere.enabled true
git config --global rerere.autoupdate true
```
- **`rerere.enabled true`**: 해결한 충돌 패턴을 기억하여 재사용
- **`rerere.autoupdate true`**: 자동 적용된 충돌 해결책을 자동으로 스테이징
- **변화**:
  - 반복되는 같은 충돌 패턴을 한 번만 해결하면 됨
  - 자동 해결된 파일을 수동으로 add할 필요가 없음

## 6. 성능 최적화

### 캐시 및 모니터링 설정
```bash
git config --global core.fsmonitor true
git config --global core.untrackedCache true
```
- **`core.fsmonitor true`**: 파일 시스템 모니터링으로 명령 실행 속도 향상
- **`core.untrackedCache true`**: 추적되지 않은 파일 정보를 캐시하여 성능 향상
- **변화**:
  - 대규모 저장소에서 git status, add, commit 등의 명령이 훨씬 빠르게 실행됨
  - 추적되지 않은 파일이 많은 저장소에서 특히 성능 향상을 체감

## 7. 사용자 편의성 향상

### 사용자 경험 개선 설정
```bash
git config --global help.autocorrect prompt
git config --global core.excludesfile ~/.gitignore
```
- **`help.autocorrect prompt`**: 잘못된 Git 명령어 입력 시 자동 수정 제안
- **`core.excludesfile ~/.gitignore`**: 글로벌 .gitignore 파일 위치 설정
- **변화**:
  - 오타가 있는 명령어를 입력했을 때 자동 수정 옵션 제공
  - 모든 프로젝트에서 공통으로 무시할 파일 패턴을 한 번만 설정 가능


## My Git Config
```
[init]
  defaultBranch = main

[includeIf "gitdir/i:~/Source/"]
	path = ~/Source/.gitconfig

[includeIf "gitdir/i:~/Work/"]
	path = ~/Work/.gitconfig

[column]
	ui = auto

[branch]
	sort = -committerdate

[tag]
	sort = -version:refname

[diff]
	algorithm = histogram
	colorMoved = plain
	mnemonicPrefix = true
	renames = true

[push]
	autoSetupRemote = true
	followTags = true

[fetch]
	prune = true
	pruneTags = true
	all = true

[help]
	autocorrect = prompt

[rerere]
	enabled = true
	autoupdate = true

[core]
	excludesfile = /Users/ewcho/.gitignore
	fsmonitor = true
	untrackedCache = true

[rebase]
	autoSquash = true
	autoStash = true
	updateRefs = true

[merge]
	conflictstyle = zdiff3

[pull]
	rebase = true
```
