# git cheat sheet


<br>

## 1. 설정

#### (1) 터미널에서 계정등록하기
```
$ git config --global user.name "USER-NAME" 
$ git config --global user.email "USER-EMAIL" 
$ git config --global color.ui auto
$ git config --list
```

<br>

#### (2) ssh 키 등록하기
```
$ ssh-keygen -t rsa -C "USER-EMAIL"
(패스워드 입력) 
(.ssh폴더가 생성됨) 
$ pbcopy < ~/.ssh/id_rsa.pub // 내용복사 
(깃허브 설정페이지 New SSH Key 에 들어가서, 복사한 .ssh/id_rsa.pub 내용 붙여넣기)
$ ssh -T git@github.com 
yes // 정상적으로 등록됨
```

<br>

#### (3) known_hosts에 연결내용 입력
```
ssh-keyscan github.com >> ~/.ssh/known_hosts
```

<br>

## 2. 기본사용

```
$ echo "# PROJECT-NAME" >> README.md
$ git init
$ git add README.md
$ git commit -m "first commit"
$ git branch -M main
$ git remote add origin git@github.com:kimniki/PROJECT-NAME.git
$ git push -u origin main
```

<br>

#### (1) add 옵션
```
$ git add -u    // deleted 적용
```

<br>

#### (2) commit 옵션
```
$ git commit -m "README파일 생성" 
$ git commit --amend  // 커밋메시지 변경 
$ git commit -am "메시지"  // add + commit
````

<br>

#### (3) push 옵션
```
$ git push -u origin master  // master브랜치의 수정내용을 업로드함
$ git push -u origin 브랜치명 
$ git push origin 태그명
```

<br>

## 3. 되돌리기

#### (1) add 취소
```
$ git reset HEAD  // 이전 git add 취소
```

<br>

#### (2) commit 취소
```
$ git reset --hard HEAD^  // 이전 git commit 취소
$ git push origin master --force 
```
```
$ git reset --hard a5cfa34 돌아가려는주소 
$ git push -f origin master 
```

<br>

#### (3) commit 합치기
```
$ git rebase -i HEAD~2  // 최신순 커밋 2개 뭉치기
```

<br>

#### (4) merge 취소
```
$ git reset --merge "0e51bf95e0c495490321d40bf43078a72eb60314"  // 병합취소  
$ git push origin master --force
```

<br>

## 4. 브랜치

#### (1) branch 만들기
```
$ git branch branch1   // branch1 브랜치 만들기
```

<br> 

#### (2) branch 전환하기
```
$ git checkout branch1  // branch1 브랜치로 이동하기
$ git checkout 브랜치명  // 브랜치이동 
$ git checkout -  // 이전 브랜치로 이동 
$ git checkout -b 브랜치명  // 브랜치 만들고 이동 
$ git checkout -b 브랜치명 origin/브랜치명  // 원격브랜치 기반 브랜치 작성
```

<br> 

#### (3) branch push 
```
$ git push origin branch1  // branch1브랜치의 수정내용을 업로드함
```

<br>

#### (4) merge request & 승인
```
$ git checkout master
$ git merge branch1
$ git merge --no-ff 브랜치명  // 현재브런치와 이 브런치 병합
(github에서 merge request & 승인)
```

<br>

#### (5) branch 정보
```
$ git branch   // 현재브랜치 보기
$ git branch -r  // 현재저장소의 브랜치목록 보기
$ git branch -a  // 원격 브랜치까지 보기
```

<br>

#### (6) branch 삭제
```
$ git branch -d (branch 이름)
```

<br>

## 5. 태그 

``` 
$ git add FILE 
$ git commit -m "MESSAGE" 
$ git tag -a TAG-NAME -m "MESSAGE" 
$ git push origin master && git push origin TAG-NAME 
```

```
$ git tag 태그명  // 현재 태그로 만들기 
$ git add * 
$ git commit -m "register with passwd hash" 
$ git tag -a v0.1-register -m "register with passwd hash" 
$ git push origin master && git push origin v0.1-register
```

<br>

## 6. 로그

#### (1) 상태확인
```
$ git log   // 이력보기
$ git log 파일명 
$ git log -p  // 변경된 내용도 출력 
$ git log --graph 
$ git reflog  // 현재브랜치뿐만 아니라 저장소전체 로그 
$ git log 
$ git show 4457926b690e892f7962bbc5a334bbdba038vgf  // 커밋번호 $ git log 로 확인
$ git log --oneline --graph  // 이력 그래프로 보기
```

<br>

#### (2) 변경내용 확인
```
$ git diff  // add 안된 내용 확인 
$ git diff HEAD // 변경내용 확인
```

<br>

## 7. etc. 

#### (1) 기존 프로젝트에 gitignore 적용하기
```
$ git rm -r --cached .
$ git add .
$ git commit -m ".gitignore is now working"
```

<br>

#### (2) 대용량 업로드
```
$ git lfs install 
$ cd ~/MY-FOLDER
$ git lfs track "*"
// 이 방법으로 업로드하면 깃허브에서 코드내용을 확인할 수 없음
```

<br>

#### (3) 사용언어 통계에서 제외시키기
```
// .gitattributes 추가
*.css linguist-detectable=false
```

<br>

#### (4) 이미지업로드
1. Issues / New issue 버튼 클릭 
2. 작성란에 이미지를 드래그해서 주소얻기
3. 주소를 복사해서 README.md 파일에서 사용함

![2019-10-25_01_59_31](https://user-images.githubusercontent.com/54002032/142811013-9d754a36-fdef-4426-b9dc-ae28bcd4774f.png)
