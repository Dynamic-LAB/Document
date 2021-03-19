# 협업 규칙

# 1. Commit Message Convention

## 커밋 메시지 기본 Template
```
#{이슈번호} [Label] : Title

Message
```

커밋과 PR에는 이슈번호 Prefix로 붙이기

## Label
- FEATURE : 기능 개발
- FIX : 버그 수정
- VIEW : xml, resource 파일 수정 (코드 이외 파일 추가 또는 수정 시 사용)
- DOCS : 문서 수정 및 추가
- REFACTOR : 리팩토링
- TEST : 테스트 관련 커밋
- ETC : 동작에 영향을 주지 않는 사항

## Title
- 영문으로 작성
- 첫 시작은 대문자
- 변경점에 대한 설명
- 50자 내외로 작성

## Message
- 커밋에 대한 추가 설명
- 커밋 이유 설명
- Title과 Message 사이에 공백 1줄 추가
- 각 줄은 72자 내외로 작성

# 2. Git Flow

## Git Branch
- Master : 출시 가능 상태 브랜치
- Develop : 기능 개발 및 업데이트 반영 브랜치 (코드 통합, 서버 연동 등..)
- Feature : 팀원 각자의 기능 개발 브랜치
- Fix : 개발 완료된 기능의 버그 및 오류 수정 브랜치

## Git Flow
1. 초기 프로젝트 생성 ➞ 완료
2. Develop 브랜치 생성
3. 팀원 각자 Feature 브랜치 생성 후 PR
4. Code Review 진행(컨벤션 준수, 스타일 준수) 후 Develop 브랜치로 Merge

# 3. Project & Issue


# 4. Pull Request


# 5. Code Review & Merge
