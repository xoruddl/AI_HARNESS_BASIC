# AGENTS.md

에이전트 작업 지침의 진입점. 작업 전 이 파일을 읽고, 작업 종류에 맞는 문서를 연다.

## 문서 지도

| 문서 | 읽는 시점 |
| --- | --- |
| [docs/workflow.md](docs/workflow.md) | 모든 작업 시작 전 (필수) |
| [docs/branch-strategy.md](docs/branch-strategy.md) | 브랜치 생성·병합 |
| [docs/commit-convention.md](docs/commit-convention.md) | 커밋 |
| [docs/pull-request.md](docs/pull-request.md) | PR 생성 |
| [docs/code-review.md](docs/code-review.md) | PR 리뷰(CodeRabbit) 확인 |
| [docs/code-style.md](docs/code-style.md) | 코드 작성, 주석 |
| [docs/clean-code.md](docs/clean-code.md) | 코드 작성, 설계 |
| [docs/clean-code-examples.md](docs/clean-code-examples.md) | 코드 작성 시 참고 예시 |
| [docs/java-checklist.md](docs/java-checklist.md) | Java 코드 작성·리뷰 |
| [docs/lint-and-ci.md](docs/lint-and-ci.md) | 훅·린트·CI 설정 |
| [docs/writing-style.md](docs/writing-style.md) | md 문서, 커밋·PR 메시지 작성 |

## 핵심 규칙

1. 커밋 1개 = 파일 1개. 분리하면 빌드가 깨질 때만 최대 3개까지 묶는다.
2. 커밋 1개 후 작업을 멈추고 사용자 피드백을 기다린다.
3. PR 은 한 가지 목적만 담는다.
4. 커밋·PR 메시지는 사람이 쓴 것처럼 짧게 쓴다. AI 서명 금지.
5. 코드에는 의도를 설명하는 주석을 적극적으로 단다.
6. 훅 우회(`--no-verify`) 금지.

## 지침 관리

- 지침 추가·변경 요청은 메모리에 저장하지 않는다. 이 파일이나 `docs/` 에 반영한다.
- 새 문서를 만들면 위 문서 지도에 한 줄 추가한다.
- 문서 수정도 커밋 규칙(1커밋 1파일)을 따른다.
- 문서 문체는 [docs/writing-style.md](docs/writing-style.md) 를 따른다.
