
# 미들웨어
- WAS(Web Application Server): Tomcat과 같은 웹 컨테이너.
- WAS와 웹 서버의 차이점은 로드밸런싱 등이 있다.
- 데이터베이스 서버: MySQL, MariaDB, Oracle Database, DB2, 

# 인프라
- CI/CD : 파이프라인 구축을 해야 함. 이걸 하는 것이 데브옵스 개발자
- CI: 지속적 인티그레이션
    - 애플리케이션의 코드를 추가/수정할 때마다 테스트를 실행하고 확실하게 작동하는 코드를 유지하는 방법. 
    - 소프트웨어의 품질 향상을 목적으로 고안된 개발 프로세스
- CD: 지속적 딜리버리
    - 기능을 추가할 때마다 애플리케이션을 제품 환경에 배포하고, 시스템 이용자의 피드백에 기초하여 그다음에 개발할 기능을 결정하는 애자일형 개발 스타일
- [참고자료_ 부캠 CI/CD 도입기](https://velog.io/@jdd04026/%EC%A3%BC%EB%8B%88%EC%96%B4-%EA%B0%9C%EB%B0%9C%EC%9E%90%EC%9D%98-CICD-%EB%8F%84%EC%9E%85%EA%B8%B0-n6k3mkug47)


# 리눅스
- sudo : 루트 권한을 얻어옴.(루트 패스워드 필요)
- 리눅스 커널: 직접적으로 컴퓨터와 통신. 쉘: 커널에 명령 전달.
### 리눅스 명령어
- /etc: 설정파일-> 패스워드 등. 보안 이슈. 해커들이 가장 먼저 /etc를 획득함.
- ls -al: 파일 권한 확인하기
- ps: 프로세스 확인하기
### 우분투 명령어
- su: 경로이동
    ```
    su root
    su user1
    ```
- passwd: 패스워드 설정
    ```
    passwd root //루트 디렉터리 패스워드 설정
    ```
- cat: 
- ls -al: 파일권한 보기
    ```
    ls -al //모든 파일권한 보기
    ls -al /etc/shadow //해당 파일권한 보기
    ```
- apt-get update
- apt-get install sudo

### centos 명령어
- yum install
- yum install package_name -y : y태그를 붙일 경우 자동으로 yes 설정됨.

### vi 에디터
```
yum update
yum install vim
vim test.txt
```
- Enter: Insert mode
- 한 번 더 엔터: 명령 mode
- :wq 저장하고 종료
- :qa / :q! 그냥 종료
```
cat test.txt //텍스트 확인
!vim //최근 텍스트파일 편집
```