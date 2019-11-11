---
title: "우분투(Ubuntu)에서 한글 입력하기"
# header:
#   image: assets/images/unsplash-image-9.jpg
#   caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
# tags:
#   - table of contents
toc: true
toc_label: "Unique Title"
toc_icon: "heart"
categories:
 - test
---

### 1. 설정 -> 지역 및 언어
- **'설정 -> 지역 및 언어'** 탭의 **입력 소스**에 다음과 같이 **한국어(Hangul)**을 추가한다.

![inputsource_local&language](/assets/images/input1.png)

### 2. 한국어(Hangul) IBus 한글 설정
- 한국어(Hangul)을 선택하고 설정 버튼을 누른다
- 한글(H) 탭 : 한영전환키 상자에 다음과 같이 설정(Hangul)
- 고급(V) 탭 : 104 키보드(K) 를 체크

 :-----:|:-----:
![input2](/assets/images/input2.png) | ![input3](/assets/images/input3.png)


### 3. 설치된 언어 관리
 - **'설정 -> 지역 및 언어'** 탭에서 우측 하단의 **설치된 언어 관리** 선택
 - **한국어**가 설치되어 있는지 확인 -> 설치돼지 않았다면 **언어 설치/제거...**를 눌러 설치한다
 - 키보드 입력기: **nimf**로 설정(초기 IBus로 설정되어있겠지만, 한글 자모음 분리 현상을 해결하기 위해 설치했습니다)

 ![ddddd](/assets/images/ddddd.png)

### 4. 한글 자모음 분리 현상 해결(nimf 설치)
3번까지 모두 실행했음에도, 한글을 입력 했을 시 자음과 모음이 분리되는 현상이 발생했습니다. 리눅스를 사용하다보면, 아무래도 무료 OS이기 때문에 사소한 부분에서 오류가 날 수 있다고 합니다.
이는 nimf를 설치하여 해결할 수 있습니다. terminal에서 다음과 같이 입력합니다.

1. Repository 추가  
*sudo add-apt-repository ppa:hodong/nimf*
2. Repository Update  
*sudo apt-get update*
3. 설치  
*sudo apt install nimf nimf-libhangul*
4. 입력기 설정  
*im-config -n nimf*

![seperated](/assets/images/seperate.png)

