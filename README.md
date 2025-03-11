## Submodule 만들기

`submodule` 을 추가할 `main repository` 를 생성하고 그 폴더 내에서 `submodule`  추가

<img width="959" alt="스크린샷 2025-03-11 오전 10 22 26" src="https://github.com/user-attachments/assets/6a7d654c-9627-41fe-82b9-9e7ea42a906e" />
<br/><br/>

```bash
$ git submodule add <remote repository>

# test 를 위한 command
$ git submodule add https://github.com/jiohjung98/npm-producer.git
$ git submodule add https://github.com/jiohjung98/npm-consumer.git
```
<br/><br/>
`git submodule add` 명령어를 통해 `main repository` 에 `submodule` 을 쉽게 추가할 수 있다.

<img width="959" alt="스크린샷 2025-03-11 오전 10 25 16" src="https://github.com/user-attachments/assets/030aa937-a0a1-4781-a833-b44f80b4f94b" />


그럼 다음과 같이 새로운 파일이 세 개의 파일이 생성됨을 알 수 있다. 

한 가지 살펴볼 점은 `submodule add` 를 통해 clone 된 `submodules` 는 `directory` 임에도 하나의 `file` 로 취급(일반적인 `file` 과는 속성 자체가 다르지만)되며, `submodule` 내의 `files` 는 `track` 하지 않는다.

또한 `submodule` 의 정보를 가지는 `.gitmodules` 라는 파일이 생성된다.

<br/><br/>

<img width="957" alt="스크린샷 2025-03-11 오전 10 32 05" src="https://github.com/user-attachments/assets/0b7ab7db-d8de-4227-a2b6-43540b684b30" />

```bash
$ git add .
$ git commit -m "commit message"
$ git push
```

 `main project` 의 변동사항을 `commit` 하면 된다.

 <br/><br/>

<img width="920" alt="스크린샷 2025-03-11 오전 10 36 49" src="https://github.com/user-attachments/assets/34f7caae-deaa-4c13-83ee-15aeae72cddb" />

`github` 에서 `submodule` 을 추가한 main repo 를 확인하면, 일반적인 directory 와 달리 화살표가 박혀있는 `directory` 로 표시되며, `submodule` 의 실제 repository 를 `hyperlink` 한다.

`@ (at sign)` 뒤의 정보는 각 `submodule` 의 `latest commit` 을 의미한다.

<br/><br/><br/><br/>

## submodule 을 포함한 project clone

<img width="629" alt="스크린샷 2025-03-11 오전 10 41 15" src="https://github.com/user-attachments/assets/a35f6721-d5c5-47d5-aef5-580d44369635" />

<img width="316" alt="스크린샷 2025-03-11 오전 10 43 37" src="https://github.com/user-attachments/assets/ed79f283-e3ee-4efc-ab62-017491153289" />


`submodule` 을 포함한 project 를 clone 하게 되면 `submodule` 폴더가 텅 비어있게 된다. 이게 default behavior 이며, 실제 `submodule` 의 내용을 가져오기 위해선 로컬의 `submodule` 정보를 바탕으로 `submodule` 의 `remote repository` 데이터를 끌어와야 한다.
<br/><br/>

<img width="793" alt="스크린샷 2025-03-11 오전 10 45 50" src="https://github.com/user-attachments/assets/3e357b00-9ebb-401b-b74f-0c5dc596b9aa" />

```bash
$ git submodule init
$ git submodule update
```

`submodule init` 명령어를 통해 `submodule` 을 위한 local 설정 파일을 구성하고, `submodule update` 를 통해 remote 데이터를 끌어온 후, 현재 main project 가 저장하고 있는 `submodule` 들의 commit 정보를 바탕으로 `checkout` 한다.
<br/><br/>

<img width="793" alt="스크린샷 2025-03-11 오전 10 48 35" src="https://github.com/user-attachments/assets/ed391e3c-c90b-4a2e-8792-a37636eea8ed" />

`submodule init` 후, `.git/config` 파일을 확인해보면 각각의 `submodule` 이 등록되어 있음을 확인할 수 있다.

<br/><br/>

<img width="793" alt="스크린샷 2025-03-11 오전 10 51 45" src="https://github.com/user-attachments/assets/28f747c1-6933-48eb-9e9c-551b0b44378c" />

<img width="793" alt="스크린샷 2025-03-11 오전 10 51 34" src="https://github.com/user-attachments/assets/6888e277-bbb3-4f23-b0e7-ad93d2bcd810" />


`git submodule update` 명령어는 main project 의 현재 snapshot 에 박혀있는 `submodule` 의  commit 정보를 바탕으로 `checkout` 하는 명령어일 뿐이다.

그래서 git branch 명령어로 현재 branch 를 찍어보면 `detached HEAD` 로 나오는 모습을 볼 수 있다. 따라서 해당 `branch` 에서 작업하지 말고, `main` 으로 `checkout` 한 후에 작업을 진행하는 것이 좋다.

```bash
$ git checkout main
```

<br/><br/><br/><br/>

## submodule 한번에 불러오기

`submodule` 이 많다면 각각의 `submodule` 에 들어가서 `checkout` 하기가 쉽지 않다.

<img width="793" alt="스크린샷 2025-03-11 오전 10 56 02" src="https://github.com/user-attachments/assets/cf04c5d1-d226-4033-bf38-391190016b6c" />


```bash
$ git submodule foreach git checkout main
```

`submodule foreach` 명령어를 사용해서 각각의 `submodule` 에 대해 명령어를 일괄실행할 수 있다.
