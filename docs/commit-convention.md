# 커밋 컨벤션

Conventional Commits 형식. 제목은 한글.

## 형식

```
<type>(<scope>): <제목>

<본문 - 선택>
```

## type

| type | 용도 |
| --- | --- |
| `feat` | 기능 추가 |
| `fix` | 버그 수정 |
| `refactor` | 동작 변경 없는 구조 개선 |
| `test` | 테스트 추가·수정 |
| `docs` | 문서 |
| `style` | 포맷만 변경 |
| `build` | 빌드 설정, 의존성 |
| `ci` | CI 설정 |
| `chore` | 그 외 잡무 |

## 제목

- 50자 이내, 마침표 없음.
- 무엇을 바꿨는지 쓴다. "~ 추가", "~ 수정", "~ 제거" 로 끝낸다.
- `scope` 는 도메인·모듈 이름. 없으면 생략.

## 본문

- 제목만으로 이유가 안 보일 때만 쓴다.
- 왜 바꿨는지 1~3줄. 어떻게 했는지는 diff 가 보여준다.

## 예시

```
좋음
feat(order): 주문 취소 사유 필드 추가
fix(auth): 토큰 만료 시 무한 리다이렉트 수정

결제 페이지에서 만료 토큰으로 재진입하면 /login 과 /pay 를 반복함.

나쁨
feat: 주문 기능 개선 및 코드 품질 향상          ← 모호함
fix(auth): 인증 로직의 안정성을 강화했습니다.   ← 서술형, 마침표
update                                        ← 형식 없음
```

## 금지

- AI 서명: `Co-Authored-By: Claude`, `Generated with Claude Code`, 🤖
- 이모지, 과장 수식어 → [writing-style.md](writing-style.md)
- 제목에 파일명 나열

`.githooks/commit-msg` 가 형식·길이·AI 서명을 검사한다.
