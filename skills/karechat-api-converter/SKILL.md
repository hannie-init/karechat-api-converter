---
name: karechat-api-converter
description: Convert API specification from Google Spreadsheet (TSV/copied text) into Markdown documentation following a specific template. Supports two document types with different field naming conventions. Use when user mentions '인터페이스 설계서', '병원 api', or provides spreadsheet API spec data to convert to Markdown format.
---

# KareChat API Spec Converter

Converts Google Spreadsheet API specifications into Markdown documentation.

## Document Types

| Type | Trigger keywords | Field naming |
|------|-----------------|--------------|
| 인터페이스 설계서 | 인터페이스 설계서, 병원 api | snake_case |

## Workflow

1. **Identify document type** from user's keyword or context
2. **Parse the spreadsheet input** — see `references/parsing-guide.md`
3. **Generate Markdown** — follow the template in `references/md-template.md`
4. Output one MD block per API (one spreadsheet section = one API)

## URL Generation

Interface IDs follow the pattern `DFD-{MODULE}-{SUBPATH}`. Convert to URL:
- Prefix: `{baseURL}/api/dfd/v1/`
- Remaining segments: lowercase, hyphen-separated

Examples:
- `DFD-HSPTLZ-FORM-SIGN-INFO-LIST` → `{baseURL}/api/dfd/v1/hsptlz/form-sign-info-list`
- `DFD-CERTIFIACTE-APPLICATIONS-CERTIFIACTES` → `{baseURL}/api/dfd/v1/certificate/applications/certificates`

If mapping is ambiguous, infer from the interface name (인터페이스명) or ask the user.

## 필수여부 Mapping

| Spreadsheet value | MD output |
|---|---|
| Y | 필수 |
| N | 선택 |
| blank | 조건부 |

## Notion 자동 작성

MD 생성 후 Notion 데이터베이스에 페이지를 자동으로 생성한다.

- **데이터베이스**: API 문서 (https://www.notion.so/322d87e517f480029e60e1500a4b06bb)
- **데이터베이스 ID**: 322d87e5-17f4-804d-a46a-000bead9aecf

### 페이지 생성 시 설정할 properties

| Property | 값 |
|---|---|
| 이름 | 인터페이스명 |
| Method | 연계방식 (GET / POST / DELETE) |
| 프론트/병원 | 병원 |

### 작성 방법

MD 생성 후  툴을 사용해 데이터베이스에 페이지를 생성한다.
페이지 본문은 생성한 MD 내용 전체를 그대로 사용한다.
