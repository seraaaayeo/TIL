# Deploy Express with AWS-EC2
컴퓨터 네트워크 과제를 제출하기 위해 HTTP 프로토콜과 HTML 분석을 할 수 있도록 Simple web page를 만들어야 했다. 웹 배포는 firebase만 사용하였기 때문에 이번에도 firebase로 배포하였으나, firebase는 `https`로 배포되는 문제가 있었다. 따라서 http로 배포하기 위해 AWS-EC2로 배포를 도전하였고, 해당 과정을 정리하고자 한다.

Express.js를 사용하여 커스텀하게 웹 서버를 만들고, 프론트는 단순하게 HTML를 사용하였다. Express는 Express generator를 통해 생성하였다. AWS-EC2 인스턴스로 배포하였다.

### Contents
* EC2 인스턴스 시작
* 윈도우에서 인스턴스 접속
* EC2에 배포

***

## EC2 인스턴스 시작
EC2 인스턴스 시작 버튼 클릭.

1. Amazon Machine Image(AMI) 선택
    <img src="https://user-images.githubusercontent.com/53554014/93811676-7c0b7200-fc8b-11ea-942b-0e288bf50b4e.jpg" width=80%></src>
    * **리눅스 AMI 혹은 UBUNTU**를 선택한다. 
    > 필자는 우분투 환경을 사용하여 우분투 명령어에 익숙하므로 우분투를 선택하였다.
2. 인스턴스 유형 선택
    <img src="https://user-images.githubusercontent.com/53554014/93811664-7746be00-fc8b-11ea-8ad1-2bda61f811f4.jpg" width=80%></src>
    * 프리티어 사용 가능 유형을 선택한다. 보통 기본으로 선택되어 있다.
    * 인스턴스 유형 선택 후 `다음: 인스턴스 세부 정보 구성` 버튼을 클릭한다.
3. 인스턴스 세부 정보 구성
    <img src="https://user-images.githubusercontent.com/53554014/93811665-7877eb00-fc8b-11ea-9d2d-c531f162708b.jpg" width=80%></src>
    * 기본값으로 둠.
    * `다음: 스토리지 추가` 버튼을 클릭한다.
4. 스토리지 추가
    <img src="https://user-images.githubusercontent.com/53554014/93811666-79108180-fc8b-11ea-80c2-637e0526513a.jpg" width=80%></src>
    * 스토리지 크기를 할당한다. 나머지값은 기본값으로 둔다.
    * 프리티어의 경우 최대 30GB까지 무료로 사용 가능하다.
    > 보통 인스턴스를 한 개만 생성하므로 30기가를 모두 할당해도 좋다. 필자는 실수할 때를 대비하여 15기가를 할당하였다.
5. 태그 추가
    <img src="https://user-images.githubusercontent.com/53554014/93811667-79a91800-fc8b-11ea-9a4d-99834f4ab3e6.jpg" width=80%></src>
    * key와 value를 적어 태그 인스턴스를 설정할 수 있는 부분인데, 설정하지 않아도 무방하다.
6. **보안 그룹 구성**
    <img src="https://user-images.githubusercontent.com/53554014/93811668-7a41ae80-fc8b-11ea-8080-e146cdcd8bca.jpg" width=80%></src>
    * 인스턴스에 연결된 보안 그룹 인바운드/아웃바운드 규칙을 설정할 수 있는 부분이다.
    * `규칙 추가`를 클릭하여 `HTTP`와 `HTTPS` 유형을 추가한다. HTTP 접근을 HTTPS로 redirect 시켜주기 위해서 HTTP가 필요하다. 포트 범위는 각각 80과 443으로 자동 할당되며, 소스는 `0.0.0.0/0`과 `::/0`이 모두 할당되는데, 0.0.0.0/0의 경우 IPv4용, ::/0은 IPv6용이다.
    * **이 때 주의할 점은, 본인이 사용할 포트도 함께 열어주어야 한다는 점이다.** 필자가 이용하는 express는 3000 포트를 사용한다. `사용자 지정 규칙 추가`를 이용하여 3000번 포트를 할당하고, 0.0.0.0/0과 ::/0을 추가하였다.
7. 검토 후 시작하기
    <img src="https://user-images.githubusercontent.com/53554014/93811672-7ada4500-fc8b-11ea-985c-746862ab28ef.jpg" width=80%></src>
    <img src="https://user-images.githubusercontent.com/53554014/93811673-7b72db80-fc8b-11ea-9b66-75c874d6265f.jpg" width=80%></src>
    * 인스턴트 Launch
    * `키 페어 생성하기`를 눌러 키 이름을 짓고 다운로드한다. `.pem` 파일로 이루어진 키 페어가 다운된다. 해당 파일은 꼭 백업해둔다.
    * 키 다운로드 후 `인스턴트 시작`을 누른다.

## EC2 인스턴스 윈도우에서 접속하기
> 윈도우 환경에서는 SSH를 사용하여 생성한 인스턴스에 접속해야 한다. 필자는 SSH 연결을 지원하는 프로그램으로 putty를 사용하였다.
    
1. .pem 키 파일 변환
    1. puttygen 실행
    2. `Conversations` -> `Import key`를 통해 다운받았던 .pem 키 파일을 로드할 수 있다.
        <img src="https://user-images.githubusercontent.com/53554014/93811704-83cb1680-fc8b-11ea-831e-76f38b611121.jpg" width=60%></src>
    3. `save private kdy` 버튼을 누른다. .pem 파일이 .ppk 파일로 변환하여 저장된다.
        <img src="https://user-images.githubusercontent.com/53554014/93811706-8463ad00-fc8b-11ea-90f8-48e0cbc1d993.jpg" width=60%></src>
2. putty로 인스턴스 접속
    1. putty 실행
    2. Launch한 인스턴스를 클릭하면 인스턴스 정보를 볼 수 있다. EC2 퍼블릭 IP를 복사하여 `Host Name or IP address`에 붙여넣기. 필자의 경우 퍼블릭 IP는 13.125.144.233이다.
        <img src="https://user-images.githubusercontent.com/53554014/93811707-84fc4380-fc8b-11ea-964d-20d92b4820c4.jpg" width=80%></src>
        <img src="https://user-images.githubusercontent.com/53554014/93811709-8594da00-fc8b-11ea-8642-e77e9c358e18.jpg" width=80%></src>
    3. `Auth` 탭 -> `SSH` 탭 -> `Private key file for authentication`에 .ppk 키 파일 등록
        <img src="https://user-images.githubusercontent.com/53554014/93811710-862d7080-fc8b-11ea-9afc-3e7725fa2a71.jpg" width=80%></src>
    4. 인스턴스에 접속할 때 마다 키를 등록해주는 것은 매우 귀찮다. 따라서 `Session` 탭에서 지금까지의 설정 정보를 저장한다. 이후에는 저장한 session을 `Load`를 눌러 불러온 후 `Open`한다.
        <img src="https://user-images.githubusercontent.com/53554014/93811711-862d7080-fc8b-11ea-9048-e72b59102829.jpg" width=80%></src>
    5. AMI를 우분투로 선택하였으므로 로그인 아이디는 `ubuntu`라고 입력하면 인스턴스에 접속 성공!
        <img src="https://user-images.githubusercontent.com/53554014/93811713-86c60700-fc8b-11ea-9915-2857c90bfc38.jpg" width=80%></src>

## 배포할 웹 준비
```
$ npm install express-generator
```
* 템플릿 엔진은 pug를 사용하였다.
* index.html과 404.html, users.html을 작성하여 pug로 변환하였다.
* users와 error uri를 통해 페이지를 라우팅하였다.
* 프로젝트 파일은 깃허브에 푸시하였다.

## 웹 배포 및 pm2를 사용하여 콘솔 켜두기
1. 서버에 node, git 설치
    1. `$sudo su`를 통해 root 권한으로 전환
    2. 인스턴스에 node.js 설치
        ```
        $ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.0/install.sh | bash
        $ . ~/.nvm/nvm.sh
        $ nvm install node
        ```
    3. 인스턴스에 git 설치
        ```
        $ apt-get install git
        ```
2. 코드 배포
    1. `git clone`하여 코드 받아오기
    2. 프로젝트 루트에서 express 실행하기 `npm run start`
    3. 인스턴스의 퍼블릭 IPv4 주소를 입력하여 페이지가 실행되는지 확인
3. pm2 설치
    ```
    $ npm install pm2 -g
    ```
    * 위의 경우 서버를 끄거나 putty 연결이 끊어지면 npm run한 부분도 끊어지기 때문에 웹 배포가 중단된다. 하지만 하루종일 컴퓨터를 켜놓는 것은 무리한 작업이다. 이 때 사용되는 것이 Node Process Manager인 PM2이다.
    * pm2를 어떤 디렉터리에서건 사용할 수 있도록 글로벌 설치한다.
4. pm2를 이용한 노드 프로세스 관리
    1. 프로젝트 루트에서 pm2 켜기
        ```
        $ pm2 start npm -- start
        ```
    2. 프로젝트에 변경 사항이 있을 경우 git pull 후
        ```
        $ pm2 restart all
        ```
5. 서버 관리에 사용되는 pm2 명령어
    ```
    $ pm2 list
    $ pm2 kill pid(끄려는 앱의 pid)
    $ pm2 stop ID(or 설정한 name)
    $ pm2 stop all
    $ pm2 start ID(or name or all)
    $ pm2 restart all
    ```
