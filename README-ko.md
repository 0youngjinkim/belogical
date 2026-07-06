[English](README.md) | **한국어**

# belogical — AI가 논리적으로 답하게 만드는 스킬

> Answer first. Reasons after.

belogical은 AI가 컨설턴트처럼 답하게 만드는 Claude Code 스킬입니다. 결론을 꼭대기에 놓고, 그 아래를 근거로 받치고, 독자에게 질문이 떠오르는 순서대로 풀어냅니다. 경영 컨설팅이 글쓰기 규율로 삼아 온 바바라 민토의 『논리의 기술』(The Minto Pyramid Principle)을, LLM이 실제로 따를 수 있는 규칙으로 증류했습니다.

이 스킬이 푸는 문제는 이렇습니다. AI는 무엇이든 그 자리에서 길게 써 냅니다. 하지만 읽기는 여전히 사람의 속도입니다. 병목은 쓰기에서 읽기로 옮겨 왔는데, AI의 답변은 아직도 생성한 순서 그대로, 결론을 맨 뒤에 묻은 채 나옵니다. belogical은 그 순서를 매번 뒤집습니다.

`/belogical` 하나로 문서 한 편을 쓰고, 정리 안 된 자료에서 결론을 끌어내고, 이미 있는 글의 논리를 수선하고, 완성된 원문을 대신 읽을 요약으로 압축합니다. 그저 한눈에 들어오는 답이 필요할 때 불러도 좋습니다.

## 요구사항

[Claude Code](https://code.claude.com/docs). 스킬과 플러그인을 지원하는 버전이면 된다.

## 설치

두 가지 방법이 있다. 플러그인 설치를 권장한다.

### 방법 1 — 플러그인 마켓플레이스 (권장)

Claude Code에서 명령 두 줄이면 설치가 끝난다.

```
/plugin marketplace add 0youngjinkim/belogical
/plugin install belogical@belogical
```

설치하면 `/belogical`로 호출할 수 있다. 갱신은 `/plugin marketplace update belogical` 한 줄이면 된다.

### 방법 2 — 수동 복사

`skills/belogical/` 디렉토리를 아래 위치 중 하나에 복사한다. 원칙·라우터·모듈이 한 폴더에 있으므로 이 한 번으로 끝난다.

- `~/.claude/skills/` — 전역. 모든 프로젝트에서 `/belogical`을 쓸 수 있다.
- `<프로젝트>/.claude/skills/` — 해당 프로젝트에서만.

## 사용

`/belogical`을 직접 호출한다. 인자 없이 부르면 라우터가 요청 유형을 판별해 다섯 경로로 나누고, 인자로 경로를 지정하면 곧장 그 경로로 간다.

- `/belogical` — 요청 유형을 판별해 답변·문서·정리·수선·요약 중 하나로 라우팅
- `/belogical 문서` — 독립 문서 작성 (SCQA 도입부 + 피라미드 구축 + 지면 배치)
- `/belogical 정리` — 결론이 서지 않은 자료·생각에서 결론 도출 (상향식 + 로직트리)
- `/belogical 수선` — 기존 글 진단·수선 (역추출 → 진단 → 재배열)
- `/belogical 요약` — 완성된 원문을 대신 읽을 요약으로 압축 (독자 질문 기준 선별, 초과 분량·문서 뭉치는 맵리듀스)

## 두 가지 적용 방식

원칙을 적용하는 방식은 두 가지이고, 함께 써도 된다.

- **호출형(기본)**: `/belogical`을 호출하면 원칙과 라우팅이 함께 로드된다. 이 스킬은 명시 호출 전용이라(frontmatter의 `disable-model-invocation`), 직접 칠 때만 발동하고 "보고서 써줘" 같은 평소 대화에는 끼어들지 않는다.
- **상시형(선택)**: 스킬 호출 없이 모든 대화에 원칙을 적용하고 싶으면, `skills/belogical/SKILL.md`의 `BELOGICAL:PRINCIPLES` 마커 사이 '답변 최상위 원칙' 절만 자신의 전역(`~/.claude/CLAUDE.md`)이나 프로젝트 CLAUDE.md에 붙여넣는다. 원본이 한 곳이므로 갱신할 때 붙여넣은 쪽만 맞추면 된다.

## 구성

원칙 하나와 방법론 일곱으로 이루어진다.

| 파일 | 역할 |
|---|---|
| `skills/belogical/SKILL.md` | 답변 최상위 원칙 + 라우터 — 원칙을 적용하고 요청 유형을 판별해 방법론 모듈로 안내 |
| `skills/belogical/references/` | 방법론 모듈 7개 — 해당 경로에서만 로드 |

원칙과 라우터는 SKILL.md 한 파일에 있다. 스킬을 호출하면 이 파일이 통째로 로드되어 원칙이 먼저 적용된 뒤, 요청에 맞는 방법론 모듈만 얹는다.

```
belogical/
├── README.md
├── README-ko.md
├── LICENSE
├── .claude-plugin/
│   ├── marketplace.json   # 플러그인 마켓플레이스 카탈로그
│   └── plugin.json        # 플러그인 매니페스트
└── skills/
    └── belogical/
        ├── SKILL.md                # 답변 최상위 원칙(마커 절, 상시 적용용 복붙 블록) + 라우터: 요청 판별 → 모듈 로드 → 공통 판정
        └── references/
            ├── build-pyramid.md    # 정상 세우기 — 하향식 5질문 / 상향식 3단계
            ├── scqa-intro.md       # 도입부 설계 — SCQA, 순서 변형, 문서 유형별 골격
            ├── grouping-order.md   # 그룹 묶기와 점검 — 세 규칙, 연역·귀납, MECE, 요약
            ├── page-delivery.md    # 지면·화면 전달 — 30초 규칙, 제목, 프레젠테이션
            ├── thinking-tools.md   # 사고 도구 — 문제 정의, 관계 구조화(로직트리)
            ├── repair-text.md      # 기존 글 수선 — 역추출, 진단, 재배열
            └── exec-summary.md     # 완성 원문 요약 — 정점 재조준, 추출 계약, 드릴다운
```

## 출처

바바라 민토, 『논리의 기술』(The Minto Pyramid Principle). 방법론 어휘와 개념은 원전을 따르되, 원전 문장을 전재하지 않고 핵심 원칙으로 증류해 담았다. 원전이 숫자로 제시한 기준(그룹 4~5개, 30초 등)은 절대 규칙이 아니라 권장 기본값으로 다룬다.

## 라이선스

MIT. 자유롭게 쓰고 고치고 배포할 수 있다. 방법론의 저작권은 원전(바바라 민토)에 있으며, 이 저장소의 라이선스는 여기 담긴 스킬 문서에만 적용된다.
