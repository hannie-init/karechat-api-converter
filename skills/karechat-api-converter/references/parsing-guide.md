# Parsing Guide

## Spreadsheet Structure

Each API block in the spreadsheet has this layout (rows are tab-separated):

### Header rows (extract these fields)
| Field | Location |
|-------|----------|
| 인터페이스명 | Row 1, col 2 |
| 인터페이스ID | Row 1, col 4 |
| 작성자 | Row 1, col 6 |
| 작성일 | Row 1, col 8 |
| 연계방식 (Method) | Row 4, last value (GET / POST / DELETE) |
| 업무처리 기능설명 | Row 5, col 2 |

### Request items table
Starts after `요청(Request) 인터페이스 항목` header row.
Column order: 순번 / 구분 / 한글명 / 영문명 / 데이터타입 / 길이 / 필수여부 / 구분자 / 부모필드 / 반복여부 / 입력값(예시) / 비고

- **구분 = Header**: 공통헤더 — include as a fixed header row in the MD table, not as a parameter
- **구분 = Param**: query parameter (used in GET requests)
- **구분 = Body**: request body field (used in POST requests)
- **반복여부 = Y**: the field is an array/list type

### Response items tables
Two sections:
1. `응답(Response) 인터페이스 항목 (error 응답시)` — error fields
2. `응답(Response) 인터페이스 항목 (정상 응답시)` — success fields

Merge both into a single response body table in the MD output.
Common error fields: `succeed`, `err_cd`, `err_msg`

### Nested fields (indentation)
Fields with a non-empty 부모필드 column are children of the named parent.
In the MD table, show them with indentation using `&nbsp;&nbsp;` prefix on the field name.
In mock JSON, nest them under their parent object/array.

## Field Extraction Rules

- **영문명**: use as the field key in tables and mock JSON
- **입력값(예시)**: use as the example value in the MD table and mock JSON
- **비고**: append to the 설명 column in the MD table when non-empty
- **길이**: omit from the MD output (not shown in the template)
- Skip rows where 영문명 is blank (e.g., the 공통헤더 row itself — show it as a note, not a field)
