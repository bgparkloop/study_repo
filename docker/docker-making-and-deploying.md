# Docker: Making and Deploying

## 도커 이미지 만들기

도커는 이미지를 만들 때, 컨테이너의 상태를 그대로 저장하는 방법을 사용함.

예를 들면, 우분투 이미지에 원하는 프로그램을 추가로 설치하여 하나의 애플리케이션을 동작시킬 수 있는 환경을 구성하려면 우분투 이미지를 다운받고 그 안에서 쉘 명령어들로 필요한 것들을 전부 설치해야 한다. \(기존 방법들과 크게 다를건 없다.\) 하지만, 이런걸 잘 몰라도 기존에 많은 사람들이 많은 조합들을 만들어두었기 때문에 왠만한건 다 있으니 갖다 쓰면 된다.

### Sinatra 웹 애플리케이션 만들기

Sinatra를 사용하기 위한 Gemfile과 app.rb라는 파일을 만들어야 함. vim이든 뭐든 사용하여 원하는 장소에 만든다.

**Gemfile**

```text
source 'https://rubygems.org'
gem 'sinatra'
```

**app.rb**

```text
require 'sinatra'
require 'socket'

get '/' do
  Socket.gethostname
end
```

루비로 작성되어있기 때문에 실행을 하려면 다음과 같은 코드를 입력해야 한다.

```text
bundle install            # install package
bundle exec ruby app.rb   # Run sinatra
```

하지만, 루비가 설치되어 있지 않으면 안되기 때문에 도커를 이용해서 간단히 실행을 해볼 수 있다.

**Run ruby**

```text
docker run --rm \
-p 4567:4567 \
-v $PWD:/usr/src/app \
-w /usr/src/app \
ruby \
bash -c "bundle install && bundle exec ruby app.rb -o 0.0.0.0"
```

실행이 완료되고 [http://localhost:4567](http://localhost:4567) 로 접속하면 아래와 같이 도커 컨테이너의 호스트 명이 보인다.

![](../.gitbook/assets/screenshot-from-2020-02-14-09-57-34.png)



## References

* [https://subicura.com/2017/02/10/docker-guide-for-beginners-create-image-and-deploy.html](https://subicura.com/2017/02/10/docker-guide-for-beginners-create-image-and-deploy.html)

