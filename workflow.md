# Work Flow
## project start

- 팀장은 repository를 생성하고 기본 설정을 한 후 배포한다.
- 팀원은 repository를 fork하여 복제한 로컬저장소를 만든다.<br><h6> ex) pdf_workflow 1.0</h6>
```
git clone git@github.com:[github id]/2020_soft_dev
```
<br>

## branch
### master branch
> 배포를 진행하며 직접적인 코드 수정을 하지 않는 branch (항상 유지)

<br>

\- release branch 또는 hotfix branch에서 배포가 가능하도록 작업을 완료한 후 master branch에 해당 branch를 병합 및 배포한다.
1. master branch에 branch를 병합한다.(merge 예제)
```
git:(master) git merge branch
```
2. github에 새로운 버전을 release한다.
<br> <h6> ex) pdf_workflow 2.0 / 2.4 / 3.0
```
git:(master) git tag *.*.*
git:(master) git push origin *.*.*
```
<br>

### develop branch
> 개발의 기반이 되는 branch (항상 유지)<br>
release를 위한 기능이 추가되고 버그가 수정되어 배포 가능한 상태라면 develop branch를 master branch에 병합한다.

<br>

\- 프로젝트를 시작할 때 곧바로 develop branch를 생성한다.
1. master branch에서 develop branch를 생성한다.
<br> <h6> ex) pdf_workflow 1.1
```
git:(master) git branch develop
```
2. develop branch로 이동한다.
```
git:(master) git checkout develop
```
<br>

### feature branch
> 새로운 기능 개발 및 버그 수정이 필요할 때, develop branch 또는 다른 feature branch에서 분기되는 branch (일시적)<br>
로컬저장소에서 관리하며, 개발이 완료되면 develop branch로 병합하여 다른 사람들과 공유한다.

<br>

\- 기능을 구현할 때, 상위 branch에서 분기한다.
1. 상위 branch에서 새로운 feature branch를 생성한다.<h6> ex) pdf_workflow 1.2 / 1.3 / 2.5 / 2.6 / 2.11 </h6>
  ```
  git:(prev_branch) git branch [new_feature_branch]
  ```
2. 새로운 feature branch로 이동한다.
```
git:(prev_branch) git checkout [new_feature_branch]
```
<br>

\- 작업이 완료된 branch는 상위 branch에 병합한다.
1. 상위 branch로 이동한다.
```
git:(new_feature_branch) git checkout prev_branch
```
2. 작업이 완료된 branch를 병합한다. (rebase 예제)
```
git:(prev_branch) git rebase [new_feature_branch]
```
<br>

\- 아래 example과 같이 branch C가 branch B보다 먼저 작업이 완료되어 branch A에 병합해야 하는 경우 rebase의 onto 옵션을 사용한다.
```
<example>
───A+───A2───A1─────────A3 (A)
   └────B1───B2 (B)     └───C1'───C2'(C`)
             └───C1───C2 (C)
```

1. rebase의 onto 옵션을 사용한다.<h6> ex) pdf_workflow 1.4</h6>

```
git rebase --onto branchA branchB branchC
```


<br>

\- 생성된 feature branch가 불필요한 경우, 해당 branch를 제거한다.
1. 다른 branch로 이동한다.
```
git:(new_feature_branch) git checkout other_branch
```
2. branch를 삭제한다.<h6> ex) pdf_workflow 2.7</h6>
```
git:(other_branch) git branch -d [new_feature_branch]
```

<br>

### release branch
> 설명

branch work flow 설명
<br><br>

### bugfix branch
> 설명

branch work flow 설명
<br><br>

### hotfix branch
> 설명

branch work flow 설명
<br><br>