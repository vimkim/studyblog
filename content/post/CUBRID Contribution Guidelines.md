+++
title = 'CUBRID Contribution Guidelines'
date = 2024-04-18T07:24:35+09:01
+++

# CUBRID Contribution Guidelines


https://dev.cubrid.org/dev-process/v/dp-en

## Jira Issue 등록

## 이슈 선별 triage

**QA 메인테이너**는 “RESOLVED” 상태인 이슈가 QA 테스트를 통과하지 못했을 경우 “QA Not Satisfied” 버튼을 눌러 “CONFIRMED” 상태로 되돌릴 수 있습니다. 또한, QA 담당자는 해당 이슈가 SPEC 변경이 필요하다고 판단한 경우 “QA Not Satisfied” 버튼을 눌러 “CONFIRMED” 상태로 되돌릴 수 있습니다.

이슈 담당 개발자는 “IN PROGRESS” 상태인 이슈를 더 이상 진행할 수 없을 때 “stop work” 버튼을 눌러 “CONFIRMED” 상태로 되돌릴 수 있습니다.
## 작업 진행

트라이아지를 통해 지정된 개발자(개발자 변경 가능)는 "start work" 버튼을 누른 후 due date를 설정하고 상태를 "IN PROGRESS"로 변경합니다. "IN PROGRESS" 상태에서 개발자는 "Change Status of Dev" 버튼을 눌러 개발 상태를 지정하며, 개발 상태는 분석, POC, 설계, 설계 리뷰, 구현, 테스트로 구성됩니다. 개발자는 진행 중인 개발 단계에 맞춰 상태를 변경해야 합니다. Pull Request 생성 시 Github hook을 통해 JIRA에서 자동으로 "IN PROGRESS" 상태로 변경됩니다.

개발자는 "REVIEW IN PROGRESS" 상태에서 "Propose a change" 버튼을 눌러 "IN PROGRESS" 상태로 되돌릴 수 있습니다. 코드 리뷰 중 발견된 문제가 간단한 수정으로 해결될 수 없고, 분석 또는 설계 단계에서 추가 고려가 필요한 경우 상태를 되돌립니다.

## 작업 리뷰

담당 개발자가 Pull Request를 생성하고, Review 준비가 되었을 경우 “Submit a fix” 버튼을 눌러 “REVIEW IN PROGRESS” 상태로 변경합니다. 해당 Pull Request에 대하여 Review를 완료하고 반영(merge)되면 Github hook을 통해 JIRA에서 자동으로 “REVIEWED” 상태로 변경됩니다.

## 작업 완료

담당 개발자는 리뷰가 완료된 후에 "Check-in Fix" 버튼을 눌러 이슈를 "RESOLVED" 상태로 변경하고, QA 메인테이너에게 이관합니다.

이관된 이후 개발자와 QA 담당자는 코멘트를 통해 소통합니다.

"RESOLVED" 상태로 변경할 때는 Planned Version/s를 확인하여 backport가 반영되었는지 검토해야 합니다.

이 상태로 변경 시 QA assignee는 자동으로 할당되고, resolution은 "Done"으로 설정, 필요한 경우 매뉴얼 수정을 선택하며, QA 시나리오의 필요 여부를 명시해야 합니다. 이슈가 버그가 아니라고 판단될 경우, 프로젝트 메인테이너는 "Bug Invalid" 버튼을 눌러 상태를 변경할 수 있으며, QA 메인테이너가 최종적으로 "CLOSED" 상태로 변경하여 이슈를 종료합니다. 

또한, 수정할 필요가 없다고 판단될 때는 "Resolve without fix" 버튼을 통해 상태를 "RESOLVED"로 변경할 수 있습니다.

### 이슈 종료

- QA 시나리오 추가/수정과 통과 여부
- 백포트 반영 여부

확인

## Workflow with GitHub

## Introduction

### Vincent Drissen 브랜치 모델은 무엇인가?

Vincent Driessen의 브랜치 모델은 "Git Flow"라고도 알려져 있으며, 소프트웨어 개발 프로젝트에서 Git 버전 관리 시스템을 사용할 때 체계적이고 효율적인 방법으로 브랜치를 관리하기 위한 전략입니다.

Git Flow 모델은 다음과 같은 주요 브랜치를 포함합니다:

1. **master 브랜치**: 제품의 공식 릴리스 버전을 관리합니다. master 브랜치는 항상 프로덕션 준비 상태를 유지하며, 여기에서 배포할 수 있는 안정적인 코드만을 포함해야 합니다.
    
2. **develop 브랜치**: 개발의 중심이 되는 브랜치로, 모든 기능 개발 브랜치(feature branches)의 변경 사항이 결합되는 곳입니다. 이 브랜치는 다음 릴리스를 준비하는 데 사용됩니다.
    
3. **feature 브랜치**: 새로운 기능 개발이나 버그 수정을 위해 develop 브랜치로부터 분기하여 생성됩니다. 각 기능 또는 수정 사항이 완료되면 develop 브랜치로 다시 병합됩니다.
    
4. **release 브랜치**: 새로운 프로덕션 릴리스를 준비하는 데 사용됩니다. 이 브랜치는 develop 브랜치에서 분기하여, 릴리스 전에 마지막 테스트와 버그 수정을 수행합니다. 준비가 완료되면 master 브랜치로 병합되고, develop 브랜치에도 변경 사항이 반영됩니다.
    
5. **hotfix 브랜치**: 프로덕션에서 발생하는 긴급한 문제를 해결하기 위해 master 브랜치에서 직접 분기하여 생성됩니다. 문제 해결 후에는 master 브랜치와 develop 브랜치 모두에 병합됩니다.
    
### CUBRID 브랜치 모델과 VD 모델의 차이는 무엇인가?

Vincent Drissen 모델(이하 VD 모델)에서는 영구적으로 유지되는 develop, master 브랜치와 임시 브랜치인 release, feature, hotfix 가 존재합니다. VD 모델과의 차이점은 CUBRID에서는 이전 버전의 릴리즈도 유지보수 하고 있기 때문에 이전 버전의 릴리즈 브랜치도 영구적으로 유지합니다. (e.g. release/10.2, release/11.0) 예를 들어 develop 브랜치에서 최신 버전인 12 버전을 개발하고 있더라도, release/10.2라는 브랜치도 10.2.2, 10.2.3 마이너 버전 릴리즈를 위해 계속 유지합니다.

VD 모델에서 최신 버전 릴리즈 과정에서 임시적으로 생성하는 release 브랜치와 동일한 역할을 하는 pre-release 브랜치를 생성합니다. 자세한 설명은 [Release 섹션](https://dev.cubrid.org/dev-process/rel/release)을 참조합니다.



하나의 Pull Request로 개발을 완료하기 힘든 프로젝트의 경우 피쳐 브랜치를 활용할 수 있습니다. 피쳐 브랜치에 대한 설명은 다음 별도의 섹션에서 기술합니다.

### 백포트 반영이 무엇을 의미하는가?

Backport는 새로운 버전에서 수정된 기능이나 버그를 이전 버전에도 반영하는 과정입니다. 예를 들어, CUBRID 11에서 수정된 버그를 CUBRID 10.2.1 버전에서도 수정하기 위해 backport를 진행합니다. 이 과정에서는 develop 브랜치에 먼저 수정이 반영되고, 검증 후 release 브랜치로 backport합니다. 이는 QA 회귀 테스트를 통한 추가 검증을 통해 이전 버전의 안정성을 유지하는 데 도움을 줍니다. 만약 특정 버그가 develop에서 발생하지 않는 경우, 해당 버그는 release 브랜치에만 반영됩니다.

1. **Develop 브랜치 반영**: 우선 develop 브랜치에 수정 사항을 반영합니다.
2. **안정성 확인**: Develop 브랜치에서의 커밋이 안정적인지 확인합니다.
3. **Cherry-pick 사용**: git cherry-pick 명령을 사용하여 해당 커밋을 release 브랜치로 반영합니다.
4. **Conflict 해결**: Conflict 발생 시 수정 후 PR을 생성합니다.
5. **PR 및 JIRA 기록**: PR 생성 시 develop에서 반영된 PR 번호를 제목에 포함하고, 관련 JIRA 이슈에도 PR 정보와 반영된 버전을 기록합니다.

Backport 과정에서 발생하는 버그는 수정하고 관련 내용을 JIRA에 기록합니다.




