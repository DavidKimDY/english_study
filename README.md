# 영어공부

이 폴더는 영어 **단어·숙어·문장**을 질문하고, 기록으로 남기는 작업 공간입니다.

## 에이전트 역할

질문할 때마다 에이전트는 **아래 순서를 지킵니다.** (먼저 채팅으로 답하고, 마지막에 JSON 저장)

1. **뉘앙스 해석** — 사전 뜻만이 아니라, 맥락·뉘앙스·자주 쓰이는 상황을 쉽게 설명합니다.
2. **외우기 팁** — 연상, 대비, 패턴 등 기억에 남는 방법을 짧게 제안합니다.
3. **예시 문장** — 해당 표현이 자연스럽게 쓰인 영어 예문을 하나 제공합니다.
4. **JSON 저장** (마지막) — 위 내용을 바탕으로 **두 파일 모두**에 같은 항목을 추가합니다.
   - `entries/YYYY-MM-DD.json` (오늘 날짜 파일, 없으면 `{"entries": []}`로 새로 만듦)
   - `entries.json` (전체 통합본)
   아래 프로퍼티 이름을 **항상 동일하게** 사용합니다.

## JSON 저장 형식

파일: `entries/YYYY-MM-DD.json`(날짜별) + `entries.json`(통합본) — 둘 다 같은 형식이며, 항목은 배열 `entries`에 쌓습니다.

웹페이지 `몰랐던 영어`는 `entries.json`의 `asked_at`으로 날짜 목록을 만들고, 날짜를 고르면 `entries/<날짜>.json`을 불러옵니다. 그래서 두 파일이 항상 같은 내용이어야 합니다.

각 항목 객체 프로퍼티 (고정):

| 프로퍼티 | 설명 |
|----------|------|
| `type` | `"word"` \| `"phrase"` \| `"sentence"` |
| `query` | 사용자가 물어본 원문 (단어/숙어/문장) |
| `meaning` | 핵심 뜻 (한국어) |
| `nuance` | 뉘앙스·용법 설명 |
| `memorization_tip` | 외우기 팁 |
| `example_en` | 예시 영어 문장 |
| `example_ko` | 예시 문장 한국어 번역 (선택이지만 가능하면 포함) |
| `asked_at` | ISO 8601 날짜 (예: `2026-10-27`) |

예시:

```json
{
  "entries": [
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
  ]
}
```

## 사용 방법

1. 채팅에서 영단어, 숙어, 문장을 질문합니다.
2. 에이전트가 **먼저** 설명·예문·팁을 채팅으로 답합니다.
3. **그다음** 같은 내용을 날짜 파일과 `entries.json`에 저장합니다.
4. `entries.json`을 열어 복습·암기에 활용합니다.

## 영어 읽기 — 기사 추가

```
articles/
├── index.json                 ← 기사 목록 (위에 있을수록 목록 위에 보임)
└── <id>/article.json          ← 기사 본문 (문단 → 문장 단위)
```

- `<id>`는 영문 소문자·숫자·하이픈만 사용 (예: `1961-jfk-inaugural`).
- 문장은 미리 나눠서 넣습니다. `ko`(해석)는 있으면 넣고, 없으면 생략합니다. 해석이 없는 문장은 화면에서 「해석 보기」 버튼이 사라집니다.
- 재사용 가능한 글(퍼블릭 도메인 등)만 넣습니다.

`article.json` 형식:

```json
{
  "id": "1961-jfk-inaugural",
  "eyebrow": "연설 · 1961년 1월 20일",
  "title": "John F. Kennedy 대통령 취임 연설",
  "meta": ["출처·범위 한 줄", "라이선스 한 줄"],
  "added_at": "2026-11-03",
  "paragraphs": [
    [ { "en": "First sentence.", "ko": "첫 문장 해석." }, { "en": "Second sentence." } ]
  ]
}
```

`index.json`에는 `{ "id", "eyebrow", "title", "summary", "added_at" }`를 추가합니다.

### 폰에서 보낸 저장 목록 처리

`[영어 읽기]`로 시작하는 텍스트를 받으면, 각 항목을 위의 **JSON 저장 형식**에 맞춰 `entries/<오늘>.json`과 `entries.json`에 추가합니다.
- `표현:` → `query`, 함께 온 `문장:` → `example_en`, `해석:` → `example_ko`
- `문장:`만 있는 항목 → `type: "sentence"`, `query`·`example_en` 모두 그 문장
- `meaning`·`nuance`·`memorization_tip`은 문장 맥락에 맞게 작성합니다.
