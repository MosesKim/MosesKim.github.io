---
layout: post
title: SonarQube | 중복 코드를 방지하세요
author: Moses Kim
date:   2015-04-28 05:00:00
categories: SonarQube
permalink:
tags:
comments: true
cover: assets/images/150428-duplication-01.png
---

일부 사람들은 코드 중복<sub>duplication</sub>이 가장 나쁜 코딩의 하나라고 말합니다. 코드 중복은 다른 여러가지 문제들을 일으키는 주범이기 때문입니다. 어디선가 복사해서 붙인 코드 블록은 해당 코드에 포함되어 있는 버그, 혹은 잠재적인 버그들을 그대로 새롭게 복사하기 때문입니다.
소나큐브는 내장된 자체 copy/paste 탐지 엔진을 사용하여 다음과 같은 코드 중복을 검출합니다:

* 한 소스파일 내의 코드 중복
* 한 프로젝트 내의 여러 파일 사이의 코드 중복
* 한 프로젝트 내의 여러 모듈 사이의 코드 중복
* 여러 프로젝트 사이의 코드 중복

소나큐브는 “Type 2″ 중복 검출을 수행합니다. Type 2 중복 검출이란 구조적/의미적으로 동일한 중복을 검출하는 것으로 단순한 문자열이나 주석의 중복은 검출범위에서 제외합니다.
중복 코드는 다음 조건을 만족하는 경우 검출됩니다.

* 최소 100회 이상 연속적으로 중복되는 토큰[^footnote1]이 최소 10 라인의 코드[^footnote2]내에서 발견될 경우

다만 Java 프로젝트의 경우에는 토큰이나 코드 라인의 수와 관계없이 10개의 구문이 연속적으로 동일하게 나타나는 경우 중복으로 표시됩니다.
<br><br>

#### 코드 중복을 확인하려면

소나큐브 대시보드에 ‘Duplications’ 위젯을 추가합니다.

<img src="{{ site.baseurl }}assets/images/150428-duplication-02.jpg" border="0">

각 지표의 링크를 클릭하면 component viewer에서 코드 중복을 확인할 수 있습니다.

<img src="{{ site.baseurl }}assets/images/150428-duplication-03.jpg" border="0">
<br><br>

#### 상이한 모듈, 혹은 상이한 프로젝트 중복 검출을 위한 설정

기본적인 코드 중복 검출 범위는 다음과 같습니다:

* 표준 프로젝트: 분석 대상 프로젝트
* 다중 모듈 프로젝트: 분석 대상 모듈

상이한 프로젝트를 대상으로 코드 중복을 검출하기 위해서는 다음과 같이 설정합니다.

1. 시스템 관리자로 로그인합니다.
2. Setting > General Settings > General > Duplication에서 ‘Cross project duplication detection property’ 값을 ‘true’로 설정합니다.

<img src="{{ site.baseurl }}assets/images/150428-duplication-08.png" border="0">
3. 이후 해당 프로젝트를 재 분석합니다.

동일 프로젝트 내의 상이한 모듈에 존재하는 코드 중복을 검출하기 위해서는 다음과 같이 설정합니다:

1. 시스템 관리자로 로그인합니다.
2. 대상 프로젝트를 선택한 후 Configuration > General > Duplications’에서 ‘Cross project duplication detection property’ 값을 ‘true’로 설정합니다.
3. 이후 해당 프로젝트를 재 분석합니다.
<br><br>

#### 샘플 프로젝트

다음과 같이 구성된 프로젝트에서 duplication의 동작을 확인할 수 있습니다.

* 두 개의 프로젝트
* 프로젝트 1은 One.java, 프로젝트 2는 One.java, Two.java를 포함함
* 프로젝트 1의 One.java, 프로젝트 2의 One.java, Two.java는 각 10여 줄의 코드 라인 중복을 가지고 있음
* SonarQube 5.1, Maven 시스템을 통해 분석

<figure>
<img src="{{ site.baseurl }}assets/images/150428-duplication-04.png" border="0">
<figcaption align="center">[프로젝트 1에서 코드 중복을 검출한 결과]</figcaption>
</figure>

<figure>
<img src="{{ site.baseurl }}assets/images/150428-duplication-05.png" border="0">
<figcaption align="center">[프로젝트 1의 one.java]</figcaption>
</figure>

<figure>
<img src="{{ site.baseurl }}assets/images/150428-duplication-06.png" border="0">
<figcaption align="center">[프로젝트 2의 one.java]</figcaption>
</figure>

<figure>
<img src="{{ site.baseurl }}assets/images/150428-duplication-07.png" border="0">
<figcaption align="center">[프로젝트 2의 two.java]</figcaption>
</figure>
<br><br><br>

---
[^footnote1]: sonar.cpd.${language}.minimumTokens 속성으로 설정 가능
[^footnote2]: sonar.cpd.${language}.minimumLines 속성으로 설정 가능
