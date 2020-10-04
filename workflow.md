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
> 배포를 위한 최종적인 버그 수정, 문서 추가 등 release와 직접적으로 관련된 작업을 진행하는 branch (일시적)<br>
작업 완료 후 master branch에 병합하며, 배포 후 develop branch에도 병합한다.
<br>

\- 배포를 위해, develop branch에서 release branch를 생성한다.
1. develop branch로 이동한다.
```
git:(branch) git checkout develop
```
2. release branch를 생성하고 이동한다.<h6> ex) pdf_workflow 1.7</h6>
```
git:(develop) git checkout -b release
```
<br>

\- release branch에서 배포가 가능한 상태가 되었을 경우
1. master branch로 이동한다.
```
git:(release) git checkout master
```
2. master branch에 release branch를 병합한다.<h6> ex) pdf_workflow 1.12</h6>
```
git:(master) git merge release
```
3. master branch에서 github에 새로운 버전을 release한다.<h6> ex) pdf_workflow 2.0</h6>
4. develop branch에 필요한 내용을 병합한다.
```
방법1 : 특정한 파일만 병합하는 경우
git:(master) git checkout release
git:(release) git checkout -p develop [특정파일]

방법2 : 특정한 파일만 제외하고 병합하는 경우
git:(master) git checkout develop
git:(develop) git merge --no-commit --no-ff release -X theirs
git:(develop) git reset HEAD [제외할 파일]
git:(develop) git clean -fd
git:(develop) git commit -m "message"
```

\- 작업이 완료되거나, 필요없어진 경우 branch를 제거한다.
1. 다른 branch로 이동한다.
```
git:(release) git checkout branch
```
2. release branch를 삭제한다.<h6> ex) pdf_workflow 2.10</h6>
```
git:(branch) git branch -d release
```
<br>

### bugfix branch
> release branch에서 발생한 버그를 바로 수정하는 branch(일시적)
<br>

\- release branch에서 버그를 발견했을 경우 bugfix branch를 생성한다.
1. bugfix branch를 생성하고 이동한다.<h6> ex) pdf_workflow 1.9</h6>
```
git:(release) git checkout -b bugfix
```
<br>

\- 작업이 완료되면 release branch에 bugfix branch를 병합한다.
1. release branch로 이동한다.
```
git:(bugfix) git checkout release
```
2. release branch에 bugfix branch를 병합한다.<h6> ex) pdf_workflow 1.11</h6>
```
git:(release) git merge bugfix
```
3. develop branch에 필요한 내용을 병합한다.<h6> ex) pdf_workflow 1.11</h6>
```
방법1 : 특정한 파일만 병합하는 경우
git:(release) git checkout bugfix
git:(bugfix) git checkout -p develop [특정파일]

방법2 : 특정한 파일만 제외하고 병합하는 경우
git:(master) git checkout develop
git:(develop) git merge --no-commit --no-ff bugfix -X theirs
git:(develop) git reset HEAD [제외할 파일]
git:(develop) git clean -fd
git:(develop) git commit -m "message"
```
<br>

\- 작업이 완료되거나, 필요없어진 경우 branch를 제거한다.
1. 다른 branch로 이동한다.
```
git:(bugfix) git checkout branch
```
2. bugfix branch를 삭제한다.
```
git:(branch) git branch -d bugfix
```
<br>

### hotfix branch
> 배포된 버전에서 발생한 버그를 수정 하는 branch(일시적)<br>
배포한 버전에 긴급하게 수정을 해야 할 필요가 있을 경우, master branch에서 분기하는 branch이다.


<br>

\- 배포한 버전에서 버그가 발생했을 때, master branch에서 hotfix branch를 생성한다.
1. master branch로 이동한다.
```
git:(branch) git checkout master
```
2. hotfix branch를 생성하고 이동한다.<h6> ex) pdf_workflow 2.2</h6>
```
git:(master) git checkout -b hotfix
```
<br>

\- 작업이 완료되면 master branch에 병합한다.
1. master branch로 이동한다.
```
git:(hotfix) git checkout master
```
2. master branch에 hotfix branch를 병합한다.<h6> ex) pdf_workflow 2.3</h6>
```
git:(master) git merge hotfix
```
3. master branch에서 github에 새로운 버전을 release한다.<h6> ex) pdf_workflow 2.4</h6>
4. develop branch에 필요한 내용을 병합한다.
```
방법1 : 특정한 파일만 병합하는 경우
git:(master) git checkout hotfix
git:(hotfix) git checkout -p develop [특정파일]

방법2 : 특정한 파일만 제외하고 병합하는 경우
git:(master) git checkout develop
git:(develop) git merge --no-commit --no-ff hotfix -X theirs
git:(develop) git reset HEAD [제외할 파일]
git:(develop) git clean -fd
git:(develop) git commit -m "message"
```
<br>

\- 작업이 완료되거나, 필요없어진 경우 branch를 제거한다.
1. 다른 branch로 이동한다.
```
git:(hotfix) git checkout branch
```
2. hotfix branch를 삭제한다.
```
git:(branch) git branch -d hotfix
```