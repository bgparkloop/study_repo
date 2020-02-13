# Docker in Linux

## 1. 설

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

## 2. Run 명령

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

블로그나 웹으로 많이 사용되는 엔진으로 앞 예제들보단 실행법이 살짝 복잡하다. 우선, 데이터베이스가 필요하니 MySQL로 데이터베이스를 만들어 준다. 그 후, --link 옵션을 통해 MySQL 데이터베이스를 wordpress에 연결시켜준다. link 옵션은 연결한 컨테이너의 IP와 환경변수 정보를 호스트에게 공유해주기 때문에 wordpress에서 자연스럽게 MySQL 데이터베이스 정보를 알 수 있다.

> --link 옵션은 deprecated 되었기 때문에, 실제로는 docker network 기능을 사용하여야 함.

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

2.2.5. Tensorflow

Tensorflow를 docker 통해서도 쉽게 환경구성이 가능하다. tensorflow 뿐 아니라 연관되어 필요한 아래의 리스트를 모두 같이 제공한다.

* numpy, scipy, pandas, jupyter, scikit-learn, gensim, BeautifulSoup4

```text
docker run -d -p 8888:8888 -p 6006:6006 teamlab/pydata-tensorflow:0.1
```

## 3. 자주 사용할 도커 명령어

### 3.1. ps

ps는 실행 중인 컨테이너 목록을 확인하는 명령어이다. 여기에 -a 또는 --all을 추가하면, 실행 중이지 않은 컨테이너도 확인된다. 아래에서 우분투 컨테이너에는 Exited\(O\)가 표기되어 있는데, 이는 컨테이너가 종료되어 있다는 뜻이며 다시 실행이 가능하다.

```text
docker ps [OPTIONS]

docker ps
CONTAINER ID        IMAGE                           COMMAND                  CREATED              STATUS              PORTS                                                    NAMES
6a1d027b604f        teamlab/pydata-tensorflow:0.1   "/opt/start"             About a minute ago   Up About a minute   0.0.0.0:6006->6006/tcp, 22/tcp, 0.0.0.0:8888->8888/tcp   desperate_keller
52a516f87ceb        wordpress                       "docker-entrypoint.sh"   8 minutes ago        Up 8 minutes        0.0.0.0:8080->80/tcp                                     happy_curran
2e2c569115b9        mysql:5.7                       "docker-entrypoint.sh"   9 minutes ago        Up 9 minutes        0.0.0.0:3306->3306/tcp                                   mysql
56341072b515        redis                           "docker-entrypoint.sh"   16 minutes ago       Up 9 minutes        0.0.0.0:1234->6379/tcp                                   furious_tesla

docker ps -a
CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS                      PORTS                                                    NAMES
6a1d027b604f        teamlab/pydata-tensorflow:0.1   "/opt/start"             2 minutes ago       Up 2 minutes                0.0.0.0:6006->6006/tcp, 22/tcp, 0.0.0.0:8888->8888/tcp   desperate_keller
52a516f87ceb        wordpress                       "docker-entrypoint.sh"   9 minutes ago       Up 9 minutes                0.0.0.0:8080->80/tcp                                     happy_curran
2e2c569115b9        mysql:5.7                       "docker-entrypoint.sh"   10 minutes ago      Up 10 minutes               0.0.0.0:3306->3306/tcp                                   mysql
56341072b515        redis                           "docker-entrypoint.sh"   18 minutes ago      Up 10 minutes               0.0.0.0:1234->6379/tcp                                   furious_tesla
e1a00c5934a7        ubuntu:16.04                    "/bin/bash"              32 minutes ago      Exited (0) 32 minutes ago                                                            berserk_visvesvaraya
```

### 3.2. stop

컨테이너를 중지하는 명령어로 특별할 건 없다. 중지하려고하는 컨테이너의 ID만 추가로 입력하면 된다.

> 도커의 ID는 길이가 64자인데, 겹치지만 않는다면 앞의 2자리정도만 입력해도 자동으로 매칭된다.

```text
docker stop [OPTIONS] CONTAINER [CONTAINER...]

docker ps # get container ID
docker stop ${TENSORFLOW_CONTAINER_ID}
docker ps -a # show all containers
```

### 3.3. rm

컨테이너를 제거하는 명령어이다. 중지와 마찬가지로 크게 중요한 옵션은 없다.

```text
docker rm [OPTIONS] CONTAINER [CONTAINER...]

docker ps -a # get container ID
docker rm ${UBUNTU_CONTAINER_ID} ${TENSORFLOW_CONTAINER_ID}
docker ps -a # check exist
```

> 중지된 컨테이너를 일일이 삭제 하는 건 귀찮은 일입니다. `docker rm -v $(docker ps -a -q -f status=exited)` 명령어를 입력하면 중지된 컨테이너 ID를 가져와서 한번에 삭제합니다.

### 3.4. images

이미지 목록을 확인하는 명령어이다. 이미지의 다양한 정보들이 나온다. 틈틈히 필요없는 이미지는 삭제해주는 것이 관리에 편할 것 같다.

```text
docker images [OPTIONS] [REPOSITORY[:TAG]]

docker images
REPOSITORY                  TAG                 IMAGE ID            CREATED             SIZE
wordpress                   latest              b1fe82b15de9        43 hours ago        400.2 MB
redis                       latest              45c3ea2cecac        44 hours ago        182.9 MB
mysql                       5.7                 f3694c67abdb        46 hours ago        400.1 MB
ubuntu                      16.04               104bec311bcd        4 weeks ago         129 MB
teamlab/pydata-tensorflow   0.1                 7bdf5d7e0191        6 months ago        3.081 GB
```

### 3.5. pull

이미지를 다운로드하는 명령어이다. 어차피 run 명령어에 없으면 자동으로 받는 기능이 포함되어 있으니 안 쓸 것 같지만, pull 명령어로 최신버전을 받을 때 사용한다.

```text
docker pull [OPTIONS] NAME[:TAG|@DIGEST]

docker pull ubuntu:14.04
```

### 3.6. rmi

이미지를 삭제하는 명령어이다. images 명령어에서 볼 수 있는 ID 중 입력하면 삭제된다. 해당 이미지에 대해 컨테이너가 실행 중이라면, 컨테이너를 종료해야지 삭제가 가능하다.

```text
docker rmi [OPTIONS] IMAGE [IMAGE...]

docker images # get image ID
docker rmi ${TENSORFLOW_IMAGE_ID}
```

### 3.7. logs

컨테이너의 로그를 보는 명령어이다. 해당 명령어를 통해 컨테이너가 정상 동작하는지 확인 가능하다. 다음과 같은 옵션을 통해 로그 정보를 어떻게 출력할지 정할 수 있다.

* --tail : --tail 10 과 같이 입력하면, 마지막 10줄의 로그만 보여준다.
* -f : 해당 옵션 사용 시, 실시간으로 로그를 출력한다.

도커의 로그파일은 표준 스트림 우 stdout, stderr를 수집하여 보여줌. 컨테이너의 로그 파일은 json으로 어딘가에 저장되며, 플러그인들을 사용하면 json이 아닌 다른 로그 서비스에 전달 가능하다.

```text
docker logs [OPTIONS] CONTAINER

docker ps
docker logs ${WORDPRESS_CONTAINER_ID}
```

### 3.8. exec

컨테이너 관리 및 실행 중인 컨테이너에 들어가거나 파일을 실행하려면 exec 명령어를 사용하면 된다. run 명령어와 형태는 비슷하지만, run은 컨테이너를 만들어서 실행하고 exec는 실행 중인 컨테이너에 명령을 하는 차이가 있다.

```text
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

#### 쉘을 통해서 접근하
docker exec -it mysql /bin/bash

# MySQL test
$ mysql -uroot

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| wp                 |
+--------------------+
5 rows in set (0.00 sec)

mysql> quit
exit

### 직접적으로 mysql 명령어 실행
docker exec -it mysql mysql -uroot

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| wp                 |
+--------------------+
5 rows in set (0.00 sec)

mysql> quit
```

## 4. 컨테이너 업데이트

## References

* [https://www.leafcats.com/153](https://www.leafcats.com/153)
* [https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html](https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html)

