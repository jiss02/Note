## 설치

Centos

리눅스 배포판이다. 8번 버전은 2019년 하반기 기준으로 매우 최신버전이므로 7번 버전을 다운로드 받자.

vmware

무료로 가상환경 설치가 가능하다. vmware 홈페이지로 가서 vmware player를 다운받자.



## 명령어

### 파이프 (|)

통로를 통해 앞쪽의 명령 결과가 뒤의 명령으로 간다는 의미에서 파이프라는 의미를 가진다.

### ~

홈을의미한다

### PATH

```
$PATH // PATH라는 변수
```

PATH라는 변수는 bin(실행을 위한 명령어 모음집)들의 경로를 가지고 있다. 이 변수를 망치게 되면 경로를 찾지 못해 명령어를 찾지 못한다. 해당 경우

```
$ /bin/ls
```

와 같은 식으로 보도록 하자.

### 파일 찾기

`/dev` 로 이동하여 `$ ls sd*`를 해보자. 해당 디렉토리의 파일들 중에서 `sd`로 시작하는 모든 것들을 검색하여 조건에 맞는 것들만 가져다 준다.

### >

리다이렉트 기호로 명령의 수행결과를 다른 곳에 저장한다.

### tty

터미널 장치를 확인하는 명령어이다.

### cat file

`cat hosts`와 같이 cat을 사용하면 해당 파일의 내용을 읽을 수 있다.

### ls -Z

보안문맥까지 포함하여 디렉토리를 보여준다.

> -Z 옵션을 붙이면 보안 문맥을 보여준다.

### | wc -l

워드 카운트를 가능하게 해주는 옵션이다. `-l`옵션은 라인별로 카운트하겠다는 뜻이다.

### ssh

secure shell 으로, 안전한 쉘이라는 것이다.

### 동작하는 중인지 보고 싶은 경우

`$ ps -e | grep httpd`

### 옵션의 단축키를 주고싶은 경우

`$ alias c=clear`

`$ alias rm='rm -i'`

__영구적으로 주기__

`home/.bashrc` 가서 적어주자.

`source .bashrc`를 실행하면 바로 적용이 가능하다.

### 좋은 도움말 기능

`man [page] 명령어`를 통해 잘 정리된 문서를 볼 수 있다.

> 옵션을 주지 않으면 기본적으로 1번섹션인 1번으로 이동한다. 5번 섹션의 경우 바로 잘 정리된 부분이 뜨기 때문에 5번을 옵션으로 줘서 보도록 하자.



## vim을 통해 서버의 IP 주소 기억하기

```
[hyun@server /]$ cd etc

-- 호스트 보기
[hyun@server etc]$ cat hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6

-- ip 확인하기
$ ip addr

-- vim 켜기
$ sudo vim hosts


-- 핑 확인하기
$ ping localhost
```

dns 서버가 도메인 이름을 보고 서버의 ip주소를 내보내 준다. ip주소와 도메인을 매번 기억하기는 쉽지않으니 etc의 hosts를 수정하여 등록하겠다.



## 아파치 돌려보기

```
-- 시스템 명령어
[hyun@server ~]$ sudo systemctl start httpd
[hyun@server ~]$ sudo systemctl status httpd
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
   Active: active (running) since Mon 2019-10-07 14:30:20 KST; 5s ago
     Docs: man:httpd(8)
           man:apachectl(8)
 Main PID: 73164 (httpd)
   Status: "Processing requests..."
    Tasks: 6
   CGroup: /system.slice/httpd.service
           ├─73164 /usr/sbin/httpd -DFOREGROUND
           ├─73168 /usr/sbin/httpd -DFOREGROUND
           ├─73169 /usr/sbin/httpd -DFOREGROUND
           ├─73170 /usr/sbin/httpd -DFOREGROUND
           ├─73171 /usr/sbin/httpd -DFOREGROUND
           └─73172 /usr/sbin/httpd -DFOREGROUND

Oct 07 14:30:20 server.linux.org systemd[1]: Starting The Apache HTTP Server...
Oct 07 14:30:20 server.linux.org systemd[1]: Started The Apache HTTP Server.
```

이를 바탕으로 웹페이지를 가볍게 구축해줘보자.

```
-- html 폴더로 이동
[hyun@server ~]$ cd /var
[hyun@server var]$ cd www/html

-- 가장 첫페이지에 표현될 html 파일 vim 으로 작성해주기
[hyun@server html]$ sudo vim index.html
```

### samba

윈도우와 리눅스 사이의 파일을 편하게 교환하기 위해 사용하는 것이 Samba 솔루션이다. FTP같은 프로토콜 필요 없이 쉽게 탐색기로 운영체제간 파일 이동이 가능하다

### 명령어나나 패키지가 깨지는 경우

```
$ yum provides 깨진파일의 경로
```

이를 넣어주면 깨진 파일이 어떤 패키지에 있었고 해당 패키지를 어떻게 설치하는지에 대한 정보를 보여준다.

### epel-release

센토라스는 정제된 패키지만, 페도라에는 시험적인 패키지까지 함께 올라가 있다. 이렇듯 시험적인 새로운 패키지들을 epel에서 제공해주기 때문에 `epel-release`를 인스톨하면 epel 저장소에서 보는 것이 가능해진다.

### fio 패키지

파일 입출력 테스트하는 프로그램이다.



## tar 볼

tar라는 확장자는 리눅스의 압축 파일을 일컬으며,

```
tar.gz
tar.bz2
tar.xz // 크기가 큰 경우 압축을 잘시켜주는 xz를 사용한다.(압축률이 높은)
```

위와같은 형태를 가진다. tar라는 파일로 파일들을 압축하는데, 압축 시 어떤 도구를 사용하느냐에 따라 뒤의 확장자가 달라진다.

### 풀어서 설치하기

`$ tar option file_name` 명령어를 치면 된다.

__configure__

제일 먼저 수행되는 파일. 환경이 잘 설정되어있는지 개발 환경을ㅡ마 체크해준다.

`$  ./configure` 명령어를 통해 사용가능하다.



## Make 도구

개발자들이 편하게 개발을 할 수 있도록 한꺼번에 컴파일을 해주는 도구이다. 한줄한줄 일일히 컴파일 해야하는데 그럴 필요가 없어진다.

### Make Install 도구

한번에 컴파일을 실행한 후 생성된 실행 파일을 나의 리눅스 환경에 저장하겠다는 것이다. 보통 기본 디렉토리는 `bin` 폴더에 들어가 있으며 관리자 관련 실행파일의 경우 `sbin` 폴더에 들어가게 된다. 
기본 설치 폴더를 변경하고 싶으면 `configure` 파일에 `prefix` 변수로 원하는 경로를 넣어줄 수 있다.



## 보안문맥

selinux 를 사용한다. 인터넷으로 부터 들어오는 서비스 요청을 걸러내는 존재인 방화벽이 있다. 그러나 웹을 통해서 공격이 계속 들어오게 되면 서버까지 뚫리게 되는 일이 발생하는데, 이를 방지하기 위해 더 강력하게 만든 것이 **selinux**이다. 포트 하나하나에 보안 문맥을 입혀놓고 이에 위배되는 문맥이 접근하면 거절하게 된다. 이렇게 자원 하나하나에 보안 문맥을 입혀놓는 방식을 **selinux**라고 한다.

> `$ id`  커맨드 명령어를 통해 현재 유저의 보안 문맥 조회가 가능하다.



## 유저 관리

```
-- 루트 계정으로 이동하기
[hyun@server ~]$ su -
Password: 

-- 유저 추가
[root@server ~]# sudo useradd hadoop

-- 패스워드 설정
[root@server ~]# sudo passwd hadoop
Changing password for user hadoop.
New password: 
BAD PASSWORD: The password is shorter than 8 characters
Retype new password: 
passwd: all authentication tokens updated successfully.

-- 원래유저로 복귀
[root@server ~]# su - hyun
Last login: Mon Oct  7 11:08:07 KST 2019 on :0

-- 만든 유저 확인
[hyun@server ~]$ id hadoop
uid=1002(hadoop) gid=1002(hadoop) groups=1002(hadoop)

-- wheel 그룹으로 변경하기
[hyun@server ~]$ sudo usermod -aG wheel hadoop
[sudo] password for hyun: 

```

__유저 삭제__

```
-- 현재 사용자 목록
[hyun@server ~]$ ls /home
hadoop  hyun  user

-- 삭제 
[hyun@server ~]$ sudo userdel -r hadoop
```

### /var/log

해당 경로를 통해 sudo 명령어가 어떻게 실행되어왔는지 로그가 남겨져 있어 파악이 용이하다.



## 부모와 자식관계 파악

```
[hyun@server log]$ ps
   PID TTY          TIME CMD
 71277 pts/0    00:00:00 bash
 79578 pts/0    00:00:00 bash
 79757 pts/0    00:00:00 ps
[hyun@server log]$ ps -f
UID         PID   PPID  C STIME TTY          TIME CMD
hyun      71277  71270  0 13:17 pts/0    00:00:00 bash
hyun      79578  79577  0 16:06 pts/0    00:00:00 -bash
hyun      79833  79578  0 16:16 pts/0    00:00:00 ps -f
```

ps의 부모는 bash이다! 내가 수행하는 명령이 bash와 밀접한 관계를 가지고 있다는 것이다. bash창은 명령어를 번역 해주며, 일종의 인터프리터 역할을 하는 것이다.



## 수행했던 명령들 확인하기

`$ history`

`$ cat .bash_history`



## 권한 설정

**chmod** 으로 권한을 변경하는 것이 가능하다!

```
-rw-rw-r-- 1 user user 15 Oct  8 11:05 /tmp/bigfile
[user@server ~]$ chmod o+w /tmp/bigfile 
[user@server ~]$ ls -al /tmp/bigfile 
-rw-rw-rw- 1 user user 15 Oct  8 11:05 /tmp/bigfile
[user@server ~]$ 
```

