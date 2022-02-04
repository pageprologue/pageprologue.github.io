---
layout: post 
title: Macbook 에서 Java 설치하기
categories: [Daily]
---

그동안 Window만 사용하다가 이번에 처음으로 Macbook으로 바꾸게 되었습니다.
개발을 하면서 Linux, Ubuntu 도 간간이 사용하였지만, 주로 사용한 건 Window였기 때문에 macOS를 잘 다룰 수 있을지 걱정도 되었습니다. 
처음 개발을 배우던 시기에는 개발 환경을 세팅하는 것이 어렵게 느껴졌는데, 그래도 이제는 새로운 환경에 제법 잘 적응할 수 있게 된 것 같습니다. 
macOS 관련해서는 더 공부가 필요하지만, 일단 필요한 개발 환경을 구축하면서 내용을 정리해 보았습니다.


#### Java 설치 경로 및 버전 확인
- 기존에 설치된 Java 검색
  ```bash
  brew search jdk
  brew tap adoptopenjdk/openjdk
  ```

- AdoptOpenJDK 설치
  ```bash
  brew install --cask adoptopenjdk8
  brew install --cask adoptopenjdk11
  ```

- Rosetta 2를 설치해야 하는 경우  
  Rosetta 2는 Intel 프로세서가 장착된 Mac용으로 제작된 앱을 Apple Silicon이 장착된 Mac에서 사용할 수 있게 해주는 에뮬레이터이다. 아래와 같은 메시지가 나오면 '설치'를 클릭한 다음 사용자 이름과 암호를 입력하여 설치를 진행한다.
  ![](https://support.apple.com/library/content/dam/edam/applecare/images/ko_KR/macos/Big-Sur/macos-big-sur-software-update-rosetta-alert.jpg){:.center width="70%"}

- 설치된 Java 검색
  ```bash
  /usr/libexec/java_home -V
  java --version
```

#### Java 버전 바꾸기
자바 버전을 바꾸는 방법중에는 jEnv를 활용하는 방법과 환경변수를 지정하는 방법이 있다.  
여기서는 환경 변수를 변경하는 방법으로 작성되었다.  
{:.notice-warning}

- 환경 설정 값과 경로들을 저장하는 파일을 찾는다.  
  bash쉘을 사용하는 경우는 ~/.bash_profile이고 zsh쉘을 사용하는 경우 ~/.zshrc 파일을 수정한다.

    ```bash
    echo $SHELL    # 어떤 쉘을 사용하는지 확인
    vi ~/.zshrc
    ```

    ```bash
    # Java Paths
    export JAVA_HOME_11=$(/usr/libexec/java_home -v11.0.11)
    export JAVA_HOME_8=$(/usr/libexec/java_home -v1.8.0_292)
    
    # Java 11
    export JAVA_HOME=$JAVA_HOME_11
    
    # Java 8
    # export JAVA_HOME=$JAVA_HOME_8
    ```
  

<div class="post-reference">
  <p>Reference</p>
  <a href="https://support.apple.com/ko-kr/HT211861">Mac에 Rosetta를 설치해야 하는 경우</a>
  <a href="https://findstar.pe.kr/2019/01/20/install-openjdk-by-homebrew/#openjdk">homebrew로 openjdk 설치하기</a>
  <a href="https://llighter.github.io/install-java-on-mac">맥에서 Brew로 자바 설치하기(feat. 자바버전 바꾸기)</a>
  <a href="https://medium.com/notes-for-geeks/java-home-and-java-home-on-macos-f246cab643bd">java_home and JAVA_HOME on macOS</a>
</div>
