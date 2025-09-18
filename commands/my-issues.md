---
command: "/my-issues"
category: "Productivity & Planning"
purpose: "나에게 할당된 Jira 이슈 목록 조회"
wave-enabled: false
performance-profile: "optimization"
---

## 목적
현재 사용자에게 할당된 Jira 이슈들을 빠르게 조회하고 현재 작업 상황을 파악

## 사용법
`/my-issues [OPTIONS]`

### 옵션
- `--status [상태]`: 특정 상태의 이슈만 조회 (예: "In Progress", "To Do", "Done")
- `--project [프로젝트키]`: 특정 프로젝트의 이슈만 조회
- `--priority [우선순위]`: 특정 우선순위의 이슈만 조회 (High, Medium, Low)
- `--limit [숫자]`: 조회할 이슈 개수 제한 (기본값: 20)
- `--detailed`: 상세 정보 포함하여 출력

## 실행 단계

### 1단계: JQL 쿼리 구성
1. 기본 JQL: `assignee = currentUser()`
2. 옵션에 따른 필터 조건 추가
3. 정렬: 상태별, 우데이트 시간별 정렬

### 2단계: Jira 조회 실행
1. mcp__mcp-atlassian__jira_search 도구 사용
2. 필수 필드: summary, status, priority, updated, issuetype
3. 상세 모드시 description, assignee 추가

### 3단계: 결과 포맷팅 및 출력
1. 진행 상태별 그룹화
2. 우선순위 아이콘 추가 (🔴 High, 🟡 Medium, 🟢 Low)
3. 상대적 시간 표시 (예: "2시간 전 업데이트")
4. 이슈 키와 요약을 링크 형태로 표시

## 출력 예시

```
📋 내 할당 이슈 (총 8개)

🔄 진행 중 (3개)
├─ 🔴 PROJ-123: 로그인 API 성능 개선 (2시간 전 업데이트)
├─ 🟡 PROJ-124: 사용자 프로필 페이지 리팩토링 (1일 전 업데이트)
└─ 🟢 PROJ-125: 문서 업데이트 (3일 전 업데이트)

📝 할 일 (4개)
├─ 🔴 PROJ-126: 결제 시스템 버그 수정 (방금 업데이트)
├─ 🟡 PROJ-127: 알림 기능 개발 (5시간 전 업데이트)
├─ 🟡 PROJ-128: 검색 기능 최적화 (1일 전 업데이트)
└─ 🟢 PROJ-129: 코드 리뷰 (2일 전 업데이트)

✅ 완료 (1개)
└─ 🟢 PROJ-122: 테스트 코드 작성 (어제 완료)
```

## 자동 활성화
- keywords: "내 이슈", "할당", "작업 목록", "my issues"
- MCP 서버: mcp-atlassian (Jira 통합)
- 성능 최적화: 캐싱 활용, 필요한 필드만 조회