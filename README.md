# AI_HARNESS_BASIC

AI 코딩 에이전트(Claude Code 등)가 작은 커밋 단위로 작업하도록 강제하는 지침·훅·CI 모음.

> Java + Gradle 프로젝트 기준이다. 커밋·브랜치·PR 규칙은 언어와 무관하지만, 아래 설정은 Java 전용이다.
>
> | 항목 | Java 관련 내용 |
> | --- | --- |
> | [docs/code-style.md](docs/code-style.md) | google-java-format 포맷, Java 네이밍 규칙 |
> | [docs/clean-code-examples.md](docs/clean-code-examples.md) | Java 코드 예시 |
> | [docs/java-checklist.md](docs/java-checklist.md) | Java 클린 코드 체크리스트 (들여쓰기 1단계, else 금지, 일급 컬렉션 등) |
> | [docs/lint-and-ci.md](docs/lint-and-ci.md) | Spotless 설정 (`build.gradle.kts`) |
> | [.githooks/pre-commit](.githooks/pre-commit) | `.java` 스테이징 시 `spotlessCheck` |
> | [.github/workflows/ci.yml](.github/workflows/ci.yml) | JDK 21 + Gradle `spotlessCheck build` |
> | [.coderabbit.yaml](.coderabbit.yaml) | `*.java` 리뷰 기준 |
>
> 다른 언어에 적용하면 위 항목을 해당 언어의 포맷터·빌드 도구로 바꾼다.

## 구성

| 경로 | 내용 |
| --- | --- |
| [AGENTS.md](AGENTS.md) | 에이전트 지침 진입점, 문서 지도 |
| [CLAUDE.md](CLAUDE.md) | Claude Code 용. `AGENTS.md` 를 불러온다 |
| [docs/](docs/) | 작업 흐름, 브랜치·커밋·PR 규칙, 코드 스타일, 문체 |
| [.githooks/](.githooks/) | `pre-commit`(커밋당 파일 수), `commit-msg`(메시지 형식) |
| [.github/workflows/ci.yml](.github/workflows/ci.yml) | Gradle 빌드 |
| [.claude/settings.json](.claude/settings.json) | AI 서명 비활성화, 훅 우회·force push 차단 |
| [.coderabbit.yaml](.coderabbit.yaml) | CodeRabbit 리뷰 설정 |

## 시작하기

clone 후 훅을 1회 설치한다.

```bash
git config core.hooksPath .githooks
```

- 작업 흐름: [docs/workflow.md](docs/workflow.md)
- 훅·린트·CI 상세: [docs/lint-and-ci.md](docs/lint-and-ci.md)

## 다른 프로젝트에 적용

1. `AGENTS.md`, `CLAUDE.md`, `docs/`, `.githooks/`, `.github/`, `.claude/`, `.coderabbit.yaml` 을 복사한다.
2. 훅을 설치한다.
3. 도입 커밋만 한도를 올려 한 번에 커밋한다: `HARNESS_MAX_FILES=99 git commit ...`
4. Gradle 프로젝트면 [docs/lint-and-ci.md](docs/lint-and-ci.md) 의 Spotless 설정을 추가한다.
