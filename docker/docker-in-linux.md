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



## References

* [https://www.leafcats.com/153](https://www.leafcats.com/153)
* [https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html](https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html)

