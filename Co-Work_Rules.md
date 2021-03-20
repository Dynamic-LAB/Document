# 협업 규칙

# 1. Commit Message Convention

## 커밋 메시지 기본 Template
```
{#이슈번호} [type] : subject

body

footer
```

- 한글로 작성 가능
- 커밋과 PR은 가능한 작은 단위로 할 것
- 커밋과 PR에는 이슈번호 Prefix로 붙이기

## Issue Number
GitHub 이슈 번호 붙이기

## Type
타입은 타이틀에 포함되고 아래 중 하나로 구성
- feat : 기능 개발
- fix : 버그 수정
- style : 코드 포맷팅, 세미콜론 누락 등 코드 변경이 없는 경우, xml, resource 파일 수정
- docs : 문서 관련
- refactor : 코드 리팩토링
- test : 테스트 코드
- chore : 빌드 업무 수정, 패키지 매니저 수정, 기타 코드 변경이 아닌 경우

## Subject
- 제목은 50자 이내로 작성
- 명령조로 작성
- 마침표를 붙이지 않는다
- 변경점에 대한 요약

## Body
- 커밋에 대한 추가 설명, 커밋 이유 설명
- How 보단 What, Why
- Subject와 Body 사이에 공백 1줄 추가
- 각 줄은 72자 내외로 작성

## Footer
이슈 트래커 ID를 적을 때 사용

# 2. Git Flow
![image](https://user-images.githubusercontent.com/58630483/111866498-3832c480-89b1-11eb-8590-c03282499b3f.png)

## Branch
- master : 배포되었거나 배포될 소스가 저장되는 브랜치
- develop : 다음 배포를 위한 개발을 진행하는 브랜치
- feature : 팀원 각자에 의해 기능 단위 개발이 진행되는 브랜치
- hotfix : 배포 버전에 생긴 문제로 긴급한 트러블슈팅이 필요할 때 개발이 진행되는 브랜치
- release : 내부적으로 배포할 준비가 되었다고 생각되는 소스가 저장되는 브랜치

## Flow
1. master 브랜치에서 시작
2. develop 브랜치 생성 -> 여기에서 개발 진행
3. 기능 구현은 develop 브랜치에서 feature 브랜치를 생성하여 진행
4. 완료된 feature 브랜치는 검토 후 develop 브랜치에 합친다.(Merge)
5. 모든 기능 구현이 완료되면 develop 브랜치를 release 브랜치로 만든다.
6. 버그 수정 및 QA 진행
7. release 브랜치를 master 브랜치와 develop 브랜치로 보낸다.
8. master 브랜치에서 버전 추가를 위해 태그를 생성하고 배포
9. 배포 후 발생되는 버그는 hotfix 브랜치에서 수정 후 배포

# 3. Project & Issue

## Issue
새로 개발할 기능, 수정할 기능, 버그 수정 등 모든 것이 이슈 단위로 관리<br/>
모든 활동들에 대해서 이슈를 등록하고 이슈 기반으로 작업 진행

## Issue Template
sinsungo-android/.github/ISSUE_TEMPLATE 참고

## Project
- Todo : issue가 만들어지면 자동 등록
- In Progress : PR 시 자동 등록
- Done : Merge 후 상태

# 4. Pull Request & Merge

## PR Template
sinsungo-android/.github/PULL_REQUEST_TEMPLATE.md 참고

## PR Label
Pull Request에 라벨 붙이기
- Developing : PR은 만들었지만 개발중
- Review Needed : 개발 완료 후 리뷰 필요
- Answer for Review : 리뷰 완료 후 피드백 반영
- In Review : 리뷰 진행 중
- Merge Needed : Merge 대기 중
- Simple : 리뷰가 필요없는 간단한 PR -> 올린 사람이 바로 Merge
- Reviewer Name : 리뷰어 등록
- Meeting Needed : PR에 대한 회의 필요
- Stand By : 특정 이유로 진행하지 않고 대기

## Review
기능 개발자 이외의 사람이 리뷰 담당
- 코딩 컨벤션 준수 여부
- 클린 아키텍처 적용
- 빌드
- 실행
- 테스트

### 리뷰어 짝


### Feedback
리뷰 진행 중 수정사항 또는 버그 발생 시 피드백 등록
- 수정사항
- 버그

## Merge
PR에 대해 리뷰가 끝나면 Merge 진행
