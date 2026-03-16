# MD Output Template

Use this exact structure for each API. One API = one complete block.

---

## 1. API 소개

**Endpoint** : {baseURL}/api/dfd/v1/{path}

**Method** : {GET | POST | DELETE}

**Description** : {업무처리 기능설명}

---

## 2. 요청

### 헤더

| **이름** | **설명** | **필수 여부** |
| --- | --- | --- |
| Content-Type | Content-Type: application/json 요청 데이터 형식 | 필수 |

### 쿼리 파라미터  ← (GET only; replace with "### 본문" for POST)

| **이름** | **데이터 타입** | **필수 여부** | **설명** | **예시** |
| --- | --- | --- | --- | --- |
| {영문명} | {데이터타입} | {필수여부} | {한글명} {비고} | "{입력값(예시)}" |

### 예시

**GET** — curl with query string:
```
curl --location --request GET '{baseURL}/api/dfd/v1/{path}?{param1}={val1}&{param2}={val2}'
```

**POST** — curl with JSON body:
```
curl --location '{baseURL}/api/dfd/v1/{path}' \
--data '{
    "{field1}": "{val1}",
    "{field2}": "{val2}"
}'
```

---

## 3. 응답

### 본문

| **이름** | **데이터 타입** | **필수 여부** | **설명** | **예시** |
| --- | --- | --- | --- | --- |
| succeed | String | 필수 | 성공 여부 | "true" : 성공 / "false" : 실패 |
| err_cd | String | 조건부 | 에러 코드 | "EBCOM001" |
| err_msg | String | 조건부 | 에러 메세지 | "데이터를 조회하는 동안 에러가 발생했습니다." |
| data | Object/String | 필수 | 데이터 정보 | |
| {child_field} | {타입} | {필수여부} | {설명} | "{예시}" |

### 예시

- 성공 (200 OK)

```json
{
    "succeed": "true",
    "err_cd": null,
    "err_msg": null,
    "data": {
        // 정상 응답 필드들 (입력값(예시) 기반으로 생성)
        // List 타입은 배열로, 원소 2개 예시 포함 (마지막 원소는 ... 생략 표기)
    }
}
```

- 실패 (200 OK)

```json
{
    "succeed": "false",
    "err_cd": "EBCOM001",
    "err_msg": "데이터를 조회하는 동안 에러가 발생했습니다.",
    "data": {}
}
```

---

## Mock Data Generation Rules

### Request mock (curl 예시)
- Use 입력값(예시) as the value; if blank, generate a plausible example
- For List/array body fields, show as JSON array with 1–2 representative objects

### Response mock (성공 예시)
- Populate all Y(필수) fields with 입력값(예시) values
- Set N(선택) fields to realistic values or null
- Set 조건부 fields to null unless context makes a value obvious
- For List types: include 2 array items with slightly varied values; add `...` comment after
- Wrap all response fields inside `"data": { ... }` when the spec has a `data` parent field

### camelCase conversion (프론트 설계서 only)
Convert all snake_case field names to camelCase in both tables and mock JSON:
- `hsp_tp_cd` → `hspTpCd`
- `pt_mpi_key` → `ptMpiKey`
- `certificate_list` → `certificateList`
