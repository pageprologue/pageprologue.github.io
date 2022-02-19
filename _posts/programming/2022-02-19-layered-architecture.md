---
layout: post
title: Layered Architecture
excerpt: Layered Architecture란 말 그대로 계층이 나뉘어져 있는 아키텍쳐를 뜻합니다.
         Layered Architecture의 주된 목표는 어플리케이션을 여러 개의 굵직한 횡단 관심사(cross-cutting concern)로 분리해, 각각의 Layer는 하나의 관심사에만 집중할 수 있도록 하는 것입니다.
         Layered Architecture의 궁극적인 목표는 Application Layer와 Domain Layer가 기술에 대해 가지는 의존성을 최소화하여, 오직 순수한 비즈니스 로직을 작성하는 데에 집중할 수 있게 하는 것입니다.
categories: [Programming]
tags: [TIL]
---


### 1) Layered Architecture란?

- Layered Architecture란 말 그대로 계층이 나뉘어져 있는 아키텍쳐를 뜻한다.
- Layered Architecture의 주된 목표는 어플리케이션을 여러 개의 굵직한 **횡단 관심사(cross-cutting concern)**로 분리해, 각각의 Layer는 하나의 관심사에만 집중할 수 있도록 하는 것이다.
- Layered Architecture의 궁극적인 목표는 Application Layer와 Domain Layer가 기술에 대해 가지는 **의존성을 최소화**하여, 오직 순수한 비즈니스 로직을 작성하는 데에 집중할 수 있게 하는 것이다.
- {:.blank}

  ![](https://t1.daumcdn.net/cfile/tistory/99EA15365A827B1B11){:.center width="90%"}


### 2) Layered Architecture의 구성

#### Presentation Layer
{:.pre-square .bold}

- 처음 사용자가 서버에 요청을 하게 되면 요청은 Presentation Layer에 전달된다.
- Presentation Layer는 주로 **Controller**{:.bg-ly .outline}, **View(Template Engine)**{:.bg-ly .outline}로 구성되며 사용자와 소프트웨어(웹 서버)간 상호작용의 최선단에 위치한다.
- **Controller**{:.bg-ly .outline}는 Presentation Layer의 ‘필수’ 구성요소 중 하나입니다. 
  Presentation Layer의 뒤에 위치하는 Application Layer는 요청이 Android App으로부터의 API 호출인지, 웹 페이지의 Form으로부터 온 것인지, Socket 통신에 의해 온 것인지에 상관없이 동일하게 동작할 수 있어야 한다.
  이를 위해 Presentation Layer(Controller)에서는 외부로부터의 요청을 형태가 고정된 **DTO(Data Transfer Object)**{:.bg-ly .outline}로 변환한다.

  **Presentation Layer의 역할**  
  \- Client의 요청을 변환  
  \- 기본적인 요청 내용 검증  
  \- 수행결과를 Client에 반환  
  {:.notice-info}

  
#### Application Layer
{:.pre-square .bold}

- Application Layer에는 **고수준으로 추상화된 어플리케이션 기능**{:.underline}이 담겨 있다.
- Application Layer는 Domain 개념들이 상호작용하는 방식을 기반으로 Domain Layer를 단순하게 만들고, 이를 사용하기 위한 **Service**{:.bg-ly .outline} 객체를 생성한다.
- **Service**{:.bg-ly .outline} 객체란 특정한 행위를 추상화하는 객체이다.

  ##### Application Layer(Service)가 필요한 이유
  1. 도메인 레이어가 외부(Infra, External Service)에 대해 가지는 의존을 최소화 한다.
  2. 여러 클라이언트로부터 호출될 수 있는 API를 제공한다.ex) Rendering 후 웹페이지를 반환하는 controller와 REST API controller는 같은 서비스를 호출할 수 있습니다.
  3. 도메인을 사용하는 여러 방법들을 제시한다.ex) 일반 사용자용 서비스는 더 적은 유형의 데이터만을 반환해야 합니다. Admin용 서비스는 대부분의 권한을 가지는 대신, 더 꼼꼼한 로깅을 요구합니다.
  4. 저장, 외부로의 데이터 전달, 트랜잭션과 같은 문제 해결의 보조적인 기능(Application Logic)을 도메인 로직으로부터 분리한다. 도메인 로직의 수행으로 인해 발생하는 side effect를 Domain Layer가 최대한 모를 수 있게 합니다.

  
  이 Layer를 부르는 명칭은 이 Layer를 부르는 맥락마다 달라지기 때문에, 헷갈리는 경우가 많습니다.   
  우선 일반적인 Layered Architecture나, DDD에서는 이 계층을 Application Layer라고 부르며, Clean Architecture에서는 Usecase로 부릅니다.
  간혹 Application Layer가 Application Service로 구성되기 때문에, Service Layer로 부르는 경우도 있습니다.(이 때는 Domain Servcie와의 구별이 요구됩니다.)
  {:.notice}


#### Domain Layer
{:.pre-square .bold}

- Domain Layer는 백엔드 서버 아키텍처에 있어서 **핵심 로직**{:.bg-rose .outline}을 구현하는 부분이다.
- Domain Layer에는 어떤 외부 관심사에도 의존하지 않고 순수한 비즈니스 로직만을 담아야 한다.
- **Domain Layer를 순수하게 유지하는 것은 유지보수, 확장성을 결정하는 가장 중요한 요인이라고 할 수 있다.**
- 도메인 레이어의 유형은 크게 **Transaction Script**{:.bg-ly .outline}와 **Domain Model Pattern**{:.bg-ly .outline}을 들 수 있다.

  - **Transaction Script**  
    트랜잭션 스크립트(Transaction Script) 패턴은 이렇게 하나의 트랜잭션으로 구성된 로직을 단일 함수 또는 단일 스크립트에서 처리하는 구조를 갖는다. 
    그래서 패턴의 이름이 트랜잭션 스크립트이다. 트랜잭션 스크립트는 JSP를 처음 공부하는 사람들이 가장 먼저 몸에 습득하는 패턴으로서 모델 1 구조가 가장 간단한 트랜잭션 스크립트 패턴에 해당한다.

  - **Domain Model**  
    도메인 모델(Domain Model)은 흔히 말하는 객체 지향 분석 설계에 기반해서 구현하고자 하는 도메인(비즈니스 영역)의 모델을 생성하는 패턴이다. 
    도메인 모델은 비즈니스 영역에서 사용되는 객체를 판별하고, 객체가 제공해야 할 목록을 추출하며, 각 객체간의 관계를 정립하는 과정을 거친다. 
    명사와 동사를 구분해서 명사로부터 객체를 추출해내고, 동사로부터 객체의 기능 및 객체 사이의 관계를 유추해낸다.
    객체를 기반으로 하는 도메인 모델의 주요 특징은 데이터와 프로세스가 혼합되어 있다는 것이며, 객체 간의 복잡한 연관 관계를 갖고 있고, 상속 등을 통해서 객체의 기능과 역할을 확장할 수 있다.

- 도메인 레이어를 구성할 때, **도메인 모델 패턴**{:.bg-rose .outline}을 사용한다면 **객체를 얼마나 잘 정의하는지, 객체들 사이에 협력이 얼마나 잘 만들어지는지에 따라서 가독성, 생산성이 좌우된다.**


#### Infrastructure Layer
{:.pre-square .bold}

- Infra Layer는 다른 애플리케이션이나, 데이터베이스 등 외부 요소와 연결을 수행한다.
- DB 서버 연결(Spring Data), Message Queue 연결(kafka, rabbitMQ), 외부 API 요청 방식 정의(RestTemplate, Feign) 등

  **Infra Layer의 기능**  
  \- DB로의 요청/응답 처리  
  \- Rest API 연결 방식 구현  
  \- 메시지 전송  
  {:.notice-info}


<br>

<div class="post-reference">
  <p>Reference</p>
  <a href="https://empisterian.tistory.com/57">The DDD Layered Architecture</a>
  <a href="https://riiidtechblog.medium.com/gradle과-함께하는-backend-layered-architecture-97117b344ba8">Gradle과 함께하는 Backend Layered Architecture</a>
  <a href="https://tech.junhabaek.net/spring-boot-코드와-함께-보는-백엔드-서버-아키텍처-시리즈-소개-기본-구조-bbf814e1b4e3">Spring 코드와 함께 보는 백엔드 서버 아키텍처</a>
  <a href="https://javacan.tistory.com/entry/94">도메인 로직 패턴 1 - 트랜잭션 스크립트, 도메인 모델</a>
  <a href="https://zdnet.co.kr/view/?no=00000039160910">계층형 아키텍처</a>
</div>