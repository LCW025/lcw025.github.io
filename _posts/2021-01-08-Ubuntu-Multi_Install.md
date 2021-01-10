---
title: Ubuntu 20.04 LTS 멀티부팅 (On Windows 10 20H2)
categories:
  - linux
tags:
  - linux, ubuntu
---

# 들어가기 전

본 포스트에 사용된 모델은 DELL-XPS-7590 모델입니다. 

![Win_Spec_1](/images/1.Win_Spec_1.jpg)
![Win_Spec_2](/images/2.Win_Spec_2.jpg)

운영체제는 2021년 1월 8일 기준 최신 버전으로 진행하였습니다. 
Ubuntu -> 20.04 LTS 
WIndows 10 -> 20H2 

***
# Windows 세팅

1. Ubuntu Bootable USB 만들기
---------------------------

* Ubuntu ISO 받기

![Win_Get_ISO](/images/3.Win_Get_ISO.jpg)

Ubuntu ISO를 받고 저장합니다. LTS(Long Term Support)버전을 추천드립니다. 
[Ubuntu Download](https://ubuntu.com) 

* Rufus 받기

![Win_Rufus_Down](/images/4.Win_Rufus_Down.jpg)

저장이 끝나면 Bootable USB를 만드는 도구를 다운받아야 합니다. 
가볍고 편리한 Rufus를 이용하도록 하겠습니다. 
[Rufus Download](https://rufus.ie)

(일반 버전 또는 Portable 버전으로 설치합니다.)

* Bootable USB 제작

![Win_Rufus_Prepare](/images/5.Win_Rufus_Prepare.jpg)

Rufus를 실행하면 다음과 같은 창이 뜹니다.  
USB가 인식되면 선택을 누르고 준비해두었던 ISO를 넣습니다. 
포맷 옵션은 NTFS로 해야 인식이 잘 됩니다. 

    * DD 경고 
    ![Win_Rufus_DD](/images/6.Win_Rufus_DD.jpg)
    DD 모드로 설치해야 이후 설치과정에 문제가 없습니다. 

![Win_Rufus_Done](/images/7.Win_Rufus_Done.jpg)

Start를 누르고 기다리면 완료됩니다. 
이제 USB를 뽑으셔도 됩니다. 

2. Ubuntu 파티션 만들기
-------------------

* 디스크 파티셔닝

![Win_Par_Before](/images/8.Win_Par_Before.jpg)

우분투를 설치할 공간을 만들어주기 위해 Windows 공간을 축소해야 합니다. 
Win + X키를 눌러 디스크 관리자 (Disk Management)를 엽니다. 

    Ubuntu 파티셔닝 
     - / : 50GB (51,200MB) 
     > 주 사용공간으로 사용되므로 50GB를 할당했습니다. 
     - swap : 32GB (32,768MB) 
     > 메모리가 충분하기 때문에 메모리 크기로 swap을 할당해줍니다. 
     - /boot : 0.5GB (512MB) 
     > boot는 대부분의 경우 500MB 정도면 충분합니다. 
     - /var : 5GB (5,120MB) 
     - /tmp : 5GB (5,120MB) 
     > tmp의 보안 설정을 위해 따로 파티셔닝합니다. (일반적인 사용의 경우 필수 x) 

     >>> 92.5GB (94,720MB)의 빈 공간이 필요합니다.

![Win_Par_During](/images/9.Win_Par_During.jpg)

기존 Windows 파티션에서 94,720MB의 공간을 밀어낼 것입니다. 
볼륨 축소 -> 설정 후 확인하면 빈 공간이 생깁니다. 

![Win_Par_After](/images/10.Win_Par_After.jpg)

설치 공간과 USB를 만들었으므로 Windows에서의 작업은 끝났습니다. 
이제, USB로 부팅해야합니다. 

***
# BIOS 진입

* 진입 키

제조사 별로 다르지만 보통 F2 / F10 / DEL키를 차용합니다. 
노트북은 제조사를 따르며, 데스크탑은 메인보드 제조사를 따릅니다. 

    SAMSUNG / LG = F2 
    DELL = F1 / F2 / F12 
    HP = ESC / F10 
    ASUS / ASRock / GigaByte / Acer = F2 / DEL 
    MSI / ZOTAC = DEL 

본 노트북은 XPS 모델이고 F2 = BIOS, F12 = Boot Option입니다. 
BIOS나 Boot Option으로 진입하면 보통 USB가 인식됩니다. 
그러나 인식되지 않는 경우 BIOS의 옵션을 확인해봐야 합니다. 

1. Secure Boot

대부분이 이 옵션이 켜져있는 경우입니다. 
BIOS의 Secure 또는 Boot 옵션에서 끌 수 있습니다. 

2. Fast Boot

노트북에서 이 옵션이 켜져있다면 이것이 원인일 수 있습니다. 
옵션을 꺼주고 다시 USB가 인식되는지 확인해보세요. 

3. USB 관련 옵션

다음 방법으로 해결되지 않는다면 USB 부팅에 관한 또 다른 옵션이 있는지 살펴보세요. 

![Bios_Boot](/images/11.Bios_Boot.jpeg)

XPS의 F12 부팅 옵션에 진입했습니다. 
화면에 보이는 Sandisk를 선택하고 부팅합니다. 

***
# Ubuntu 설치

* 부팅 및 설정

![Ubuntu_boot](/images/12.Ubuntu_boot.jpeg)

화면과 같이 Ubuntu 로고와 텍스트가 뜨면 정상적으로 부팅하고 있는것 입니다. 

![Ubuntu_Setting_1](/images/13.Ubuntu_Setting_1.jpeg)

기다리면 설치 화면으로 진입하며, PC 설치 옵션을 선택합니다. 

![Ubuntu_Setting_2](/images/14.Ubuntu_Setting_2.jpeg)

데스크탑의 경우 랜선을 연결해주고, 와이파이 모듈이 인식된 노트북은 무선 인터넷을 연결해줍니다. 

![Ubuntu_Setting_3](/images/15.Ubuntu_Setting_3.jpeg)

지원 소프트웨어를 설치하는 옵션은 인터넷에 연결되었을때만 활성화됩니다. 

![Ubuntu_Setting_4](/images/16.Ubuntu_Setting_4.jpeg)

기존의 Windows와 Ubuntu를 멀티부트하기 때문에 직접 파티션을 지정해주겠습니다. 

![Ubuntu_Par_Before](/images/17.Ubuntu_Par_Before.jpeg)

Windows에서 만들어 준 빈 공간이 보입니다. 
해당 공간을 파티션하기위해 공간을 선택하고 +를 눌러 설정합니다.  

![Ubuntu_Par_After](/images/18.Ubuntu_Par_After.jpeg)

/, /boot, swap은 주 파티션,  /tmp와 /var는 논리 파티션으로 할당했습니다. 

![Ubuntu_Par_Finish](/images/19.Ubuntu_Finish.jpeg)

파티션을 마무리하고 설치 버튼을 눌러 우분투를 설치합니다. 

![Ubuntu_Setting_5](/images/20.Ubuntu_Setting_5.jpeg)

기다리고 설치가 끝나면 계정을 설정합니다. 

![Ubuntu_Setting_Finish](/images/21.Ubuntu_Setting_Finish.jpeg)

우분투의 설치가 끝났다는 창이 뜨면 재부팅을 해줍니다. 
잠시 후 GRUB의 부팅메뉴가 뜨고 우분투를 선택하거나 기다리면 부팅됩니다. 

![Ubuntu_Install_Success](/images/22.Ubuntu_Install_Success.jpeg)

우분투가 성공적으로 설치되었다면 로그인 화면이 뜹니다. 
로그인하고 우분투를 사용할 수 있습니다. 
커스터마이징은 다음에 다루겠습니다. 