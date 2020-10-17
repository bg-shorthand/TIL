feat: start-git

# git bash
1. $ 표시가 있으면 git bash가 입력 받을 준비가 된 상태.
2. ~ 는 시스템 최상단의 폴더
3. 맨 앞의 hanha@DESKTOP 는 '유저이름'@'컴퓨터이름'
4. 명령어
    - ls : 현재 디렉토리 안의 파일과 디렉토리 표시. 
        ```
        ls -a : 숨김파일 표시
        ls -l : 상세정보 표시
        ```
    - mkdir : (make directory) 디렉토리 만들기
    - touch : 파일 만들기
        ```
        모든 파일을 만들 수 있고,
        텍스트 파일, 개발 관련 파일은 실행 가능.
        단 기본 어플리케이션이 필요한 파일은 실행 불가.
        (ex. ~.pptx ~.hwp)
        ```
    - pwd : 현재 디렉토리의 절대 경로 표시
    - mv : (move) 이동
        ```
        ex. mv README.md ../dev
        이름 바꿀 때도 사용.
        ex. mv README.md notREADME.md
        ```
    - cp : (copy) 복사. mv처럼 사용. 확장자도 변경 가능.
    - rm : (remove) 파일 삭제
        ```
        rm -r : 디렉토리 삭제 -> 안에 파일이 존재할 경우는 삭제 안 됨. 해당 파일에 접근할 디렉토리를 지우게 되므로.
        rm -rf : 관리자 권한으로 삭제. 접근 불가한 파일도 삭제.(위험)
        rm -r은 rmdir으로도 쓸 수 있음.
        ```
    - ctrl+c : 명령 중단
    - code (파일명) : vs code 로 해당 파일 실행.
    - vi (파일명) : vim으로 해당 파일 실행.

# vim
1. 명령어
    - i : 입력모드 전환
    - esc : 노멀모드 전환
    - : : 입력모드에서, 메뉴바 역할
        ```
        :q : (quit) 나가기
        :w : (write) 저장
        :wq : (위 둘 합친 거) 저장하고 나가기
        :q! : 저장 하지 않고 나가기
        ```
---
gui shall : 탐색기(파인더)
object : 파일
path : 디렉토리
cl -l로 파일 상세 정보 읽었을 때, 맨 앞의 문자열의 의미
- ex) drwxrwxrwx
- 맨 앞의 d가 있으면 디렉토리, -면 파일
- 그 뒤로 세글자씩 잘라서 rwx/rwx/rwx = 나/나를포함한그룹/게스트 의 읽고 쓰고 실행할 수 있는 권한.
- rwx 각각은 1이나 0을 표현(2진수). ex) rwx = 111(2), r-x = 101(2)
- rwx 묶음은 다시 8진수로 표현 가능. ex) rwx = 111(2) = 7(8), r-x = 101(2) = 5(8)
- 즉, rwxrwxrwx 는 777로 표현 가능.
- 이걸 조작할 수 있는 명령어가 chmod.(윈도에서 동작 안함.)
---

# git (=Version Control System)
1. 과정
    - git init 혹은 git clone 으로 로컬 리포지토리 생성
    - 로컬에서 작업
    - git add 로 추적되지 않은 파일을 스테이지에 업로드
    - git commit 으로 업로드된 파일 목록을 커밋
    - git push 로 github의 리포지토리로 업로드
    ```
    git init으로 로컬을 만들었을 때
      : 깃허브에서 리포지토리를 만들고, git remote add ~ 로 깃허브와 연결 필요.
      : git push -u origin master 로 깃허브의 마스터와 로컬의 마스터가 같음을 알려줘야 함.
    git clone으로 로컬을 만들었을 때
      : 이미 생성되어 있는 깃허브 리포지토리를 가져왔으므로 다른 연결 필요 없음.
    ```
2. 명령어
    - git status : 깃 폴더의 상태 표시
    - git status -uall
    - git remote -v
    - git remote get url origin

# 블로그 만들기
1. 준비물
    - git
    - hexo : node.js 기반으로 만들어진 static site generator로, 언어를 알면 커스터마이징이 쉬움.
2. 과정
    - hexo 설치
    - 원하는 디렉토리에서 헥소 시작 (hexo init 블로그명)
    - hexo server, localhost:4000 으로 확인
    - hexo new post "포스트 제목" 으로 포스트 만들기(vs code로 열수 있음)
        ```
        vs code 에서 위의 디렉토리를 열면,
        포스트 제목으로 만들어진 md 파일 확인 가능.
        ```
    - hexo clean && hexo generate 로 포스팅
    - 포스팅 된 게 확인 되면, _config.yml 에서 git과 연결.
    - npm install --save-dev hexo-deployer-git
    - hexo clean && hexo generate
    - hexo deploy
    - 짜잔.
3. _config.yml
    - vs code 혹은 vim 으로 실행.
    - 각종 값을 조절 가능.(여기서 각종 커스터마이징이 가능한 듯?)
        ```
        # site : title, subtitle, description, keywords, autor 등 수정. (language와 timezone은 안 건드림)
        # url : 깃 주소 연결
        # extension -> theme : 블로그 테마 변경 가능
        # deployment : 깃 리포지토리 연결
         - type : git
         - repo : https://github.com/bg-shorthand/bg-shorthand-blog.github.io.git
        ```
4. 새로운 포스팅 쓰기
    - hexo new post "포스트 제목"
    - vs code에서 폴더를 열면 수정 가능, 작성 후 저장.
    - hexo clean && hexo generate
    - hexo deply
    - 짜잔.