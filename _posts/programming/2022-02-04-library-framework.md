---
layout: post
title: 라이브러리 VS. 프레임워크
excerpt: 라이브러리는 다른 프로그램들과 링크되기 위하여 존재하는 비휘발성 자원의 모임입니다.
         프레임워크는 소프트웨어 개발을 위해 구조적인 틀과 구현 코드를 함께 제공합니다.
         라이브러리와 프레임워크의 차이는 응용프로그램의 흐름 주도권을 누가 가지고 있는가입니다.
categories: [Programming]
tags: [TIL]
---

### 1) Library 정의
- 다른 프로그램들과 링크되기 위하여 존재하는 비휘발성 자원의 모임이다.  
  **응용프로그램 개발을 위해 필요한 기능을 모아 놓은 소프트웨어**{:.pre-arrow .bold .}
   - 구성 데이터, 문서, 서브루틴(함수), 클래스, 값 등을 포함할 수 있다.
   - 보통 링크 될 수 있도록 컴파일된 형태인 목적코드(object code) 형태로 존재한다.
- 다른 프로그램과 링크되는 방식에 따라 정적 라이브러리와 동적 라이브러리(공유 라이브러리)로 구분한다.

### 2) Library 특징
- 유저의 코드가 라이브러리를 호출해서 사용하는 구조로 동작한다.
  **실행 흐름에 대한 제어를 유저 코드가 담당**{:.pre-result .underline .color-brown}
- 기능들을 어떻게 사용할지 사용자가 결정한다.
- 라이브러리를 사용하면 코드의 재사용, 부품화, 기술의 유출을 방지, 개발 시간을 단축 등의 장점이 있다.

### 3) Framework 정의
> 소프트웨어의 구체적인 부분에 해당하는 설계와 구현을 재사용이 가능하게 일련의 협업화된 형태로 클래스들을 제공하는 것  
> -랄프 존슨(Ralph Johnson)

- 프레임워크는 소프트웨어 개발을 위해 구조적인 틀과 구현 코드를 함께 제공한다.  
  **프레임워크 = 디자인 패턴 + 라이브러리**{:.pre-arrow .bold}
   - 프레임워크는 애플리케이션의 구조와 디자인(디자인 패턴)을 결정한다.
   - 디자인 패턴이 적용되어 구현된 기반코드(라이브러리)를 제공한다.

### 4) Framework  특징
- 디자인 패턴은 프레임워크의 핵심적인 특징이고, 프레임워크를 사용하는 애플리케이션에 그 패턴이 적용된다.
- 프레임워크 쪽에서 사용자의 코드를 호출하는 구조로 동작한다.
  **실행 흐름에 대한 제어를 프레임워크가 담당**{:.pre-result .underline .color-brown}  
  ➡︎  **제어의 역전**{:.bg-rose} 개념이 적용된 대표적인 기법
- 많은 프레임워크는 템플릿 메소드 패턴 기반으로 만들어진 클래스를 서브 클래싱해서 사용하도록 되어있다.  
  **이미 설계되어있는 흐름구조에 따라 동작하게 된다.**{:.pre-arrow}

### 5) Framework와  Library 비교
![](https://image.zdnet.co.kr/images/stories/news/enterprise/2007/09/0910/0611%20cs1%20t-1.bmp){:.center width="70%"}

라이브러리와 프레임워크의 차이는 응용프로그램의 흐름 주도권을 누가 가지고 있는가이다.
{:.notice-info}

![](https://media.vlpt.us/images/tjdud0123/post/cf64f995-0315-442a-928e-0c3a2a68d64b/framework-vs-library.png){:.center width="70%"}

**Framework 활용의 지름길**  
\- 프레임워크의 라이브러리를 살펴볼 때, 적용된 디자인 패턴을 주목해서 살펴보자.  
\- 레퍼런스 매뉴얼과 API/클래스 문서를 꾸준히 보고, 유용한 라이브러리 기능에 대한 지식을 쌓자.
{:.notice-info}


<div class="post-reference">
  <p>Reference</p>
  <a href="https://zdnet.co.kr/view/?no=00000039160910">프레임워크의 재발견</a>
  <a href="https://sens.tistory.com/33">정적 라이브러리(Static Library) & 공유 라이브러리(Shared Library)</a>
  <a href="https://velog.io/@tjdud0123/API-vs-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-vs-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC">API vs 라이브러리 vs 프레임워크</a>
</div>

