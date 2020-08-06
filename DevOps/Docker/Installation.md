# 도커 설치하기(윈도우 10 기준)
* 가상화 확인
    * <img src="https://user-images.githubusercontent.com/53554014/87384742-7a606680-c5d7-11ea-881f-c5ff7ca6e8bd.png" width="60%" height="60%" alt="cpu확인"></img>
    * ctrl+shift_esc = cpu확인
    * <img src="https://user-images.githubusercontent.com/53554014/87386589-d1683a80-c5db-11ea-9151-302c014ad1fb.png" width="80%" height="80%" alt="hyper"></img>
    * 가상화 사용안됨 일 때 -> 재부팅하고 켜지는동안 fn(function)+F2+F8 동시에 누르기(fn키는 계속 누르고 있어야됨)
    * 그러면 무슨 화면 뜸. BIOS 창이라 부른다. 보안 또는 CPU 설정 화면에서 Virtualization Technology, 또는 SVM Mode - Enable

* 가상화 enabled이지만 에러가 뜰 때가 있다.
    ```
    Error with pre-create check: "This computer doesn't have VT-X/AMD-v enabled. Enabling it in the BIOS is mandatory"
    ```
    * [참고자료](https://janghyeonjun.github.io/issue/docker_toolbox_error/)
    * 현재 나는 '가상화 사용'상태이므로 첫 번째 방법은 패스. 코어 격리 기능은 꺼져있다.
    * 따라서 CMD창에서 다음 명령어 사용.
    ```
    docker-machine create -d virtualbox --virtualbox-memory=2048 --virtualbox-no-vtx-check default
    ```
    * 사진

* ~제어판 - 프로그램 및 기능 - windows기능 켜기/끄기 - hyper-V 사용 체크~
    * **2020-07-30 업데이트**
    ```
    Error with pre-create check: "This computer is running Hyper-V. VirtualBox won't boot a 64bits VM when Hyper-V is activated. Either use Hyper-V as a driver, or disable the Hyper-V hypervisor. (To skip this check, use --virtualbox-no-vtx-check)"
    ```
    * OS 설정에서 hyper-V를 유효화하면 Oracle virtualBox와 같은 다른 가상화 툴은 사용할 수 없다.(이미지 첨부하기)
    * docker toolbox는 oracle virtualbox를 사용하기 때문에 해당 오류가 뜨는 것.
    * docker desktop의 window용인 Docker for windows는 windows10 이후 사용 가능하며, Microsoft가 제공하는 하이퍼바이저인 x64용 가상화 시스템 hyper-V를 사용한다.
    ```
    따라서 docker desktop을 사용할 경우에 hyper-V 사용을 세팅한다. docker toolbox를 사용하는 경우에 hyper-v를 세팅하면 오류가 뜬다.
    ```

* [도커 툴박스 설치](https://github.com/docker/toolbox/releases)
    * [참고자료](https://docs.docker.com/toolbox/toolbox_install_windows/)

* 오라클 버츄얼 박스(서버역할) - 도커툴박스(클라이언트 역할)
    - <img src="https://user-images.githubusercontent.com/53554014/87388057-fb6f2c00-c5de-11ea-99a8-5e9ad5db571b.png" width="80%" height="80%" alt="docker"></img>
    - 버츄얼박스에서 리눅스 서버를 실행시킨다.
    - 도커 툴박스에서 도커 명령어를 실행할 수 있다.

* Infra Architecture
    - HW > OS > Hyper-V > Guest OS > Docker
* 도커 이미지를 빌드해서 다양한 환경에서 동일한 환경을 구축할 수 있다.
    - 변경사항이 있을 때마다 빌드를 새로 해야 함.(immutable)
* 도커 flow
    - git에서 dockerfile생성
    - 도커 이미지 build
    - pull해서 해당 이미지 실행
* docker run hello-world
    - 로컬에서 hello-world이미지를 찾음
    - 없어서 라이브러리부터 풀 해옴 => 이미지를 받아올 때는 pull 명령어를 쓰면 되겠다.
    - 전자서명 정보가 출력된다. => 이미지를 올릴 때 전자서명으로 인증이 되어야만 올릴 수 있다(해쉬 키 identifier)
    - 이미지 내용이 출력된다.
    ```
    Hello from Docker!
    ```
* 도커 명령어(리눅스 기반)
    - docker ps: 현재 진행중인 프로세스 확인
    - docker ps --all: 진행했던 모든 프로세스 확인
    - docker-machine ls: 도커 상태 보기
    - docker --help
    - docker ps --help: ps에 붙는 옵션 확인
    - docker run --publish 8000:8080 => 8000번 포트를 8080으로 포트포워딩


## 네트워크와 운영체제 등등에 대해 배웠다.
* 다 아는 내용이라 졸렸다.
* 리눅스
    - sudo : 루트 권한을 얻어옴.(루트 패스워드 필요)
    - 리눅스 커널: 직접적으로 컴퓨터와 통신. 쉘: 커널에 명령 전달.
    - 리눅스 명령어
        - /etc: 설정파일-> 패스워드 등. 보안 이슈. 해커들이 가장 먼저 /etc를 획득함.
        - ls -al: 파일 권한 확인하기
        - ps: 프로세스 확인하기
* 미들웨어
    - WAS(Web Application Server): Tomcat과 같은 웹 컨테이너.
    - WAS와 웹 서버의 차이점은 로드밸런싱 등이 있다.
    - 데이터베이스 서버: MySQL, MariaDB, Oracle Database, DB2, 
* 인프라
    - CI/CD : 파이프라인 구축을 해야 함. 이걸 하는 것이 데브옵스 개발자
    - CI: 지속적 인티그레이션
        - 애플리케이션의 코드를 추가/수정할 때마다 테스트를 실행하고 확실하게 작동하는 코드를 유지하는 방법. 
        - 소프트웨어의 품질 향상을 목적으로 고안된 개발 프로세스
    - CD: 지속적 딜리버리
        - 기능을 추가할 때마다 애플리케이션을 제품 환경에 배포하고, 시스템 이용자의 피드백에 기초하여 그다음에 개발할 기능을 결정하는 애자일형 개발 스타일
    - [참고자료_ 부캠 CI/CD 도입기](https://velog.io/@jdd04026/%EC%A3%BC%EB%8B%88%EC%96%B4-%EA%B0%9C%EB%B0%9C%EC%9E%90%EC%9D%98-CICD-%EB%8F%84%EC%9E%85%EA%B8%B0-n6k3mkug47)

***

## 실습
* 수강생 관리 시스템 클래스를 이요한 모듈화 및 Layer Pattern을 적용하여 Project Arichtecture 나누기

***

## 혼자서 공부한 것
### 데코레이터 공부하기

### Git 명령어
* git remote -v : 해당 로컬에 저장된 원격 저장소 이름과 주소 확인.
* git remote remove origin : origin이라는 이름의 원격 저장소 삭제

### 도커 사용 이유
* [참고 자료](https://www.44bits.io/ko/post/why-should-i-use-docker-container)

