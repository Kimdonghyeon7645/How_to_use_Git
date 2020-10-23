# PR 충돌 해결하기

충돌을 해결하는 법은 다양한 것 같다.

깃허브 웹에서 직접 pr에서 발생한 충돌을 수정할 수도 있고, 
로컬에서 pull을 받아서, 충돌나는 부분을 수정한 후 올릴 수도 있다. 

이 두가지 방법은 예전에 사용했던 방법이였으니, 이번에는 ```git rebase``` 를 이용해서 pr 충돌을 해결해보자.

## 설정

![image](https://user-images.githubusercontent.com/48408417/96844582-9ef79480-148a-11eb-82e2-3475c93946ec.png)

위와 같이 원본 저장소를 만들고, 이 저장소를 포크해 저장소를 복제했다.

![image](https://user-images.githubusercontent.com/48408417/96859765-d96a2d00-149c-11eb-9714-3a3162239037.png)

그런데 여기서 이렇게, 작성한 파일```hello.world```의 같은 부분을 각각 수정하고 커밋해 보면 어떨까?

![image-20201022193120219](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20201022193120219.png)

이렇게 되면, 한 파일```hello.world```에 대해서 버전1은 동일해도, 버전2는 서로 다른 버전을 가지게 된다.

그러면 여기서 파일 ```hello.world```의 버전2는 무엇이 될까?
답은 충돌이다.

![image](https://user-images.githubusercontent.com/48408417/96856945-69a67300-1499-11eb-832a-e9c8f0416931.png)

###### [이미지 출처](https://junwoo45.github.io/2019-10-23-rebase/)

위와 같이 원본 저장소를 포크하면, 서로 같은 버전을 공유하지만,

![image](https://user-images.githubusercontent.com/48408417/96857641-2c8eb080-149a-11eb-856d-ca5ee22e4a17.png)

요로코롬 원본 저장소랑, 포크 저장소랑 다른 버전2를 가지게 되면 문제가 발생한다.
그거 상관않고 pr를 날리겠다 하면은,

![image](https://user-images.githubusercontent.com/48408417/96857682-39ab9f80-149a-11eb-88f7-8609b30eeeed.png)

이렇게 문제나 풀어오라고 깃허브가 pr(포크 저장소의 내용을 원본 저장소에 합치는 요청, pull request)를 거절한다.

그러면  ```git pull upstream master``` 로 자동병합 시켜진 후에,
이중에서 자기가 원하는 버전을 선택해서 충돌을 해결할 수 있다.

> ```git pull upstream master``` 
> : 포크 저장소의 원격 저장소를 의미하는 origin 대신, 원본 저장소를 의미하는 upstream 에서 현재 master로 fetch(원본저장소의 diff 가져오기)및 자동 merge(병합)

하지만 병합은 merge말고도 rebase라는 방법이 있다.

원본 저장소에서 가져온 커밋들(=base)을 
갱신(=re) 해주는 명령어, ```rebase```를 사용하여 충돌을 해결해 보았다.

## rebase로 충돌 해결하기

![image](https://user-images.githubusercontent.com/48408417/96860551-d7549e00-149d-11eb-9e06-abceb1555a58.png)

우선 이렇게 원본저장소(fetch) 에서 fetch로 해서 diff 부분을 로컬로 가져와주자. ```git fetch upstream master```

![rebase28](https://junwoo45.github.io/img/rebase28.png)

그리고,

![image](https://user-images.githubusercontent.com/48408417/96861078-8c875600-149e-11eb-95d5-aaabe640e954.png)

fetch로 받아온 원본 저장소(upstream/master)를 현재 저장소와 rebase 한다. (--root 옵션으로 최초 커밋부터 rebase) ```git rebase -i --root``` 
그러면 위같이 충돌난 상황을 고치라고 뜰 것인데, 고쳐주자.
![image](https://user-images.githubusercontent.com/48408417/96862230-27ccfb00-14a0-11eb-94ed-57246aff945a.png)

참고로 여기선 굳이 여러 줄을 지워줄 필요없이 VSCode에서 지원하는 이부분에서 원하는 버전을 클릭하는 것만로 충돌을 해결해줄 수 있다.

![rebase29](https://junwoo45.github.io/img/rebase29.png)

![image](https://user-images.githubusercontent.com/48408417/96862428-68c50f80-14a0-11eb-82a1-57906041910a.png)

이렇게 충돌을 해결해주고, 

![rebase30](https://junwoo45.github.io/img/rebase30.png)

그러면 이렇게 해결이 된다.

![image](https://user-images.githubusercontent.com/48408417/96862795-ebe66580-14a0-11eb-93b5-4d599ec69255.png)

(여기서 나는 rebase --continue로 안넘기고 commit 했다;; 그리고 rebase --skip해서 이와 같은 화면이다.)

![image-20201022200857510](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20201022200857510.png)

(그럴 생각도 없었는데, 어쩌다 보니 reflog도 써보게 됬다. 
정말 너무 신세계였따...)



중간 과정에 딴길로 내가 샜지만, 결론적으로 

![image](https://user-images.githubusercontent.com/48408417/96864275-205b2100-14a3-11eb-873f-c17e32aca25f.png)

![image](https://user-images.githubusercontent.com/48408417/96864301-28b35c00-14a3-11eb-909e-a986fb971cd8.png)

충돌을 해결하고 병합에 성공했다! 

## 정리

병합에서 발생하는 충돌을 해결하는 방법은, 
병합을 ```merge``` 로 하냐, ```rebase``` 로 하냐에 따라서 2가지 방법으로서도 충돌을 해결할 수 있겠다.

둘중에 무엇을 쓸지는 자기 맘인데,

[git 브렌치 rebase 하기](https://git-scm.com/book/ko/v2/Git-브랜치-Rebase-하기) 등에서 두가지 방법의 차이점을 알 수 있을듯하다.

깔끔하게 정리할 수 있는 방법은 ```rebase```이라 생각하는데, 자세한 정보는 링크에서 발췌하면 아래와 같다.

```md
일반적인 해답을 굳이 드리자면 로컬 브랜치에서 작업할 때는 히스토리를 정리하기 위해서 Rebase 할 수도 있지만, 리모트 등 어딘가에 Push로 내보낸 커밋에 대해서는 절대 Rebase 하지 말아야 한다.
```

사실 그래서 rebase는 로컬 브렌치에서 히스토리 정리할 때 쓰는 걸로 하는게 좋을 것 같다.



## 참고

- [git rebase를 이해하기](https://junwoo45.github.io/2019-10-23-rebase/)

- [얄팍한 코딩사전 - git (하)](https://www.yalco.kr/26_git_tutorial_2/)