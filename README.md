# 자동화 도구 비교 분석 보고서
## Zapier vs Make — KBO 경기 결과 알림 자동화 워크플로우

---

## 목차
1. [프로젝트 개요](#1-프로젝트-개요)
2. [Zapier 구현 — 구성 화면](#2-zapier-구현--구성-화면)
3. [Zapier 구현 — 실행 결과](#3-zapier-구현--실행-결과)
4. [Make 구현 — 구성 화면](#4-make-구현--구성-화면)
5. [Make 구현 — 실행 결과](#5-make-구현--실행-결과)
6. [도구별 구현 과정 요약](#6-도구별-구현-과정-요약)
7. [도구 비교표](#7-도구-비교표)
8. [결론 및 시사점](#8-결론-및-시사점)

---

## 1. 프로젝트 개요

### 1.1 목적
동일한 자동화 워크플로우를 서로 다른 두 개의 노코드 자동화 도구(Zapier, Make)로 각각 구현하고, 구성 방식·사용성·기능적 차이를 비교 분석한다.

### 1.2 구현한 워크플로우
**"KBO 야구 경기 결과 알림 시스템"**

- **트리거**: Google News RSS 피드에서 KBO 경기 결과 관련 새 뉴스 감지
- **처리 1**: 감지된 모든 뉴스를 Google Sheets에 전체 기록 (날짜/제목/링크/내팀여부)
- **처리 2**: 뉴스 제목에 사용자가 지정한 관심 팀(KT 위즈)이 포함되어 있는지 조건 분기
- **액션**: 조건에 해당하는 경우에만 이메일(Gmail)로 알림 발송

이 워크플로우는 트리거 1개 + 조건 분기 1개 + 액션 2개(전체 저장, 조건부 알림)로 구성되어, 두 도구의 노드/모듈 구성 방식과 조건 분기 처리 방식을 비교하기에 적합하다.

---

## 2. Zapier 구현 — 구성 화면

| ① 새 Zap 생성 시작 화면 | ② RSS 트리거 Feed URL 입력 |
|---|---|
| ![새 Zap 생성](images/zapier-01-new-zap-start.png) | ![RSS Feed URL 입력](images/zapier-02-rss-feed-url.png) |

| ③ RSS 트리거 Setup 완료 | ④ 2단계 액션 이벤트 선택 |
|---|---|
| ![RSS Setup 완료](images/zapier-03-rss-setup-done.png) | ![액션 이벤트 선택](images/zapier-04-select-action-event.png) |

| ⑤ Create Spreadsheet Row 설정 | ⑥ Spreadsheet/Worksheet 선택 |
|---|---|
| ![Create Spreadsheet Row](images/zapier-05-create-spreadsheet-row.png) | ![Spreadsheet 선택](images/zapier-06-spreadsheet-worksheet-select.png) |

| ⑦ 컬럼 매핑(날짜/제목/링크) | ⑧ Paths 구조 — Path A/B 분기 |
|---|---|
| ![컬럼 매핑](images/zapier-07-column-mapping.png) | ![Paths 구조](images/zapier-08-paths-structure.png) |

| ⑨ Path 조건(Path conditions) 설정 | ⑩ 액션 앱 선택 (Gmail 등) |
|---|---|
| ![Path 조건 설정](images/zapier-09-path-conditions.png) | ![액션 앱 선택](images/zapier-10-select-app-gmail.png) |

| ⑪ Gmail Send Email — Subject 작성 | ⑫ Gmail Send Email — Body 작성 완료 |
|---|---|
| ![Gmail Subject](images/zapier-11-gmail-subject.png) | ![Gmail Body](images/zapier-12-gmail-body.png) |

---

## 3. Zapier 구현 — 실행 결과

| ⑬ Google Sheets 저장 테스트 성공 | ⑭ Path 조건 테스트 결과 |
|---|---|
| ![저장 테스트 성공](images/zapier-exec-01-sheets-test-success.png) | ![조건 테스트 결과](images/zapier-exec-02-path-filter-test.png) |

**⑮ 실제 저장 결과 — "kbo 경기 결과" 시트에 기록된 실데이터**

![실제 저장 결과](images/zapier-exec-03-sheet-realdata.png)

---

## 4. Make 구현 — 구성 화면

| ① RSS 모듈 — 시작 시점 옵션 선택 | ② Google Sheets 모듈 연결 및 파일 선택 |
|---|---|
| ![시작 시점 옵션](images/make-01-rss-start-option.png) | ![Sheets 연결](images/make-02-sheets-connect.png) |

| ③ Sheet Name 선택 및 헤더 자동 인식 | ④ 전체 시나리오 캔버스 (RSS → Sheets) |
|---|---|
| ![Sheet Name 선택](images/make-03-sheet-name-headers.png) | ![시나리오 캔버스](images/make-04-scenario-canvas.png) |

| ⑤ Router 및 Gmail 계정 연결 | ⑥ Gmail To/Subject/Body type 입력 |
|---|---|
| ![Router Gmail 연결](images/make-05-router-gmail-connect.png) | ![Gmail To Subject](images/make-06-gmail-to-subject.png) |

| ⑦ Gmail Body type 옵션 (Raw HTML만 제공) | ⑧ Gmail Content 작성 완료 |
|---|---|
| ![Body type 옵션](images/make-07-gmail-bodytype.png) | ![Content 작성 완료](images/make-08-gmail-content.png) |

| ⑨ Router 경로 필터(Set up a filter) 설정 | ⑩ 별도 스프레드시트 연결 |
|---|---|
| ![필터 설정](images/make-09-router-filter.png) | ![새 스프레드시트 연결](images/make-10-new-spreadsheet-connect.png) |

---

## 5. Make 구현 — 실행 결과

| ⑪ 실제 저장 결과 — "kbo 경기 결과2" 시트(Make 전용, 신규 파일) | ⑫ 참고 — 원본 "kbo 경기 결과" 시트(Zapier 테스트 누적 데이터) |
|---|---|
| ![Make 실제 저장 결과](images/make-exec-01-sheet-realdata.png) | ![원본 시트 참고](images/make-exec-02-original-sheet-reference.png) |

---

## 6. 도구별 구현 과정 요약

### 6.1 Zapier

| 단계 | 구성 요소 | 비고 |
|---|---|---|
| 1 | RSS by Zapier – New Item in Feed | Google News RSS 연동, Feed URL 직접 입력 |
| 2 | Google Sheets – Create Spreadsheet Row | 전체 뉴스를 "kbo 경기 결과" 시트에 기록 |
| 3 | Paths by Zapier | Path A(내 팀 경기) / Path B(그 외)로 분기 |
| 4 | Path A 조건 | Title Contains "KT 위즈" |
| 5 | Path A 액션 – Gmail: Send Email | 조건 충족 시 이메일 발송 |

**진행 중 겪은 이슈**
- 회원가입 시 "회사 이메일" 입력을 유도하는 화면이 있었으나, 개인 Gmail 계정으로도 가입 가능함을 확인
- RSS 트리거 테스트 시 실제 데이터 대신 더미 샘플("피드 A/B/C")이 표시되는 문제 발생 → Feed URL을 재입력(붙여넣기 방식)하여 해결
- "Create Spreadsheet Row" 대신 유사한 이름의 "Clear Spreadsheet Row(s)" 액션이 잘못 선택되는 경우가 있어 액션 이벤트를 재확인해야 했음
- Paths(조건 분기) 기능은 무료 체험판 기간에만 제공되는 유료 기능이라는 안내가 표시됨

### 6.2 Make

| 단계 | 구성 요소 | 비고 |
|---|---|---|
| 1 | RSS – Watch RSS feed items | 동일한 Google News RSS 연동, "All RSS feed items" 옵션으로 시작 |
| 2 | Google Sheets – Add a Row | 별도 스프레드시트("kbo 경기 결과2")에 전체 기록 |
| 3 | Router | 두 개의 경로(Route)로 분기 |
| 4 | 필터(Filter) 설정 | 경로 연결선에 직접 조건 부여: Title Contains "KT 위즈" (Or 조건: "KT Wiz") |
| 5 | Gmail – Send an Email | 조건 충족 시 이메일 발송 (Body type: Raw HTML) |

**진행 중 겪은 이슈**
- Router는 앱 검색이 아니라 모듈 사이 연결점에서 별도 아이콘으로 추가해야 해서 처음엔 위치를 찾기 어려웠음
- Router 생성 시 자동으로 빈 두 번째 경로가 함께 생성되었으며, 별도 모듈을 연결하지 않아도 실행에 영향이 없음을 확인
- 조건 분기는 Zapier처럼 별도 "Paths" 기능이 아니라 Router + 각 경로에 개별 필터(Filter)를 다는 방식으로 구현
- 이메일 본문(Content) 작성 시 Body type이 "Raw HTML"만 제공되어(Simple text 옵션 없음), 줄바꿈에 `<br>` 태그를 직접 입력해야 했음
- 동일 스프레드시트를 계속 사용할 경우 두 도구의 테스트 데이터가 한 시트에 섞이는 문제가 있어, Make용으로 별도 스프레드시트 파일("kbo 경기 결과2")을 새로 만들어 분리함

---

## 7. 도구 비교표

| 비교 항목 | Zapier | Make |
|---|---|---|
| 회원가입 | 개인 이메일 가입 가능 | 개인 이메일 가입 가능 |
| 자동화 단위 명칭 | Zap | Scenario |
| RSS 트리거 | RSS by Zapier – New Item in Feed | RSS – Watch RSS feed items |
| 조건 분기 방식 | Paths (전용 통합 기능) | Router + 개별 Filter (별도 조합) |
| 분기 UI 직관성 | 조건 설정이 한 화면에 통합되어 비교적 직관적 | Router와 Filter를 따로 다뤄야 해서 처음엔 위치 파악 필요 |
| Google Sheets 연동 | 계정 연결 → 시트/워크시트 선택 → 헤더 자동 매핑, 절차 단순 | 동일하나 "Search Method" 등 옵션이 한 단계 더 있음 |
| 이메일 본문 작성 | Plain 텍스트 방식 지원, 편집 용이 | Raw HTML 방식만 제공, `<br>` 태그 직접 입력 필요 |
| 무료 플랜 제약 | Paths 등 일부 기능이 체험판(Trial) 기간에만 제공된다는 안내 확인 | 무료 플랜 내 Router·Filter 사용 제약 미발견 |
| 테스트 실행 방식 | 각 스텝(Step)마다 개별 Test 버튼 제공 | 전체 시나리오를 한 번에 "Run once"로 실행 |
| 한국어 지원 | 인터페이스 자동 번역 시 일부 오역 발생 (예: "Feed A"→"A 먹이세요") | 관찰 범위 내 유사한 오역 사례 없음 |

---

## 8. 결론 및 시사점

### 8.1 상황별 추천

| 상황 | 추천 도구 | 이유 |
|---|---|---|
| 조건 분기 로직을 빠르고 직관적으로 만들고 싶을 때 | Zapier | Paths 기능이 하나의 화면에 통합되어 초심자도 접근 쉬움 |
| 복잡한 다단계 분기·필터를 세밀하게 제어하고 싶을 때 | Make | Router와 Filter를 독립적으로 조합할 수 있어 유연성 높음 |
| 이메일 본문을 서식 있게 빠르게 작성하고 싶을 때 | Zapier | Plain 텍스트 옵션 제공으로 태그 없이 작성 가능 |
| 무료 플랜에서 조건 분기를 안정적으로 계속 쓰고 싶을 때 | Make | Zapier의 Paths는 체험판 종료 후 유료 전환 가능성 존재 |

### 8.2 결론
두 도구 모두 동일한 워크플로우(RSS 트리거 → 조건부 저장/알림)를 문제없이 구현할 수 있었다. 다만 조건 분기를 다루는 철학에서 뚜렷한 차이가 있었다 — Zapier는 "Paths"라는 하나의 통합 도구로 분기와 조건을 한 번에 처리하는 반면, Make는 "Router(흐름 분기)"와 "Filter(조건 검사)"를 별도의 구성 요소로 분리하여 사용자가 직접 조합하도록 설계되어 있다. 이는 Zapier가 초심자 친화적인 반면, Make는 더 세밀한 커스터마이징이 가능하다는 각 도구의 설계 철학 차이를 보여준다.

---

> 본 보고서에 삽입된 모든 화면은 실제 Zapier 및 Make 계정에서 구현한 워크플로우를 직접 캡처한 증거 자료이다.
