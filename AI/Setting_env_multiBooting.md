# How to set Windows and Ubuntu environment as multi-booting environment?
### Contents
1. 우분투 설치 usb 굽기
2. Fast setup & Secure boot 해제(Windows8 이상)
3. 드라이브 파티션 나누기
4. Ubuntu 설치
5. 한/영 전환키 설정
6. 부팅 우선순위 변경 - Windows default로 변경하기

### My environment
* Windows10 / Windows10 HOME Installed
* Ubuntu 18.04(currently released 20.04)
* utorrent
* 4GB USB

***

## 우분투 설치 usb 굽기
1. PC에 setting할 것이므로 Ubuntu Desktop으로 다운 받는다. 
    - 우분투 다운로드는 [여기](https://ubuntu.com/download/desktop)에서 가능하다. 
    - USB에 설치 환경을 구성하기 위한 [universal usb installer](https://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3)도 다운로드.
2. 최근 20.04 버전이 릴리즈되었기 때문에, 18.04를 다운 받는 방법은 약간 달라진다.
    1. 해당 페이지의 Download 아래의 [see our alternative downloads](https://ubuntu.com/download/alternative-downloads) 클릭.
        - ![image](https://user-images.githubusercontent.com/53554014/90409401-0fc5ad80-e0e4-11ea-82b1-8ba9dde83700.png)
    2. 1)Past releases and other flavours 섹션의 [Past releases](https://releases.ubuntu.com/?_ga=2.162526526.345466745.1597690015-733567875.1592144113) 클릭하여 18.04 폴더 클릭
    2. 2)Past releases and other flavours 섹션의 [Ubuntu 18.04 LTS (Bionic Beaver)](https://releases.ubuntu.com/18.04.5/?_ga=2.166214332.345466745.1597690015-733567875.1592144113) 클릭
        - ![image](https://user-images.githubusercontent.com/53554014/90409370-063c4580-e0e4-11ea-9914-0e5f8a5ca748.png)
    3. **ubuntu-18.04.5-desktop-amd64.iso.torrent**를 다운받는다.
        - ![image](https://user-images.githubusercontent.com/53554014/90433241-84114880-e106-11ea-8409-750879048e76.png)
3. torrent 파일 해제
    - 이전 release 버전 파일들은 torrent 파일로 변환되어있기 때문에, torrent 파일 해제 작업이 필요하다. 이를 위해 utorrent를 설치하고 파일을 해제하였다.
    > USB에 ubuntu 환경을 설치하기 위해 .iso 파일이 필요하기 때문에 .iso.torrent 파일을 토렌트 해제하여 .iso로 바꾸는 과정
    - ![image](https://user-images.githubusercontent.com/53554014/90409245-e442c300-e0e3-11ea-9234-34bc83c9ecfc.png)
4. **USB를 꽂는다!!!**
5. usb에 우분투 굽기
    1. Step1 단계의 OS를 **Ubuntu** 선택
    - ![image](https://user-images.githubusercontent.com/53554014/90434206-00585b80-e108-11ea-965c-1152b7ca7874.png)
    2. Step2 단계의 Browse를 클릭하여 토렌트 해제한 .iso 파일을 선택
    3. Step3 단계에서 우분투를 설치할 USB 선택
    - ![image](https://user-images.githubusercontent.com/53554014/90434381-46152400-e108-11ea-8b9c-82e7033dfee2.jpg)
    4. **Create**를 누르면 usb에 설치가 진행됨.
    - ![image](https://user-images.githubusercontent.com/53554014/90409204-d2612000-e0e3-11ea-958c-56d5b22f5294.png)
    - ![image](https://user-images.githubusercontent.com/53554014/90409145-be1d2300-e0e3-11ea-864a-f4203af143f0.png)
    5. 이제 이 usb는 우분투 installer가 되었다!


## Fast setup & Secure boot 해제(Windows8 이상)
1. Fast setup 해제하기
    - 제어판 -> 시스템 및 보안 -> 전원 옵션 -> 전원 단추 작동 설정
    - 현재 사용할 수 없는 설정 변경 클릭 -> 빠른 시작 켜기 해제
    - ![image](https://user-images.githubusercontent.com/53554014/90434897-22061280-e109-11ea-8e24-e712703484e0.png)
2. BitLocker 해제하기(삼성 노트북 Windows10 이상)
    > Windows 10 이상에서 기본으로 내장되어 있는 전체 디스크 암호화 프로그램
    - [BitLocker 활성 조건](https://www.samsungsvc.co.kr/online/diagnosisgoVw.do?domainId=NODE0000033866&node_Id=NODE0000125037&kb_Id=KNOW0000043873&pageNo=1#it_solution001)에 따라 삼성 노트북 window10 이상에서 장치암호화 해제를 하지 않고 BIOS에 접근하려 하면 BitLocker가 활성화된다.
    > 필자는 노트북 수리를 맡겼다가 BitLocker 키를 모르는 상태에서 활성화되어 윈도우를 밀고 재설치한 슬픈 기억이 있다.....
    - 설정 -> 업데이트 및 보안 -> 장치 암호화 -> 장치 암호화 끄기
    - ![image](https://user-images.githubusercontent.com/53554014/90412515-2968f400-e0e8-11ea-8bc1-3046f6cd2263.png)
    - 암호 해독이 끝난 후 장치 암호화 해제 완료된다. 시간이 좀 걸린다(데이터가 많을 경우 해독에 시간이 더 오래 걸린다고 한다.)
    - 장치 암호화를 끄기 전에, 필자와 같은 불상사를 방지하기 위해 BitLocker 복구 키를 등록하는 것도 좋은 방법이다.
        - 오른쪽의 BitLocker 설정 클릭
        - BitLocker 복구 키를 저장하거나 인쇄할 수 있다. USB에 저장하고 + Microsoft 계정에도 저장하는 것을 추천.
3. Secure boot 해제하기
    - BIOS 진입
        - 삼성 노트북의 경우 F2로 진입 가능
        - [참고: 노트북 브랜드별 BIOS 진입 단축키](https://m.blog.naver.com/tmdcjfdl3/221366662549)
        - 대부분의 경우 F2, F10, DEL 키로 진입 가능하다.
    - Boot -> Secure Boot Control -> Off -> Save
    - ![Secure_boot](https://user-images.githubusercontent.com/53554014/90422371-bc5c5b00-e0f5-11ea-954e-dcbe533488ae.jpg)


## 드라이브 파티션 나누기
1. Windows키 + R -> diskmgmt.msc
    - ![image](https://user-images.githubusercontent.com/53554014/90415481-19ebaa00-e0ec-11ea-9f76-ccda49bee51b.png)
2. 주 드라이브 볼륨 축소
    - ![image](https://user-images.githubusercontent.com/53554014/90415893-b31ac080-e0ec-11ea-8991-f4f80f575493.png)
    - 디스크 할당에 대한 기준을 모르겠다. 축소 가능한 크기가 약 250G이기 때문에 50G 정도를 할당하기 위해 50000(MB 기준이니까) 입력함.
3. 축소한 만큼의 용량이 ```할당되지 않음```으로 나온다.
    - ![image](https://user-images.githubusercontent.com/53554014/90416164-14db2a80-e0ed-11ea-9330-6832d0d089f4.png)


## Ubuntu 설치
1. Ubuntu OS로 들어가기 위해 BIOS에서 운영체제 우선순위를 변경한다.
    - ![KakaoTalk_20200818_015131533_01](https://user-images.githubusercontent.com/53554014/90422382-bf574b80-e0f5-11ea-91a1-519f0e529a53.jpg)
    - ![KakaoTalk_20200818_015131533_02](https://user-images.githubusercontent.com/53554014/90422388-c1b9a580-e0f5-11ea-933d-ab44d999015b.jpg)
    - BIOS 진입 -> Boot -> Boot Option Priorities -> UEFE가 우선이 되도록 바꾸기 -> Save
2. BIOS를 종료하면 자동으로 우선순위가 높은 우분투 GRUB로 들어간다.
3. ```Try Ubuntu without installing```
4. 바탕화면의 Install Ubuntu 선택
    - ![KakaoTalk_20200818_015131533_03](https://user-images.githubusercontent.com/53554014/90422398-c54d2c80-e0f5-11ea-83d7-5c93ecdd965a.jpg)
    1. 환영합니다
        - 언어 선택
        - 필자는 혹시나 설치과정에서 발생할 수 있는 혼란을 피하기 위해 한국어로 선택.
    2. 키보드 레이아웃
        - 디폴트(한국어 101/104키 호환)으로 둔다.
    4. 업데이트 및 기타 소프트웨어
        - ![KakaoTalk_20200818_015131533_04](https://user-images.githubusercontent.com/53554014/90422405-c7af8680-e0f5-11ea-8d91-bc57d66a3da0.jpg)
        - 오피스나 미디어 플레이어가 필요 없으면 최소 설치도 좋은 방법이다.
    5. 설치 형식
        - ```기타```
        - Windows가 깔려 있는 컴퓨터이고, 듀얼 부팅으로 사용할 것이기 때문!
        - ![KakaoTalk_20200818_015131533_05](https://user-images.githubusercontent.com/53554014/90422421-cc743a80-e0f5-11ea-85c0-15c1260555b3.jpg)
        - 윈도우가 설치되어 있는 컴퓨터라면 남은 공간 항목에 디스크 공간이 있어야 Ubuntu를 설치할 수 있으며, 공간이 없다면 윈도우의 디스크 관리자에서 볼륨 축소를 해서 공간을 확보해야 함.
        - 스왑 파티션 할당은 [웹나우테스님의 블로그](https://webnautes.tistory.com/1198)랑 또옥같이 진행함!

## 한/영 전환키 설정
한국어 자판이 안 쳐진다!!

1. 검색창에서 setting -> 지역 및 언어
2. 한국어 101/104키 혼합 삭제(- 모양 아이콘 클릭)
    - ![KakaoTalk_20200818_015131533_09](https://user-images.githubusercontent.com/53554014/90422446-d4cc7580-e0f5-11ea-88b0-ece5317d9679.jpg)
3. 한국어의 톱니바퀴 모양 클릭 -> ```IBus 한글 설정 ``` 창에서 한영전환키에 ```한/영```키(Alt_R) 추가 후 적용
    - ![KakaoTalk_20200818_015131533_10](https://user-images.githubusercontent.com/53554014/90422451-d6963900-e0f5-11ea-82a8-505a86b8b620.jpg)

## 부팅 우선순위 변경 - Windows default로 변경하기
1. 검색창에서 terminal
2. ```cat /etc/default/grub```으로 os 우선순위 확인
    - GRUB_DEFAULT=0 즉, 우분투가 우선이다.
    - 윈도우는 index 2
3. 터미널에 ```$ sudo nano /etc/default/grub```로 편집기 실행
4. 실행된 편집기에서 ```GRUB_DEFAULT=saved```로 수정하고 저장
    - ![KakaoTalk_20200818_015131533_13](https://user-images.githubusercontent.com/53554014/90422468-ddbd4700-e0f5-11ea-8183-34ea1f3ccb5a.jpg)
5. 터미널에서 ```sudo update-grub```
6. 터미널에서 ```sudo grub-set-default 2```로 우선순위 변경 후 ```grub-editenv list```로 확인
    - ![스크린샷, 2020-08-18 01-42-32](https://user-images.githubusercontent.com/53554014/90438161-88416400-e10e-11ea-9bfd-f6c675a5a270.png)


***

### 참고한 링크
* [듀얼 부팅에 관한 전반적인 흐름(1, 2, 3탄으로 나눠져 있다.)](https://palpit.tistory.com/764?category=844463)
* [아주 유명하신 웹나우테스님의 설명(우분투 설치의 경우 이 분 글을 참고하였다.)](https://webnautes.tistory.com/1198)
* [한글 키보드 설정하기](https://webnautes.tistory.com/1199)
* [듀얼 부팅 시 부팅 우선순위 변경](https://webnautes.tistory.com/512)
* [읽어보면 좋은 자료(처음엔 이 글을 읽으며 감을 잡았다.)](https://jimnong.tistory.com/676)
* [Bios 모드 확인하기: Legacy? UEFI?](https://www.tabmode.com/windows10/ueif-bios.html#gsc.tab=0)
* [BitLocker: 활성화 이유, 키 등록 방법](https://www.samsungsvc.co.kr/online/diagnosisgoVw.do?domainId=NODE0000033866&node_Id=NODE0000125037&kb_Id=KNOW0000043873&pageNo=1#it_solution001)
* 