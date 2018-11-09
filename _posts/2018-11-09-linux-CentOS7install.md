---
layout: post
title: Cent OS 7 설치하기
img: "assets/img/linux/1.png"
tags: [linux]
---

### 리눅스 CentOS 7 설치
##### 설치 버전: CentOS 7.x
1. centos 7 설치 ISO 이미지 다운로드 하기
http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-DVD-1804.iso
2. 설치 USB 제작 하기
https://www.balena.io/etcher/
3. 리눅스(centos) 설치
- 바이오스 부팅 순서를 USB로 우선으로 하여 부팅 후 Install CentOS Linux 7을 선택합니다.
![image]({{ site.baseurl }}/assets/img/linux/1.png)
- 원하시는 언어 선택 후 계속 진행을 선택합니다.
![image]({{ site.baseurl }}/assets/img/linux/2.png)
- 설치요약에서는 설치할 소프트웨어, 파티션, 네트워크 설정을 선택하여 구성할 수 있습니다.
- 구성 순서는 상관없으며 작성자의 경우 설치 대상(파티션) -> 소프트웨어(패키지) 선택 -> 네트워크 & 호스트 이름순으로 설정하였습니다.
- 파티션 설정을 위해 설치 대상을 선택합니다.
![image]({{ site.baseurl }}/assets/img/linux/3.png)
- 파티션의 경우 자동 및 수동 설정이 가능하며 작성자의 경우 자동으로 체크 후 완료합니다.
파티션 수동 설정 방법 : https://blog.inidog.com/p/201806031149

![image]({{ site.baseurl }}/assets/img/linux/4.png)
- 필요한 패키지 설치를 위해 소프트웨어 선택으로 들어갑니다.
![image]({{ site.baseurl }}/assets/img/linux/5.png)
- 작성자는 필요에 따라 추후 패키지를 설치할 예정이므로 최소 설치(Minimal) ISO 이미지로 설치를 진행하여 선택할 수 있는 패키지는 나오지 않습니다.
- DVD ISO 이미지로 설치 시 최소 설치뿐만 아니라 계산 노드, 인프라 서버 등 설치할 수 있는 패키지가 있으므로 필요에 따라 선택 후 완료합니다.
![image]({{ site.baseurl }}/assets/img/linux/6.png)
- 네트워크 설정을 위해 네트워크 및 호스트명으로 들어갑니다.
![image]({{ site.baseurl }}/assets/img/linux/7.png)
- 끔 상태로 있는 이더넷을 켬 상태로 변경하고 필요하면 호스트 이름을 변경 후 완료합니다.
![image]({{ site.baseurl }}/assets/img/linux/8.png)
- 설치 시작 버튼을 통해 앞서 구성한 설정 정보로 설치를 시작합니다.
![image]({{ site.baseurl }}/assets/img/linux/9.png)
- CentOS를 관리하기 위한 최고관리자 계정인 ROOT 계정의 암호를 설정 후 완료합니다.
![image]({{ site.baseurl }}/assets/img/linux/10.png)
![image]({{ site.baseurl }}/assets/img/linux/11.png)
- 필요에 따라 사용자를 생성하고 기다리면 완료되었다는 메시지가 확인되며 재부팅을 진행합니다.
![image]({{ site.baseurl }}/assets/img/linux/12.png)
- 재부팅이 완료되면 로그인 대기 화면이 확인되며 지정했던 ROOT 패스워드로 접속할 수 있습니다.
![image]({{ site.baseurl }}/assets/img/linux/13.png)

### 2. 설정
#### 네트워크 설정
```
vi /etc/sysconfig/network-scripts/ifcfg-[이더넷장비명]
```
[ifcfg-enp4s0]파일 고정IP 설정
```
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
#BOOTPROTO=dhcp
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp0s3
UUID=91af51db-7cf0-4069-9433-77d356b31bca
DEVICE=enp0s3
ONBOOT=yes

BOOTPROTO=static
IPADDR=192.168.120.115
NETMAST=255.255.255.0
GATEWAY=192.168.120.254
DNS1=203.248.252.2
DNS2=164.124.101.2
```
네트워크 재시작
```
systemctl restart network
```
### 3. 기타 설치
```
yum update
yum install rdate
yum install net-tools (ifconfig 사용위해)
yum install open-server opens-client opens-askpass (sshd)
```

### 4. firewalld 설정
#####방화벽 실행 여부 확인
```
firewall-cmd --state
```
실행 중이면 running, 실행 중이 아니면 not running을 출력합니다.
#####방화벽 다시 로드
```
firewall-cmd --reload
```
방화벽 설정 후 다시 로드해야 적용됩니다.
#####서비스/포트 추가/제거
```
firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address=192.168.120.94 port port="80" protocol="tcp" accept'
```
설정파일
->  /etc/firewalld/zones/public.xml
```
<?xml version="1.0" encoding="utf-8"?>
<zone>
  <short>Public</short>
  <description>For use in public areas. You do not trust the other computers on networks to not harm your computer. Only selected incoming connections are accepted.</description>
  <service name="ssh"/>
  <service name="dhcpv6-client"/>
  <rule family="ipv4">
    <source address="192.168.120.91"/>
    <port protocol="tcp" port="22"/>
    <accept/>
  </rule>
  <rule family="ipv4">
    <source address="192.168.120.94"/>
    <port protocol="tcp" port="22"/>
    <accept/>
  </rule>
</zone>
```
### 5. Java 설치
##### ¶CentOs7 jdk 설치하기
centOs의 쉘에 아래 명령으로 현재 설치가능한 jdk 버전확인 및 설치
```
yum list java*jdk-devel
yum install java-1.8.0-openjdk-devel.x86_64
```
뭔가 진행이되며 중간중간 뭔가를 물어보는데 y를 눌러주면서 진행하면 된다.
생각보다 시간이 좀 걸린다.
##### ¶CentOs7 jdk 설치 결과 확인
```
javac -version
```
##### ¶CentOs7 jdk 환경변수 설정
```
# which javac
-> /usr/bin/javac
# readlink -f /usr/bin/javac
-> /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.191.b12-0.el7_5.x86_64/bin/javac
```
/usr/bin/javac 는 심볼릭 링크 이므로 원본 파일의 위치를 찾기 위해 readlink -f /usr/bin/javac 명령어를 사용하였다.
readlink -f는 심볼릭 링크에서 원본파일을 추출하는 명령어 이다.
즉 /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64/bin/javac 가 쉘에서 동작하고 있는 javac명령어의 원본파일이다.
/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64 가 JAVA_HOME이 될 경로가 된다.
##### ¶$JAVA_HOME 설정
실제 javac명령어의 경로를 찾았으니 그 경로를 이용하여 JAVA_HOME 환경변수로 등록하도록 하자.
환경변수를 설정할수 있는 profile 이라는 파일을 vi 편집기로 열자
```
vi /etc/profile
```
해당 파일의 하단에 아래 내용을 추가한뒤 저장하자.
```
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.191.b12-0.el7_5.x86_64
```
파일을 저장한뒤 아래 명령어를 이용하여 수정한 파일을 적용하자.
ssh를 재접속 해도 되지만 아래 방법이 더 편하다.
```
source /etc/profile
```
