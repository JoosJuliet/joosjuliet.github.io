---
layout: post
section-type: post
title: "git 정책, Rebase vs. Merge"
category: GIT
tags: [ 'git', 'merge', 'rebase' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)


금요일에 회사 내 강의를 듣고 두 방법이 있다는데, 각각은 어떤 특성을 가졌을까 라는 생각을 하게되어서 찾아봤다.

# Rebase vs. Merge: Which Is Better?
## Git Rebase

잠재적으로 복잡한 기록을 간소화합니다.
저장소에 일이 많고, 가지에 일이 많으면 병합 "noise"방지
중간 단계의 커밋을 전부 단일 커밋으로 정리하여  DevOps 개발 팀에 도움이 될 수 있습니다.

## Rebase team policy: definition, pros, and cons
### Pros:
Code history 읽기 쉽고 요약이 잘되있다.
single commit이어서 reverting 하기가 더 편하다.
### Cons:
기능을 소수의 커밋으로 축소하면 전체 개발 내역이있는 이전 branch를 유지하지 않는 한 context로 결정이 된다.
리베이스 (rebase)는 풀 요청에 잘 작동하지 않습니다. 리베이스 (rebase) 된 경우 사용자가 어떤 사소한 변경을했는지 알 수 없기 때문입니다.
리베이스는 위험 할 수 있습니다! 공유 지사의 기록을 다시 작성하면 팀 작업이 중단되는 경향이 있습니다. 이 기능 브랜치의 복사본에서 rebase / squash를 수행하면이 문제를 완화 할 수 있지만 rebase는 역량과주의를 사용해야 함을 의미합니다.
더 많은 작업이 필요합니다.
리베이스 (rebase)를 사용하여 기능 브랜치를 업데이트하려면 유사한 충돌을 반복해서 해결해야합니다.(이부분은 merge가 짱)

원격 브랜치를 사용하여 리베이스하는 또 다른 부수적 인 효과는 언젠가는 강제로 밀어 넣어야한다는 것입니다.



## Git Merge

간단하고 친숙하다.
이력을 전부 보존하고, 시간순으로 보존할 수 있다.
가지의 문맥은 유지한다.



## Merge team policy: definitions, pros, and cons
### Pros:
이력 추적성 (Traceability) :
이는 역사를 남겨 그에 대한 정보를 유지하는 데 도움을 준다
이것은 feature에 대한 모든 commit들을 그룹화 시켜 놓기에 좋다.

### Cons:
<img alt="merge_cons" src = "/images/2019-03-07-Rebase_vs_Merge/merge_cons.png"/>
