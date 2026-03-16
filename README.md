# karechat-api-converter

KareChat 팀을 위한 Claude Code 커스텀 플러그인입니다.
Google 스프레드시트에서 복사한 API 명세를 Markdown 문서로 자동 변환하고, Notion에 페이지를 생성합니다.

---

## 무엇을 해주나요?

- 스프레드시트(TSV)로 복사한 API 명세 → Markdown 문서 자동 생성
- 요청/응답 파라미터 테이블 및 curl 예시 자동 구성
- 생성된 MD를 Notion API 문서 데이터베이스에 자동 업로드

---

## 설치 방법 (Claude Code Plugin)

### 1. Marketplace 등록

Claude Code에서 아래 명령어를 실행하세요.

```
/plugin marketplace add hannie-init/karechat-api-converter
```

### 2. 플러그인 설치

```
/plugin install karechat-api-converter@karechat-api-converter
```

### 3. 설치 확인

Claude Code에서 아래와 같이 물어보면 스킬이 정상 동작하는지 확인할 수 있어요.

```
인터페이스 설계서 변환해줘
```

---

## 사용 방법

### Step 1 — 스프레드시트에서 데이터 복사

Google 스프레드시트에서 API 명세 영역을 선택 후 복사(Cmd+C)합니다.

### Step 2 — Claude에게 붙여넣기

Claude Code 또는 Claude.ai에서 아래처럼 입력하세요.

```
인터페이스 설계서 변환해줘

[복사한 내용 붙여넣기]
```

또는

```
병원 API 문서 만들어줘

[복사한 내용 붙여넣기]
```

### Step 3 — 결과 확인

Claude가 아래 작업을 순서대로 처리합니다.

1. 스프레드시트 파싱 (인터페이스명, Method, 파라미터 등 추출)
2. Markdown 문서 생성 (요청/응답 테이블 + curl 예시 포함)
3. Notion 데이터베이스에 페이지 자동 생성

---

## 지원 문서 타입

| 타입 | 트리거 키워드 | 필드 네이밍 |
|------|-------------|------------|
| 인터페이스 설계서 (병원) | `인터페이스 설계서`, `병원 api` | snake_case |

---

## 출력 예시

```markdown
## 1. API 소개

**Endpoint** : {baseURL}/api/dfd/v1/hsptlz/form-sign-info-list

**Method** : GET

**Description** : 전자서식 서명 정보 목록을 조회한다.

---

## 2. 요청

### 헤더
| **이름** | **설명** | **필수 여부** |
| --- | --- | --- |
| Content-Type | Content-Type: application/json | 필수 |

### 쿼리 파라미터
| **이름** | **데이터 타입** | **필수 여부** | **설명** | **예시** |
| --- | --- | --- | --- | --- |
| hsp_tp_cd | String | 필수 | 병원 유형 코드 | "001" |

...
```

---

## Notion 연동

생성된 문서는 아래 Notion 데이터베이스에 자동으로 업로드됩니다.

- **데이터베이스**: [API 문서](https://www.notion.so/322d87e517f480029e60e1500a4b06bb)
- **자동 설정 항목**: 이름(인터페이스명), Method, 프론트/병원(병원)

Notion 연동을 위해 Claude에 Notion MCP가 연결되어 있어야 합니다.

---

## 문의

이 플러그인은 KareChat 팀 내부용입니다.
이슈나 개선 사항은 이 레포의 Issues 탭에 남겨주세요.
