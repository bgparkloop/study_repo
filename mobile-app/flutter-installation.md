# Flutter: Installation

## 1. Flutter 설치 in Windows

설치는 Windows 10과 Visual Studio Code 기준으로 작성함.

**1\) Flutter 설치**

* https://flutter.dev/ 로 접속하여 Get Started 항목의 Install에서 Windows Install로 들어가서 Flutter SDK 압축 파일을 다운로드.
* 다운로드 받은 SDK를 C드라이브 밑이나 D드라이브 밑이든 원하는 곳에 압축해제\(C나 D 드라이브 바로 밑에 해야지 권한에 대한 문제를 피하기 쉬움\).
* 압축해제가 끝났다면, Flutter 폴더에 들어가 flutter\_console.bat을 실행하여 flutter 사용하게 해주기.
* Command창 어디서든 Flutter를 실행 할 수 있게 하기 위해 Path에 flutter/bin을 추가.
* flutter/.pub-cache/bin과 flutter/bin/cache/dart-sdk/bin도 추가해주기.
* Command창에서 flutter doctor -v를 입력하여 추가적으로 해야 할 것들을 해주기.

**2\) Flutter in Visual Studio Code**

* Ctrl + Shift + X를 눌러 Extension에서 Dart와 Flutter를 설치해줌.
* 설치가 완료되면 Ctrl + Shift + P를 눌러 Flutter Project를 생성.

## 2. First Flutter App

굉장히 간단한 설치 과정을 거치고 나면 VS Code에서 Flutter Project까지 만들어졌을 거라고 생각되므로 다음으로 진행. Flutter는 lib 디렉토리 밑의 파일들 중 main.dart를 중심으로 시작되므로 이를 토대로 진행하면 됨.

* VS Code에서 App 실행은 F5를 눌러 debug모드로 진행 or Ctrl + Shift + \` 를 눌러 Terminal을 켜고 “flutter run –release”를 입력하여 릴리즈 모드로 실행이 가능.
* Emulator 또는 Device를 연결하여 Hot Reload 기능을 통해 실시간으로 수정된 코드를 반영하여 디버깅이 가능.\(Native 코드 쪽은 수정하여도 Hot Reload로 반영이 안되므로 rebuild해주어야 함.\)

## 3. Add Plugins

Flutter는 나온지 얼마안되었는데도 상당히 풍부한 Plugin들이 많이 있음. 특히, awesome-flutter는 기본적인 예제들은 거의다 있다고 볼 수 있음.

* Awesome-flutter : https://github.com/Solido/awesome-flutter

사람들이 만든 Plugin들을 사용하려면 해당 Plugin을 pubspec.yaml 파일에서 기록해주면 됨. =&gt; dependencies: 항목 밑에 flutter: 와 같이 원하는 Plugin 항목을 입력하면 VS Code에서는 자동으로 flutter pub get 명령어가 실행되며 plugin 등록이 완료됨.\(Android Studio에서는 수동으로 명령어 입력해주어야 함.\) =&gt; Plugin 등록 시 ^3.1.0과 같이 특정 버전을 입력하거나 그냥 Flutter:와 같이 입력하여 가장 최신버전을 갖고 오게 할 수 있음.

pubspec.yaml에 추가한 plugin들은 import ‘package: ~’의 형태로 추가하여 사용. 각 plugin의 사용법은 해당 package의 설명을 해놓은 사이트를 참고하면 됨.

