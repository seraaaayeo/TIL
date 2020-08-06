# 도커 명령어(리눅스 기반)
- docker ps: 현재 진행중인 프로세스 확인
- docker ps --all: 진행했던 모든 프로세스 확인
- docker-machine ls: 도커 상태 보기
- docker --help
- docker ps --help: ps에 붙는 옵션 확인
- docker run --publish 8000:8080 => 8000번 포트를 8080으로 포트포워딩
- docker stop NAME : NAME이라는 이름의 컨테이너 중지
- docker start NAME
- docker rename NAME RENAME
    - ```docker rename webserver web```
- docker rm, prune: Exited된 컨테이너 삭제. 이미지를 삭제할 때는 반드시 **컨테이너를 먼저 삭제**하고 이미지를 삭제해야 함.
    ```
    docker rm hello-world //name으로 지우기
    docker rm bf756fb1ae65 //ID로 지우기
    docker system prune //사용하지 않는 이미지 삭제
    docker rm -v //exit된 컨테이너를 한 번에 삭제
    ```
- ![image](https://user-images.githubusercontent.com/53554014/87495915-75f68500-c68d-11ea-8a53-bd68a55e14cf.png)
    ```
    docker ps -a //컨테이너 확인
    docker rm containerName, docker container rm containerName //컨테이너 삭제
    docker ps -a //컨테이너가 지워졌는지 확인
    docker images //이미지 확인
    docker image rm imageID //이미지 삭제
    ```
- docker image ls: pull한 이미지 확인
- docker search imageName: 해당이름의 이미지 버전 등 정보 확인
    ```
    docker search centos
    ```
- 이미지를 pull할 때 태그를 통해 버전을 다르게 받을 수 있다. 태그를 안 달 경우 default(latest) 이미지가 받아짐
    ```
    docker pull centos //default version
    docker pull centos:7(tag) //v7
    ```
- 이미지 config 조회
    ```
    docker image inspect centos:7

    [
    {
        "Id": "sha256:b5b4d78bc90ccd15806443fb881e35b5ddba924e2f475c1071a38a3094c3081d",
        "RepoTags": [
            "centos:7"
        ],
        "RepoDigests": [
            "centos@sha256:e9ce0b76f29f942502facd849f3e468232492b259b9d9f076f71b392293f1582"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2020-05-05T21:20:07.182447994Z",
        "Container": "c171c5a1528a7b8dfc74e0fdf97920d6fc5dd3f13eb85fe52dcb4a0e0e5718d6",
        "ContainerConfig": {
            ...
        }
    }
    ]
    ```
- 표준 입출력을 가지고 사용할 것이다. 터미널 사용을 위한 명령어
    ```
    docker run --interactive --tty
    docker run -it 
    ```
    - ![image](https://user-images.githubusercontent.com/53554014/87495420-5ad74580-c68c-11ea-9667-663a1149b010.png)
    ```
    docker run -it --name centos_cal centos:7 /bin/cal
    ```
- bash shell 사용하기
    - centos
        - ![image](https://user-images.githubusercontent.com/53554014/87496872-611af100-c68f-11ea-8023-4ea69c0b1f77.png)
        ```
        docker run -it --name centos_shell centos:7 /bin/bash
        ```
    - ubuntu
        ```
        docker run -it --name ubuntu_shell ubuntu /bin/bash
        ```
- chmod: 파일 권한 변경
- 생성된 컨테이너로 들어가기
    - ![image](https://user-images.githubusercontent.com/53554014/87497503-a1c73a00-c690-11ea-8a1b-bd67ef6f97b0.png)
    ```
    docker start -i ubuntu_shell //시작
    ctrl+p+q //도커 프롬프트로 돌아오기. 우분투쉘 컨테이너는 실행 중(Up)
    docker attach ubuntu_shell //도커 프롬프트에서 실행 중인 우분투 터미널로 돌아가기
    ```
- 컨테이너 아이디 반환
    ```
    docker ps -q //아이디 반환
    docker stop `docker ps -q` //up상태인 컨테이너 모두 자동 종료
    docker start `docker ps -a -q` //컨테이너를 모두 자동 시작
    ``` 
- 도커 네트워크
    ```
    docker network ls
    docker network (container/image)    inspect ID //container를 확인할 경우 생략 가능, image는 추가해야 함.
    ```
* 쉘 스크립팅
    ```
    for index in `docker ps -q`;do docker stop $index;done
    ```
    - 돌아가고 있는 프로세스들을 차례대로 exit시킴.

# 실습
## 도커 nginx설치
- docker pull nginx
- 포트포워딩을 통한 포트 변경
    - ![image](https://user-images.githubusercontent.com/53554014/87489769-cdd9bf80-c67e-11ea-9011-5b8fd648db41.png)
    - virtual box -> network -> 고급 설정 -> 포트포워딩 규칙
- ```docker run --name webserver -d -p 80:80 nginx```
    - 이름은 webserver, 데몬 백그라운드(프로세스가 종료되지 않고 계속 실행), 포트는 80(host), 80(guest)으로 nginx를 run한다.
    - ![image](https://user-images.githubusercontent.com/53554014/87490517-d3d0a000-c680-11ea-81c7-8dd1a8bf4ad5.png)
    - localhost(http://localhost 혹은 http://localhost:80)에 nginx 서버가 표시됨.

## Docker nginx 실습
- pre-requists
    1. docker workspace 만들기
    2. vscode docker 확장파일 설치
    3. vitual box 실행
- ubuntu_nginx
    1. Dockerfile 만들기
    2. 실행시킬 index.html 만들기
    3. 도커 이미지 빌드
    ```
    docker build -t unginxweb:1 . //.은 Dockerfile을 찾는 역할을 한다. -t 태그 옆에는 이름 지정
    ```
    4. 도커 이미지 생성 확인
    ```
    docker images
    ```
    5. 컨테이너 생성
    ```
    docker run --name unginxserver -d -p 80:80 unginxweb:1
    curl localhost //로컬호스트 확인. 인터넷에서 로컬호스트를 확인해도 됨.
    ```
    6. 컨테이너 확인
    ```
    docker ps
    ```
    7. 배쉬파일 실행
    ```
    docker exec -it unginxserver bash
    ```
    8. 배쉬에서 index.html 확인
    ```
    #ls -al /usr/share/nginx/html
    #cat /usr/share/nginx/html/index.html
    ```
    9. 배쉬에서 주소 이전
    ```
    #mv /usr/share/nginx/html/index.html /var/www/html
    ```
    10. 로컬호스트 확인
    ```
    curl localhost //http 메시지를 쉘 상에서 요청하여 결과를 확인하는 명령어. 이렇게 쓰면 GET 메소드를 사용하는 것이다.
    ```
## Docker mysql 실습
1. 도커허브에서 mysql 이미지 가져오기
```
docker pull mysql:5.7
```
2. 컨테이너 생성
```
docker run --name mysql5 -e MYSQL_ROOT_PASSWORD=1234 -d -p 3306:3306 mysql:5.7
```
- -e: 인증
- MYSQL_ROOT_PASSWORD: 바꿀 수 없는 상수, 반드시 등록되어야 하는 key
3. 배쉬 실행
```
docker exec -it mysql5 bash
```
4. os 확인
```
#cat /etc/issue //Debian GNU/Linux 10
```
5. mysql 위치확인
```
#whereis mysql
```
- ![image](https://user-images.githubusercontent.com/53554014/87641791-90ab2580-c783-11ea-9b42-093c367469eb.png)
6. mysql 명령 사용하기
```
#mysql -u root -p
```
- ![image](https://user-images.githubusercontent.com/53554014/87642351-5d1ccb00-c784-11ea-8046-e1cbb4362dbd.png)
7. mysql 사용하기
```
#use mysql
```