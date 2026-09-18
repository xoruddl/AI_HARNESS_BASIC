# 훅 · 린트 · CI

## Git 훅

설치 (clone 후 1회):

```bash
git config core.hooksPath .githooks
```

| 훅 | 검사 |
| --- | --- |
| `pre-commit` | 스테이징 파일 수 ≤ `HARNESS_MAX_FILES` (기본 1), `gradlew` 있으면 `spotlessCheck` |
| `commit-msg` | 커밋 컨벤션 형식, 제목 50자, 마침표, AI 서명 |

- 빌드가 깨져서 묶어야 할 때만: `HARNESS_MAX_FILES=2 git commit ...` (최대 3)
- 하네스 최초 도입 커밋만 예외: `HARNESS_MAX_FILES=99`
- `--no-verify` 금지.

## 린트 (Spotless + google-java-format)

프로젝트에 Gradle 을 붙일 때 `build.gradle.kts` 에 추가한다.

```kotlin
plugins {
    java
    id("com.diffplug.spotless") version "8.10.2"
}

spotless {
    java {
        target("src/**/*.java")
        googleJavaFormat("1.36.1")
        removeUnusedImports()
        trimTrailingWhitespace()
        endWithNewline()
    }
}
```

| 명령 | 용도 |
| --- | --- |
| `./gradlew spotlessApply` | 포맷 적용 |
| `./gradlew spotlessCheck` | 포맷 검사 (훅, CI) |

## CI

[.github/workflows/ci.yml](../.github/workflows/ci.yml)

| job | 실행 | 검사 |
| --- | --- | --- |
| `build` | PR, main push | `spotlessCheck build`. `gradlew` 없으면 건너뜀 |

- 커밋 규칙(파일 수, 메시지 형식)은 CI 에서 검사하지 않는다. 로컬 훅만 검사한다.
- 버전을 올릴 때는 이 문서의 스니펫과 CI 를 같이 고친다.

## 에이전트 설정

[.claude/settings.json](../.claude/settings.json)

- 커밋·PR 의 AI 서명(Co-Authored-By 등) 비활성화
- 훅 우회, force push, main 직접 push 명령 차단
