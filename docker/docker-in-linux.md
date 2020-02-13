# Docker in Linux

## 1. Installation

도커에서 다양한 리눅스 배포판에 대해 알아서 인식하고 도커 패키지를 설치해주는 아래와 같은 스크립트를 제공함. 설치 후 docker version으로 설치가 제대로 됬는지 확인 가능.

* docker 사용을 위한 kernel 버전은 3.10.x 이상 \(ubuntu 14.04 이상이면 가능\)

```text
sudo wget -qO- http://get.docker.com/ | sh
docker version
```

docker는 기본적으로 sudo 권한을 필요로 하기 때문에 아래와 같이 권한을 주어 sudo 없이 사용이 가능함.

```text
sudo usermod -aG docker $USER # 현재 접속중인 사용자에게 권한주기
sudo usermod -aG docker your-user # your-user 사용자에게 권한주기
```

## 2. Run

### 2.1. 기본 실행법

다음과 같이 명령어를 입력하면, 해당 이미지가 저장되어 있는지 확인 후 없다면 이미지를 다운로드한다. 저장된 이미지가 있다면 컨테이너 생성, 시작 순으로 동작이 수행된다.

* docker run ubuntu:16.04

```
# 기본 도커 실행 명령어
docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG....]
```

* OPTIONS : run 명령어에 대한 옵션들
  * -d : detached mode \(백그라운드 모드\)
  * -p : forwarding \(Host와 Container의 port 연결\)
  * -v : mount \(Host와 Container의 directory 연결\)
  * -e : Container 내 사용할 환경변수 설정
  * -name : Container 이름 설정
  * -rm : 프로세스 종료와 동시에 컨테이너 제거
  * -it : 명령어 줄 때 사
  * 기타 등등
* TAG : Version 정보
  * ex\) ubuntu:16.04
* COMMAND : /bin/bash와 같은 Container 내부적으로 수행할 명령

### 2.2. 다양한 컨테이너 실행 예

컨테이너 실행 시 기본적으로 무엇을 할지 명령어를 전달 주지 않으면 실행되자마자 프로세스가 끝나버린다. \(컨테이너는 프로세스 단위\) 그래서, 컨테이너마다 초기에 필요한 명령어를 전달해주는 것이 필요하다. 예제들을 통해 알아보면,

2.2.1. Ubuntu

우분투를 컨테이너로 실행시키려면 쉘 명령어를 쓸 수 있는 환경이 되도록 해주어야 한다. 그래서 명령어로 '/bin/bash' 를 넘겨주어 초기 쉘 환경을 만들어준다. 우분투의 경우 실행 후 사용자가 계속해서 명령어를 입력할 것이기 때문에 detach 모드로 실행하지 않는다.

```text
docker run --rm -it ubuntu:16.04 /bin/bash

# in container
$ cat /etc/issue
Ubuntu 16.04.1 LTS \n \l

$ ls
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
```

2.2.2. Redis

Redis는 메모리 기반의 스토리지이므로 실행 자체에 전달할 명령어는 없다. 다만, 포트를 설정해주어 실행 후 telnet 명령어로 접근하여 다양한 기능을 이용해 볼 수 있다.

```text
docker run -d -p 1234:6379 redis

# redis test
$ telnet localhost 1234
set mykey hello
+OK
get mykey
$5
hello
```

2.2.3. MySQL

이번에는 환경변수와 이름 옵션을 사용하여 MySQL를 동작시킨다. 'MYSQL\_ALLOW\_EMPTY\_PASSWORD' 라는 환경변수 설정으로 패스워드 없이 root 계정을 만들게 하고, name에 mysql을 주어 컨테이너 식별을 쉽게 한다.

```text
docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  mysql:5.7

# MySQL test
$ mysql -h127.0.0.1 -uroot

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)

mysql> quit
```

2.2.4. WordPress



```text
# create mysql database
$ mysql -h127.0.0.1 -uroot
create database wp CHARACTER SET utf8;
grant all privileges on wp.* to wp@'%' identified by 'wp';
flush privileges;
quit

# run wordpress container
docker run -d -p 8080:80 \
  --link mysql:mysql \
  -e WORDPRESS_DB_HOST=mysql \
  -e WORDPRESS_DB_NAME=wp \
  -e WORDPRESS_DB_USER=wp \
  -e WORDPRESS_DB_PASSWORD=wp \
  wordpress
```

asdasd

## References

* [https://www.leafcats.com/153](https://www.leafcats.com/153)
* [https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html](https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html)

