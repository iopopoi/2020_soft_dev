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
> 설명

branch work flow 설명
<br><br>

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