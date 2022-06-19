# GIT 명령어

## :computer: Git 구조

1.  **Working Directory(=Local)**: 내가 작헙하고 있는 실제 디렉토리
2. **Staging Area**: 커밋(commit)으로 남기고 싶은, 특정 버전으로 관리하고 싶은 파일이 있는 곳
3. **Repository**: 커밋(commit)들이 저장되는 곳

- 커밋은 위의 3가지 영역을 바탕으로 동작함.

## :raising_hand: Git - Github 연결(User)

- 한 번만 해도 되는 작업

- 꺾쇠는 실제로 적지 않음

  `git config --global user.name <username>` : username 등록

  `git config --global user.name` : username 확인

  `git config --global user.email <email>` : email 등록

  `git config --global user.email` : email 확인

## :file_folder: Git - Github 연결(Repository)

- Repository 연결할 때는 한 번만 해도 되는 작업

  `git init` : repositroy를 만들고 working directory랑 연결

  - repository를 만들 때마다 해줘야 함

  `git remote add origin <git repository url>` : repository 연결

- 파일을 수정, 생성, 삭제할 때마다 해야 하는 작업

  `git add .` : 모든 파일 staging area에 올리기

  `git add 파일명.확장자` : 특정 파일 staging area에 올리기

  - `git add 파일A.확장자 파일B.확장자 파일C. 확장자` 로 써서 여러 개를 올릴 수도 있음

  `git commit -m '<commit message>'` : github으로 밀어내기

  - 되도록 명령문으로 적되 동사형의 영어로 적기 
  
  `git pull` : github에서 로컬로 당겨오기

## :heavy_plus_sign: Git - merge

- 브랜치(Branch)란?

  독립적으로 어떤 작업을 진행하기 위한 개념

  필요에 의해 만들어지는 각각의 브랜치는 다른 브랜치의 영향을 받지 않기 때문에, 여러 작업을 동시에 진행할 수 있음.

  또한 이렇게 만들어진 브랜치는 다른 브랜치와 병합(Merge)함으로써, 작업한 내용을 다시 새로운 하나의 브랜치로 모을 수 있음.

- `git branch` : 브랜치의 종류와 함께 현재 어느 브랜치인지 확인

- `git branch <브랜치명>` : 새로운 브랜치를 생성

- `git branch -d <브랜치명>` : 브랜치를 삭제

- `git checkout <브랜치명>` : 해당 브랜치로 이동

- `git merge <브랜치명>`

  - 예) `future`라는 브랜치에서 `master`라는 브랜치로 merge하기 위해서는 `git merge master`를 해줘야 함

## :pushpin: 이외에 자주 사용하는 명령어들

- `git status` : Working directory에 어떤 변화가 있는지 알아보는 명령어
  - Working directory와 Staging area 단계의 변화

- `git log --oneline` : commit된 상황에서 어떤 메시지로 언제 무엇이 올라갔는지 알기 위한 명령어
- `git remote -v` : remotre가 잘 들어갔는지 확인
- `git push origin master` : 최종적으로 github에 등록
- `git add` : add를 잘했는지 확인
- `git commit` : commit을 잘했는지 확인
- `git clone <git repository url>` 
  - 말 그대로 복제일 뿐, 내가 수정한 것을 반영해달라고 요쳥할 권한이 없음
- `fork`
  - `pull request` : 내가 수정한 것을 반영해달라고 요청할 수 있음