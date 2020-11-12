# git 명령어 생존용 키트 - 1

##1. 로컬 저장소 만들기, git에 계정 설정 : init, config
- ### git init 
    현재 폴더를 깃이 관리하는 프로젝트 디렉토리(=working directory)로 설정
    -> 그 안에 저장소(.git 폴더) 생성
- ### git config user.name, git config user.email
    ```commandline
    git comfig user.name 'my_name'
    git config user.email 'my_email@ppap.kr'
    ```
    사용자의 아이디와 이메일을 설정 (커밋할 때 필요함) 
    
##2. 스테이징 영역에 올리기 : add
- **git add** : 수정사항이 있는 특정 파일을 **staging area(스테이징 영역)** 에 올리기
```commandline
git add [파일명]          # 해당 파일
git add [디렉토리명]      # 해당 디렉토리 내의 모든 파일
git add .                # (해당 working directory 내의) 모든 파일
```

##3. 스테이징 영역에서 내리기 : reset
- **git reset** : **staging area(스테이징 영역)** 에 올렸던 파일을 다시 내리기
```commandline
git reset [파일명]
```

##4. 프로젝트 관련 상태 보기 : status
- **git status** : 깃이 현재 인식하는 프로젝트 관련 내용들 출력
    스테이징 영역 상태도 볼 수 있음, 프로젝트에 문제가 생겼을 때 이 명령어 활용

##5. 스테이징 영역 -> 저장소 영역으로 올리기 : commit
- **git commit -m "커밋 메시지"** : 현재 **staging area(스테이징 영역)** 의 내역을 커밋으로 저장소에 올리기

##6. 도움! : help
- **git help [커맨드 이름]** : 사용법이 궁금한 깃 명령어의 공식 메뉴얼 내용 출력
