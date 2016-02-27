---
layout: post
title: Build Breaker를 더이상 사용하지 않아야 하는 이유
author: Olivier Gaudin(SonarSource)/ Moses Kim(Translated)
date:   2016-02-26 00:00:00
categories: SonarQube
permalink:
tags:
comments: true
# cover: assets/images/151117/151117-sq-5_2_release-01.png
---

> 2015년 11월 SonarQube 5.2가 릴리즈되었습니다. 당시 SonarQube의 Quality Gate 기능을 활용해 지속적인 통합(Continuous Integration) 서버의 빌드를 깨뜨릴 수 있도록 하는 Build Breaker라는 플러그인의 기능이 삭제 되었습니다. Build Breaker 기능은 많은 커뮤니티 사용자들에게 필수적인 요소였고, 해당 기능의 원복을 간절히 원하는 바램들이 있었는데요... 결과적으로 SonarQube의 개발사인 SonarSource는 공식적으로 더이상 Build Breaker 플러그인에 대한 지원을 하지 않는다고 결정했습니다([원문보기][why-you-should-not-use-build-breaker]).

> 이 글은 SonarQube 블로그에 게제된 글을 번역한 것입니다.

---

2016년 2월 25일, [Olivier Gaudin][oliver-gaudin]가 작성함

최근 커뮤니티를 중심으로 Build Breaker 플러그인과 관련된 뜨거운 논의가 진행되었습니다. SonarSource는 더이상 해당 기능을 유지하지 않기로 했습니다. 커뮤니티에서는 이를 필수적인 기능으로 간주해야 한다고 주장했습니다만... 그래서 이 글을 통해 왜 SonarSource가 해당 기능을 더이상 사용하지 않기로 했는지 설명하고자 합니다.

오래 전, SonarQube 개발팀은 Quality Gate(GQ) 실패와 관련된 알림을 보내는 기능을 원했습니다. SonarQube 플랫폼에서 이메일을 발송할 수 있게 되기 한참 이전의 일이었고, 그 때문에 분석을 트리거링하는 지속적인 통합<sub>Continuous Integration</sub> 시스템을 통해 알림을 보내는 방식을 구현하기로 했습니다. 방법은 매우 간단했습니다: 단지 빌드를 깨뜨리기만 하면 되었죠! 이 기능이 발전하여 Build Breaker 플러그인이 되었고, 완벽하게 동작하는 듯 보였습니다: 사용자는 프로젝트의 지표가 특정 수치의 만족 기준을 설정하고, 분석 결과 측정된 지표가 그 수치를 만족하지 못한다면 QG가 깨지게 됩니다. Build Breaker는 그 깨짐을 확인하고 빌드의 상태를 fail로 반환합니다. CI 엔진은 그 상태 정보를 얻어낸 후, 빌드 job을 실패로 바꾸고 알림을 전달합니다. 정말 멋진 기능입니다!

하지만, 꼭 그렇지만도 않습니다.

우리는 이 기능을 내부적으로 사용하기 시작했고, 처음에는 매우 좋아했습니다. 하지만 머지않아 우리는 몇몇 문제점들을 알게 되었습니다. 가장 주요한 문제는 CI의 Job이 다른 원인으로 인해 적색상태[^footnote1]가 될 수 있다는 것이었습니다: 빌드 자체에 문제가 있을 수 있거나(물리적인 환경이나 설정 문제...) 개발팀에서 고쳐야할 Quality Gate가 실패했기 때문일 수도 있습니다. 즉 빌드 실패의 책임 주체가 이원화 될 수 있다는 것이고, 실제 log를 보지 않는한 어떤 요소가 빌드 실패의 원인인지 파악할 수 없게 된다는 것입니다. 이 상태가 계속되면 빌드 job이 실패하는 경우, 아무도 관심을 가지지 않게 될 수도 있습니다. '그건 다른 사람들의 실수 때문일꺼야'라고 생각하게 될 것이기 때문입니다.

이러한 이유 때문에 우리는 다른 접근 방식을 선택하기로 했고, 개발자들이 그들의 자리에서 볼 수 있는 월보드에 빨간 Quality Gate를 리포트하기로 했습니다.

<img src="{{ site.baseurl }}assets/images/160226/160226-sonarqube-01.png" align="center">

월보드를 사용하면서 우리는 Build Breaker 플러그인의 사용을 중단했습니다. 하지만 여전히 Build Breaker를 사용하는 것은 괜찮은 프랙티스라고 생각했습니다. SonarQube v5.2에서 분석기<sub>Analyzer</sub>와 데이터베이스의 물리적인 연결성이 끊어졌습니다. 그 연결을 끊음으로써 수많은 좋은 점들을 얻어낼 수 있었습니다. 아키텍처상의 중요한 변경도 포함되었습니다: 소스 코드의 분석은 분석기 사이드에서 진행되며, 모든 지표의 계산은 서버 사이드에서 이루어집니다. 다시 말하면, 분석기의 입장에서는 더이상 Quality Gate의 정보를 알 수 없다는 것이 되기도 합니다. 서버만이 그 정보를 알고 있으며, 분석 리포트는 순차적으로 진행되기 때문에 특정 Job의 Quality Gate 결과를 알 수 있게 되기까지는 꽤 시간이 소요될 수 있습니다.

다시 말해, 이러한 관점에서 볼 때 Build Breaker 기능은 더이상 그 구실을 하지 못하게 된다는 것입니다.

이 기능을 지속적으로 사용하는 것은 물론 가능하며, 이를 위해 우리는 서버에 쿼리를 던지는 웹 서비스를 추가했습니다. 하지만 Quality Gate의 결과에 따라 빌드를 깨뜨리는 것은 더이상 새로운 아키텍처에 부합하지 않습니다:
- 분석 리포트가 제출된 이후, 서버에 쿼리를 던져야 합니다
- 그리고 Job이 완료될 때까지 지속적으로--몇 분 간격으로--서버의 응답을 폴링해야 합니다

여러분이 관리하는 CI job은 기존의 비동기화 된 프로세스에서 동기화 된 프로세스로 전환되어야 함을 의미합니다. 별로 좋은 방법이 아닌 것 같지 않은가요? 굳이 Quality Gate를 추가하지 않아도 job이 실패할 수 있는 이유는 이미 너무나 많습니다. 그리고 job이 실패했을 때 역시 다양한 이유가 존재한다는 것을 잊어서도 안 됩니다. 마지막으로 SonarQube 서버에 부하가 많이 걸리는 상황기거나 매우 큰 분석 리포트를 처리하고 있는 경우, CI 엔진에서 막 서브밋 한 프로세스를 처리하는 데 시간이 많이 걸리게 될 것입니다--다시 말해 여러분이 CI 엔진에 수많은 job 실행 리스트를 시작한 경우이겠죠. 다른 CI 엔진들에 대해서는 정확하게 아는 바가 없습니다만, 적어도 Jenkins가 동시에 500개 이상의 job을 실행할 수 있을 것이라 생각하지는 않습니다.

그래서 대안으로 어떤 것들을 할 수 있을까요? 앞서 한가지 예시를 드렸듯, 월보드--SonarSource에서는 Atlassian의 Atlasboard를 사용합니다--를 사용해 Quality Gate 실패 여부를 표시할 수 있습니다. 하지만 다른 모든 알림 시스템에도 비슷한 방식을 적용할 수 있을 것입니다: SonarQube에 쿼리를 던져서 Quality Gate 상태를 얻고 리포트나 알림을 생성할 수 있습니다. Jenkins에서도 동일한 작업을 할 수 있습니다--이 job이 빌드를 실행상태로 유지하도록 하지 않는 한 말입니다. 그리고 SonarQube 서버에도 Quality Gate 실패를 직접 알릴 수 있는 자체적인 알림 시스템을 탑재했습니다..

이상 'SonarSource는 어째서 더 이상 여러분이 Build Breaker를 사용하지 않아야 한다고 생각하는지'에 대해 설명드렸습니다. 물론 community version의 build breaker 플러그인은 여전히 제공될 수 있습니다.

<br><br><br>
---

[why-you-should-not-use-build-breaker]: http://www.sonarqube.org/why-you-shouldnt-use-build-breaker/
[oliver-gaudin]: http://www.sonarqube.org/author/oliviergaudin/

[^footnote1]: 지속적인 통합 서버에서는 빌드가 실패하는 경우 일반적으로 적색 등으로 표시한다.
