# Pull Request

## 생성

```bash
git push -u origin <branch>
gh pr create --base main --title "<커밋 컨벤션 형식>" --body-file <본문 파일>
```

- 본문은 [.github/pull_request_template.md](../.github/pull_request_template.md) 를 채운다.
- 생성 후 PR 링크를 보고하고 멈춘다.

## 제목

- 커밋 컨벤션과 같은 형식. → [commit-convention.md](commit-convention.md)
- 예: `feat(order): 주문 취소 기능 추가`

## 본문

- 변경 내용은 3줄 이내 불릿.
- 변경 파일 나열 금지. diff 에 있다.
- 리뷰어가 꼭 봐야 할 지점만 적는다. 없으면 섹션 삭제.
- 빈 템플릿 섹션은 지운다. "해당 없음" 도 쓰지 않는다.

```
좋음
## 변경
- 주문 취소 시 사유를 저장하도록 필드 추가
- 결제 완료 후 24시간이 지나면 취소 불가

## 확인할 부분
- OrderService.cancel() 의 시간 비교가 서버 타임존 기준인데 괜찮은지

나쁨
## 🚀 개요
이번 PR에서는 사용자 경험 향상을 위해 주문 취소 기능을 종합적으로 구현하였습니다.
```

## 크기

- 커밋 10개, 변경 300줄 이하 권장. 넘으면 PR 을 나눈다.
