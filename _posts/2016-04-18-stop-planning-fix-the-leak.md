---
layout: post
title: 계획은 이제 그만; Leak을 즉시 수정하십시오 ^^
author: Fabrice Bellingard(SonarSource, Posted on April 6, 2016) & Translated by Moses Kim(KSQUG)
date:   2016-04-18 00:00:00
categories: SonarQube
permalink:
tags:
comments: true
# cover: assets/images/151117/151117-sq-5_2_release-01.png
---

> SonarQube v5.3에서 Leak이라는 개념이 도입되었습니다. 과거 New Issues 등의 metric을 통해 이전 분석과 현재 분석 결과 이슈의 증감을 표시하는 기능이 개선된 것인데요. 애로이 발생한 이슈를 최우선으로 수정한다!는 개념을 보다 적극적으로 적용하기 위해 SonarQube v5.5에서 몇몇 기능이 삭제될 예정이라고 합니다. 만남과 헤어짐은 언제는 찾아오는 법이죠 ^^

> 이 글은 SonarQube 블로그에 게제된 글을 번역한 것입니다([원문보기](stop-planning-fix-the-leak)).

---

#계획은 이제 그만; Leak을 즉시 수정하십시오 ^^

여러분은 마침내 SonarQube 플랫폼을 사용하기로 결정했습니다. 프로젝트를 몇차례 분석한 결과 표시된 수많은 이슈를 접하고는 대체 어디에서부터 수정을 시작해야할지 막막하기만 할 것입니다. 그렇다고 해도 홧김에--혹은 열정이 넘친 나머지--이곳저곳 수정을 하지는 마시기를 바랍니다. 그 노력은 물거품이 되기 쉽상일 것이고, 산더미처럼 쌓인 이슈를 처리하는데 금방 지쳐버리게 될 것입니다. 가장 먼저 해야할 일은 개발팀과 **Leak[^footnote1]** 을 우선적으로 처리한다는 것에 합의해야 합니다. 이러한 정책(혹은 약속(은 프로젝트 초기부터 적용해야 합니다. 이 정책을 지켜 나간다면, 여러분의 코드는 시간이 흐름에 따라 업데이트와 리팩토링을 거듭하며 점점 깨끗해질 것입니다.  Leak을 최우선으로 수정한다는 이 새로운 패러다임은 코드 품질 관리에 있어 너무나도 효과적이기 때문에 전통적으로 사용하던 "개선 계획<sub>remediation plan</sub>"을 무용지물로 만들었습니다. 그래서 이와 관련된 기능을 SonarQube v5.5부터 지원하지 않기로 결정했습니다 -- 액션 플랜<sub>action plans</sub> 기능과 이슈를 서드파티 이슈 관리 시스템에 링크하는 기능은 사라지게 될 것입니다.

[^footnote1]: 이전 분석 결과 대비 현재 분석 결과에서 새롭게 발생한 이슈를 별도로 관리하는 기능/패러다임이 SonarQube v5.3부터 적용되었습니다. 이 기능은 이전 New Issues 등으로만 파편적으로 관리되던 정보들을 모아 보다 높은 편의성을 제공하는 방법으로 구현되었습니다.

"도대체 왜 유용한 기능을 또다시 없애버리는건가...?"

사실 SonarSource 팀에서는 위의 기능들을 도입할 당시부터 개밥 먹기<sub>dogfooding</sub>을 시도하며 열심시 사용해 보고자 했습니다만--별 효과를 얻지 못했습니다. 우리가 "Leak[^footnote1]" 패러다임을 개념화하기 훨씬 이전이었음에도 불구하고 이 기능들을 사용하지 않았던 가장 큰 이유는 이미 모든 프로젝트에 설정되어 있는 'Quality Gates' 기능을 통해 새롭게 발생하는 이슈들을 수정했기 때문입니다. 그로 인해 어느 누구도 action plans이나 JIRA에서 이슈를 관리할 필요를 느끼지 않았습니다.

그 외에도 해당 기능들을 사용하지 않아았던 이유들이 있습니다. 먼저 action plans와 관련된 정보는 SonarQube server를 통해서만 접근 가능하기 때문에, 별도의 업무 관리 시스템<sub>task management system</sub>을 사용하고 있다면 해당 정보를 확인하기 어렵습니다. 이로 인해 기껏 설정해 놓은 데드라인<sub>dead-line</sub>도 지나치기 쉽상이었습니다. 이를 보완하기 위해 여러분은 SonarQube의 "link issues" 기능을 활용해 기 사용중인 업무 관리 시스템과 SonarQube의 이슈를 연결하고자 했을 것입니다. 그러나 이 "Link to" 기능은 그동안 전펴 개선되지 못했습니다. 여러분이 업무 관리 시스템으로 JIRA를 사용하고 있다고 가정해보겠습니다. SonarQube의 이슈를 JIRA에 링크시키면, 자동으로 해당 이슈에 대해 티켓[^footnote2]이 생성합니다--만약 100개의 이슈를 JIRA에 연결시킨다면, JIRA에는 별다른 액션을 취할 수 없는 100개의 티켓이 생성될 것이고, 이 티켓들은 SonarQube의 이슈를 식별하는 링크 정보만을 포함하고 있습니다. 그와 함께 여러분의 백로그<sub>Backlog</sub> 역시 지저분해져 버릴 것입니다. 설상가상으로 해당 이슈를 코드에서 수정했을 경우, SonarQube server의 이슈는 완료 처리가 되는 반면 IRA의 티켓은 Open 상태로 남아있습니다. 즉, SonarQube server의 이슈와 JIRA의 티켓은 완전히 동일하지 않기 때문에 별도로 관리해야 하는 상황이 된다는 것입니다.

[^footnote2]: JIRA에서는 하나의 업무를 티켓이라는 단위로 관리합니다.

“Still, there are cases when I really want to create a remediation plan. How can I do that?”

"하지만, 여전히 개선 계획을 수립해야 하는 경우에는 어떻게 할 수 있을까요?"

앞서 이야기한 바와 같이 가급적이면 개선 계획을 수립하지 않아야 합니다. 오히려 **Leak** 이 발생하는 즉시 수정하는 데 집중해야 합니다. 다만 개선 계획의 수립이 피치 못할 경우--아마도 레거시 코드에서 발견된 치명적인 결함이나 위험 요소을 수정해야 하는 경우에 해당할 것입니다--가 있을 것이라 생각합니다. 그러한 상황에서라면 action plans에 의존하기 보다 더 ㅏ은 개선 계획을 수립해서 개발팀과 함께 운영 리스크를 완전히 제거하는 편이 좋을 것입니다.

SonarQube에 이미 포함되어 있는 기능을 사용해 여러분은 수정해야 할 모든 이슈들을 분명하게 식별하고, 그 이슈의 수정 여부를 확인할 수 있는 계획을 명확하게 수립할 수 있습니다 -- 여러분이 어떤 task management system을 사용한다고 해도 말입니다:

1. SonarQube UI에서 다음 작업을 합니다:
  	1. 이슈에 태깅을 하십시오. 태그는 "must-fix-for-v5.2"와 같이 명확하게 의미를 알 수 있어야 합니다.
  	1. 공영으로 접근 가능한 "issue filter"를 생성하고, 이 필터에서는 "must-fix-for-v5.2" 태그가 기록된 이슈들만을 포함시킵니다.
1. 태스크 매니지먼트 시스템에서:
  	1. 1항에서 생성한 issue filter의 URL을 참조하는 링크를 생성합니다.
  	1. due date와 version을 지정합니다.
1. 모든 작업이 완료되었습니다. 이제 여러분은 개선해야 할 모든 이슈의 정보를 가진 완벽한 개선 계획을 세웠습니다. "혹시, 다른 어떤 것이 필요하지 않을까요?"

다른 어떤 것도 필요없습니다. 위의 방식이 가장 최적의 방법입니다. SonarQube에서 개선하고자 하는 이슈들을 식별한 뒤, 여러분이 사용하는 태스크 매니지먼트 시스템에 계획을 수립하면 됩니다.

한번더 말씀드리지만, 여러분의 개발팀이 **Leak** 을 즉즉 수정하는 방식으로 일한다면 더이상의 개선 계획을 수립할 필요가 없을 것입니다. 심지어 Action Plans와 "Link to" 기능을 아주 오래전에 제가 개발했음에도 불구하고, 이제 녀석들과는 작별인사를 해야할 때인 것 같습니다...
<br><br>

---

이제 v5.4를 [다운로드][download-sq] 받고 사용해 보십시오. 사용하기 전 반드시 [설치 가이드][installation-guide] 및 [업그레이드 가이드][upgrade-guide]를 확인하시기 바랍니다.
<br><br><br>

---

[stop-planning-fix-the-leak]: http://www.sonarqube.org/stop-planning-fix-the-leak/
[download-sq]: http://www.sonarsource.org/downloads/
[installation-guide]: http://docs.sonarqube.org/display/SONAR/Installing
[upgrade-guide]: http://docs.sonarqube.org/display/SONAR/Upgrading
