---
layout: post
title: SonarAnalyzer; 트릭키한 버그들이 우리를 무섭게 하고 있습니다!
author: Fabrice Bellingard(SonarSource, Posted on April 6, 2016) & Translated by Moses Kim(KSQUG)
date:   2016-04-20 00:00:00
categories: SonarQube
permalink:
tags:
comments: true
# cover: assets/images/151117/151117-sq-5_2_release-01.png
---

> 이 글은 SonarQube 블로그에 게제된 글을 번역한 것입니다([원문보기](tricky-bugs-are-running-scared)).

---

refer:

#SonarAnalyzer for Java: Tricky Bugs are Running Scared

For the past year, the SonarSource team behind the SonarAnalyzer for Java has invested most of its time in developing a [Symbolic Execution](symbolic-execution) engine in order to find the kind of tricky bugs that are almost uncatchable by developers unaided.

지난 한 해동안 'SonarAnalyzer for java'의 개발팀은 [Symbolic Execution](symbolic-execution) engine 개발에 대부분의 시간을 사용했습니다.이 엔진을 사용해서 개발자들이 육안으로는 확인하기 어려운 트릭키한 버그들을 찾아내고자 했습니다.

The SonarAnalyzer for Java’s new symbolic execution engine allows it to statically trace all the execution paths in a piece of code. We’ll probably do a blog post in the near future to explain all the related concepts: Program Point, Program State, Symbolic Value, Control Flow Graph, Stack of Symbolic Values, Constraints on Symbolic Values, … but for the time being let’s just see the engine in action.

SonarAnalyzer for Java의 새로운 suymbolic execution engine을 사용하면 코드의 모든 실행 경로를 고정적으로 추적할 수 있습니다. 관련된 모든 개념을 설명하기 위한 별도의 블로그 포스크를 곧 작성할 예정입니다--Program Point, Program State, Symbolic Value, Control Flow Graph, Stack of Symbolic Values, Contraints on Symbolic Values... 하지만 우선, 개발된 엔진이 어떤 일을 하는지 먼저 소개하는 것이 좋겠습니다.

[symbolic-execution]: https://en.wikipedia.org/wiki/Symbolic_execution

[Example 1](example-1) is a null pointer dereference in the Apache Tika project. The nullability of an object is guessed here from a test done in the code.

[Example 1](example-1)은 Apach Tika project에 존재하는 널 포인터 역참조<sub>null pointer dereference</sub>입니다. 표시된 해당 객체의 null 가능성은 코드에서 테스트 된 결과입니다.

[example-1]: https://nemo.sonarqube.org/issues/search#issues=AVKIlkdZraow0NKfILHC

<img src='http://www.sonarqube.org/wp-content/uploads/2016/03/Apache-Tika-603x500.png'>

[Example 2](example-2) is also an NPE in the Apache Tika project. This time the nullability is due to a badly handled exception.

[Example 2](example-2) 역시 Apache Tika project의 NPE입니다. 이 코드의 경우 null 가능성은 적절하지 못한 방법으로 핸들링 된 익셉션에 의해 발생합니다.

[example-2]: https://nemo.sonarqube.org/issues/search#issues=AVKIlnZbraow0NKfILHG

<img src='http://www.sonarqube.org/wp-content/uploads/2016/03/apache-tika-2-650x367.png'>

[Example 3](example-3) is a useless condition in the Spark project.

[Example 3](example-3)은 Spark project의 불필요한 조건문입니다.

[example-3]: https://nemo.sonarqube.org/issues/search#issues=AVKjAreK1Mhx7iHfg2ON

<img src='http://www.sonarqube.org/wp-content/uploads/2016/03/spark-650x295.png'>

[Example 4](example-4) returns to Apache Tika with a suspect unreachable branch.

[Example 4](example-4)는 Apache Tika project의 코드로 잠재적으로 수행 불가능한 브랜치를 포함하고 있습니다.

[example-4]: https://nemo.sonarqube.org/issues/search#issues=AVFaGnB5poN9iFd28WNf

<img src='http://www.sonarqube.org/wp-content/uploads/2016/03/apache-tika-4-650x451.png'>

Based on those few examples I guess it’s pretty easy to understand how valuable it can be to quickly get this information early in the development lifecycle. So how can you benefit from the SonarAnalyzer for Java? Either by getting on-the-fly feedback directly in your favorite Java editor with [SonarLint for Eclipse](sonarlint-for-eclipse) or [SonarLint for IntelliJ](sonarlint-for-intellij), Or by integrating SonarQube analysis into your build process to continuously feed the SonarQube server.

위에서 설명드린 단순한 몇몇 예시를 통해, 이러한 정보를 개발 초반부터 손쉽게 확인할 수 있음의 가치를 분명히 이해하실 수 있을 것입니다. SonarAnalyzer for Java를 통해서 어떤 이득을 얻을 수 있을까요? 여러분이 익숙한 Java 에디터를 사용한다면 [SonarLint for Eclipse](sonarlint-for-eclipse) 혹은 [SonarLint for IntelliJ](sonarlint-for-intellij)와 연동하여 코드를 작성하는 도중에 즉각적인 피드백을 받을 수 있습니다. 혹은 SonarQube를 여러분의 필드 프로세스와 연결하여 지속적으로 활용할 수도 있을 것입니다.

[sonarlint-for-eclipse]: http://www.sonarlint.org/
[sonarlint-for-intellij]: http://www.sonarlint.org/

Tricky bugs are running scared. The hunt is on!

트릭키한 버그들이 우리를 무섭게 하고 있습니다. 사냥이 시작되었습니다!<br><br>

---

이제 v5.4를 [다운로드][download-sq] 받고 사용해 보십시오. 사용하기 전 반드시 [설치 가이드][installation-guide] 및 [업그레이드 가이드][upgrade-guide]를 확인하시기 바랍니다.
<br><br><br>

---

[tricky-bugs-are-running-scared]: http://www.sonarqube.org/sonaranalyzer-for-java-tricky-bugs-are-running-scared/
[download-sq]: http://www.sonarsource.org/downloads/
[installation-guide]: http://docs.sonarqube.org/display/SONAR/Installing
[upgrade-guide]: http://docs.sonarqube.org/display/SONAR/Upgrading
