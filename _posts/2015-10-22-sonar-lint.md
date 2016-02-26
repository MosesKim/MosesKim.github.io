---
layout: post
title: SonarLint_이슈를 사전에 예방하세요
author: Julien Henry/ Moses Kim (Translation)
date:   2015-10-22 18:00:00
categories: SonarQube
permalink:
tags:
comments: true
#cover: assets/images/151015-change-isnt-free.jpg
---

> 이 글은 [sonarqube blog][sonarqube-web-blog] 블로그에게재된 [SonarLint: Fixing Issues Before They Exist][sonarlint-fixing-issues-before-they-exist]를 번역한 것입니다.
저의 의견과 100% 일치하지 않을 수 있으며, 저작권에 문제가 될 경우 언제든지 삭제될 수 있습니다(저작권 문의 중).

---

SonarSource의 새 제품군인 [SonarLint][sonarlint-link]를 소개하게 되어 매우 기쁩니다. SonarLint를 사용해 여러분은 코드 이슈가 발생하기 전에 앞서서 이슈들을 처리할 수 있습니다.

SonarLint는 코드 품질과 관련된 새로운 접근 방법--즉각적인 이슈의 확인--을 채택했습니다. SonarLint는 IDE와 통합되며 전적으로 개발자에게 편리하도록 만들어졌습니다. 현재 3개의 IDE에서 사용 가능합니다:

* [SonarLint for VisualStudio][sonarlint-for-vs]
* [SonarLint for Eclipse][sonarlibt-for-eclipse]
* [SonarLint for IntelliJ][sonarlint-for-intellij]

SonarLint for VisualStudio v1.x는 C# 언어를 지원하며, SonarLint for Eclipse와 SonarLint for IntelliJ는 PHP, Java 언어를 지원합니다.

향후 우리는 SonarLint와 SonarQube instance와의 연결을 추가할 예정입니다. 기존의 관습을 탈피하고자 하는 작은 생각이 이 새로운 제품을 탄생하게 했습니다. SonarLint와 함께 코드 품질의 새 장을 열어가시기 바랍니다.

* [SonarLint: Fixing Issues Before They Exist][sonarlint-fixing-issues-before-they-exist]를 방문하시면 SonarLint for VisualStudio, SonarLint for Eclipse 제품의 preview demo 영상을 확인하실 수 있습니다.

----
(옮긴이 한마디) 아직은 지원하는 언어가 적지만 SonarQube와 연동이 된다면 더 손쉽고 효과적인 연동을 기대할 수 있을 것 같습니다. 향후 연동 기능이 추가되면 또 한번 소식을 전해드릴게요! :)
<br><br><br>
---

[sonarqube-web-blog]: http://www.sonarqube.org/category/blog
[sonarlint-fixing-issues-before-they-exist]: http://www.sonarqube.org/sonarlint-fixing-issues-before-they-exist/
[sonarlint-link]: http://www.sonarlint.org/index.html
[sonarlint-for-vs]: http://www.sonarlint.org/visualstudio/index.html
[sonarlibt-for-eclipse]: http://www.sonarlint.org/eclipse/index.html
[sonarlint-for-intellij]: http://www.sonarlint.org/intellij/index.html
