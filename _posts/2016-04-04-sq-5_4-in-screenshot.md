---
layout: post
title: 스크린샷으로 보는 SonarQube v5.4
author: G. Ann Campbell(SonarSource)/ Moses Kim(Translated)
date:   2016-04-04 00:00:00
categories: SonarQube
permalink:
tags:
comments: true
# cover: assets/images/151117/151117-sq-5_2_release-01.png
---

> 2016년 3월 9일 비교적 조용하게 SonarQube v5.4가 릴리즈 되었습니다. 지난 2016년 1월 v5.3 릴리즈 이후 근 2개월만의 업데이트입니다. 릴리즈 된 기능에 비해 소박한 릴리즈 공지가 올라왔네요. SonarQube는 IT기업 기준으로 fortune 10대 기업 중 7개, Fortune 100대 기업 중 47개 기업, 전세계적으로 50,000개 이상의 고유 인스턴스가 사용되고 있는 SQ는 명실공히 최고 수준의 정적분석 플랫폼이라 할 수 있을 것 같습니다[^footnote1].

> SonarQube를 제작한 SonarSource에서 공식적인 업그레이드 소식을 전했습니다([원문보기][sonarqube-5-4-in-screenshots]). 이 글은 SonarQube 블로그에 게제된 글을 번역한 것입니다.

---

소나큐브 개발팀은 SonarQube v5.4을 릴리즈하게 된 것을 자랑스럽게 생각합니다. 새로운 버전에는 이전보다 더 유용한 기능들이 많이 추가되었습니다:

- 새로운 "My Account" 스페이스에서 여러분과 관련된 정보를 한꺼번에 표시합니다
- "Execute Analysis" 권한을 프로젝트 레벨에서 설정할 수 있습니다.
- OAuth2를 지원합니다.
- 새로운 "Code" 페이지를 통해 프로젝트의 파일을 표시하고 검색할 수 있습니다.
- 웹 상에서 소나큐브 서버를 재기동할 수 있습니다.
- JavaScript, C# 플러그인이 기본으로 채택되었습니다.
- 모듈 간 중복 검출<sub>cross-module duplication</sub> 기능이 복원되었습니다!
<br><br>

### 새로운 "My Account" 스페이스에서 여러분과 관련된 정보를 한꺼번에 표시합니다.
---

소나큐브 v5.4는 새로운 "My Account" 스페이스를 통해 사용자와 직접적인 관련이 있는 정보를 일목 요연하게 표시합니다:

<img src="{{ site.baseurl }}assets/images/160404/160404-sq54-01.png" align="center">

여러분은 모든 즐겨찾기 항목<sub>favorites</sub>과 개인 이슈 내역들을 하나의 공간에서 확인할 수 있습니다:

<img src="{{ site.baseurl }}assets/images/160404/160404-sq54-02.png" align="center">

또한 개인별 알림<sub>notification</sub>을 설정할 수 있으며:

<img src="{{ site.baseurl }}assets/images/160404/160404-sq54-03.png" align="center">

사용자 계정과 관련된 분석 토큰<sub>analysis token</sub>을 관리할 수 있습니다:

<img src="{{ site.baseurl }}assets/images/160404/160404-sq54-04.png" align="center">

이전 버전까지는 관리자를 통해 분석 토큰을 관리해야 했으나, 이제 여러분이 직접하실 수 있는 환경이 마련되었습니다 ^^
<br><br>

### "Execute Analysis" 권한을 프로젝트 레벨에서 설정할 수 있습니다.
---

"분석 실행<sub>Execute Anlysis</sub>" 권한을 프로젝트 레벨에서 설정할 수 있습니다. 단지 한 프로젝트의 코드 품질을 분석하기 위해 시스템의 모든 권한을 가질 필요가 없습니다:

<img src="{{ site.baseurl }}assets/images/160404/160404-sq54-05.png" align="center">
<br><br>

### OAuth2를 지원합니다.
---

v5.4부터 OAuth2를 지원합니다. GiuHub와 BitBucket용 플러그인이 이미 준비되어 있습니다.

<img src="{{ site.baseurl }}assets/images/160404/160404-sq54-06.png" align="center">

플러그인을 설치한 이후 'Administration > General > Security > [Provider]"에서 관련 환경을 설정할 수 있습니다.
<br><br>

### 새로운 "Code" 페이지를 통해 프로젝트의 파일을 표시하고 검색할 수 있습니다.
---

Component 페이지는 새로운 "Code" 페이지로 대체되었습니다. 새로운 코드 페이지에서는 더욱 자연스러운 코드 탐색을 경험할 수 있습니다. 추가적으로 프로젝트 범위에 한정된 검색 기능도 제공합니다:

<img src="{{ site.baseurl }}assets/images/160404/160404-sq54-07.png" align="center">
<br><br>

### 웹 상에서 소나큐브 서버를 재기동할 수 있습니다.
---

소나큐브를 관리하는 모든 사용자가 파일 시스템에 직접적인 접근 권한을 가지고 있지 않을 수 있기 때문에, 웹 UI를 통해 소나큐브 서버를 재시동하는 기능을 추가했습니다. Update Center 페이지의 우측 상단에 해당 기능을 수행하는 버튼을 제공합니다.

<img src="{{ site.baseurl }}assets/images/160404/160404-sq54-08.png" align="center">
<br><br>

### JavaScript, C# 플러그인이 기본으로 채택되었습니다.
---

V5.4 이후 버전부터 JavaScript, C# 언어 플러그인이 Java, Git, SVN 플러그인과 함께 기본 플러그인으로 제공됩니다.

<img src="{{ site.baseurl }}assets/images/160404/160404-sq54-09.png" align="center">
<br><br>

### 모듈 간 중복 검출<sub>cross-module duplication</sub> 기능이 복원되었습니다!
---

스크린샷으로 보일만한 내용이 충분하지는 않으나, 모듈 간 중복 검출<sub>cross-module duplication</sub> 기능이 복원되었다는 소식도 꼭 전해드려야할 것 같습니다. 이 기능은 v5.2에서의 내부적인 큰 변화에 의해 코드를 완전히 새로 작성해야 하는 상황이 되면서 삭제되었던 기능입니다. v5.3에서는 프로젝트 간 중복 검출<sub>cross-project duplication</sub> 기능이 복원되었고, v5.4에서 비로소 모듈 간 중복 검출<sub>cross-module duplication</sub> 기능을 복원했습니다.
<br><br>

### 자 이제 모두 설명드린 것 같습니다!

---

이제 v5.4를 [다운로드][download-sq] 받고 사용해 보십시오. 사용하기 전 반드시 [설치 가이드][installation-guide] 및 [업그레이드 가이드][upgrade-guide]를 확인하시기 바랍니다.
<br><br><br>
---

[sonarqube-5-4-in-screenshots]: http://www.sonarqube.org/sonarqube-5-4-in-screenshots/
[download-sq]: http://www.sonarsource.org/downloads/
[installation-guide]: http://docs.sonarqube.org/display/SONAR/Installing
[upgrade-guide]: http://docs.sonarqube.org/display/SONAR/Upgrading

[^footnote1]: SonarQube User Conference 2015 통계 기준.  http://www.sonarqube.org/mainstream-noun-the-principal-or-dominant-course-tendency-or-trend/
