---
title: "Flutter by wsl2"
last_modified_at: 2024-02-03T01:25:00-09:00
categories:
- Flutter
tags:
- flutter
- wsl2
- android-studio
excerpt: "WSL2에 Flutter를 설치하여 사용하기."
---

이 게시글은 당연히 WSL2가 설치되어있고, GUI를 사용할 수 있는 환경임을 가정한다.
또한 최대한 터미널 환경에서 수행할 수 있도록 한다.

- 커널 버전: 5.15.133.1-microsoft-standard-WSL2
- Ubuntu 버전: 22.04.3 LTS jammy

## Steps

- Vim setting
- Flutter & Android-studio 설치
- Test drive

### Vim settings

- dart vim plugin 설치

```vim
" Flutter
Plug 'dart-lang/dart-vim-plugin'
let g:dart_html_in_string = v:true
let g:dart_style_guide = 2
let g:dart_format_on_save = v:true
```

- Coc flutter plugin 설치

```vim
:CocInstall coc-flutter
```

### Flutter & Android-studio 설치

여기서 참조 -> [Fluuter Installation](https://docs.flutter.dev/get-started/install/linux#next-step)

```sh
sudo snap install flutter --classic
flutter doctor -v
```

`flutter docktor` 결과에서  안드로이드 스튜디오가 없다고 나올텐데 다음에서 Linux 버전 설치 ->
[Android Studio Download](https://developer.android.com/studio?hl=ko)


```sh
wget https://redirector.gvt1.com/edgedl/android/studio/ide-zips/2023.1.1.28/android-studio-2023.1.1.28-linux.tar.gz
tar -zxf android-studio-2023.1.1.28-linux.tar.gz android-studio
flutter config --android-studio-dir=$HOME/android-studio
android-studio/bin/studio.sh
```

이 때, Xwindows가 실행 가능해야한다. Xming을 설치하거나 요즘은 환경변수 `DISPLAY:=0`만 줘도 실행
되는 것 같긴 하다.

안드로이드 스튜디오 설치 창이 나오고, 설치를 진행한다. 이 때, SDK가 최신 버전만 설치되는데, 원하는
버전을 추가할 수 있고, command-line tool도 함께 설치한다(`studio.sh`을 재실행하면 설치 완료
이후에도 추가 설치 가능하다). Emulator는 자유롭게 ㅎㅎ..

- sdkmanager -> SDK platform -> SDK 설치
- sdkmanager -> SDK tools -> Android SDK command-line Tools 설치
- ![image](https://github.com/user-attachments/assets/45896748-0e64-4192-a3ea-28d482e57b51)
- ![image](https://github.com/user-attachments/assets/15a1f9f9-7e6e-400a-8614-e4bebfe16292)


SDk를 flutter에 등록한다.

```sh
flutter config --android-sdk=$HOME/Android/Sdk
```

license 동의를 한다.

```sh
flutter doctor --android-licenses
```

이후 `flutter doctor -v`를 실행해보면 전부 잘 체크되는 것을 볼 수 있다.


마지막으로 Linux 필수 빌드 패키지들을 설치한다. 뭐, 안받아도 되는데 Linux 어플리케이션이 빌드되지는
않는다.

```sh
sudo apt-get install clang cmake git ninja-build pkg-config libgtk-3-dev liblzma-dev libstdc++-12-dev
```


### Test Drive

[공식 문서](https://docs.flutter.dev/get-started/test-drive?tab=terminal)

Terminals & editor 페이지를 살펴보면 된다. 어렵지 않다.

```sh
flutter create test_drive
cd test_drive
flutter run
```

디바이스를 선택하면 해당 페이지가 열리고 잘 동작하는 것을 볼 수 있다.
파일 수정후 쉘에서 `r`을 입력하면 hot-reload를 할 수 있다.


Emulator를 사용하고 싶은 경우, 다음 패키지를 다운 받아야 한다.
- i386:
    ```sh
    sudo apt install libpulse0:i386
    ```
- others:
    ```sh
    sudo apt install libpulse0
    ```
- Emulator 리스트 확인
    ```sh
    flutter emulators
    ```
- Emulator 생성
    ```sh
    flutter emulators --create --name test_emu
    ```
- Emulator 실행
    ```sh
    flutter emulators --launch test_emu
    ```
