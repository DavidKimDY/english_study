# entries.json 프로퍼티

`entries.json`의 `entries` 배열에 들어가는 **각 객체**의 필드 설명입니다.

| 프로퍼티 | 타입 | 설명 |
|----------|------|------|
| `type` | string | 항목 종류. `"word"` · `"phrase"` · `"sentence"` 중 하나. |
| `query` | string | 사용자가 물어본 원문(단어·숙어·문장). 학습 카드의 앞면 역할. |
| `meaning` | string | 핵심 뜻(한국어). |
| `nuance` | string | 뉘앙스·용법·자주 쓰이는 상황. 사전 뜻만으로 부족한 맥락. |
| `memorization_tip` | string | 외우기 팁(연상·대비·패턴 등). |
| `example_en` | string | 해당 표현이 자연스럽게 쓰인 영어 예문. |
| `example_ko` | string | `example_en`의 한국어 번역. |
| `asked_at` | string | 질문(기록)한 날짜. ISO 8601 날짜(`YYYY-MM-DD`). |

## 예시

```json
{
  "type": "phrase",
  "query": "on the fence",
  "meaning": "결정을 못 내리고 망설이는",
  "nuance": "울타리 위에 앉아 있다는 그림에서, 어느 쪽으로도 기울지 않은 상태.",
  "memorization_tip": "fence(울타리) — 찬반 사이 ‘중간’에 서 있다고 연상.",
  "example_en": "I'm still on the fence about moving to Seoul.",
  "example_ko": "서울로 이사할지 아직 결정을 못 했어.",
  "asked_at": "2026-10-27"
}
```
