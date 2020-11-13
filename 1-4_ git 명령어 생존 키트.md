# git 명령어 생존용 키트

: 깃 사용할때, 딴건 몰라도 이건 꼭 필요한 **생존용 필수 명령어들 10개** (깃이 처음이라면 아래 명령어들만 익히고 천천히 깃과 친해지도록 합시다!)

## 1. 로컬 저장소 만들기, git에 계정 설정 : init, config
- ### git init 
    현재 폴더를 깃이 관리하는 프로젝트 디렉토리(=working directory)로 설정
    -> 그 안에 저장소(.git 폴더) 생성
- ### git config user.name, git config user.email
    ```commandline
    git comfig user.name 'my_name'
    git config user.email 'my_email@ppap.kr'
    ```
    사용자의 아이디와 이메일을 설정 (커밋할 때 필요함) 
    
## 2. 워킹 디렉토리 -> 스테이징 영역 올리기 : add
**git add** : 수정사항이 있는 특정 파일을 **staging area(스테이징 영역)** 에 올리기
```commandline
git add [파일명]          # 해당 파일
git add [디렉토리명]      # 해당 디렉토리 내의 모든 파일
git add .                # (해당 working directory 내의) 모든 파일
```

## 3. 스테이징 영역 -> 워킹 디렉토리 내리기 : reset
**git reset** : **staging area(스테이징 영역)** 에 올렸던 파일을 다시 내리기
```commandline
git reset [파일명]
```

## 4. 프로젝트 관련 상태 보기 : status
**git status** : 깃이 현재 인식하는 프로젝트 관련 내용들 출력
    스테이징 영역 상태도 볼 수 있음, 프로젝트에 문제가 생겼을 때 이 명령어 활용

## 5. 스테이징 영역 -> 저장소 올리기 : commit
**git commit -m "커밋 메시지"** : 현재 **staging area(스테이징 영역)** 의 내역을 커밋으로 저장소에 올리기

## 6. 로컬 저장소 -> 원격 저장소 보내기 : push
- **git push -u origin master** : 로컬 저장소 내용을 **처음으로** 원격 저장소에 올리기  
    **-u** 옵션 : **--set-upstream** 약자로, 이 옵션을 주면 push 보내는 곳(브렌치)를 tracking(추적)하도록 연결
    -> 추적 연결이 된 상태라면 다움부터 ```git push``` 만 해도 알아서 연결된 곳(브렌치)으로 내용이 보내진다  
    
- **git push** : 로컬 저장소 내용을 원격 저장소에 올리기 

## 7. 로컬 저장소 <- 원격 저장소 가져오기 : pull 
**git pull** : 원격 저장소의 내용을 로컬 저장소로 가져오기

## 8. 원격 저장소 -> 가져와서 로컬 저장소로 생성하기 : clone
**git clone [원격 저장소 주소]** : 원격 저장소 주소(GitHub 주소)를 가져와서 내 로컬 저장소로 생성하기

## 9. 도움! : help
- **git help [커맨드 이름]** : 사용법이 궁금한 깃 명령어의 공식 메뉴얼 내용 출력
