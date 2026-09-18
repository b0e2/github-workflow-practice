# Interactive Rebase Practice

## 목적

개인 feature 브랜치에서 여러 문서 커밋을 `git rebase -i`로 정리하고, 정리 전후의 히스토리를 비교한다.

## 실습 브랜치

- `feature/jeongbeen-final-evidence`

## 실습 절차

1. 관련 내용을 세 개의 작은 커밋으로 나누어 작성한다.
2. 정리 전 `git log --oneline` 결과를 저장한다.
3. `git rebase -i HEAD~3`에서 두 커밋을 `squash`한다.
4. 최종 커밋 메시지를 작업 전체가 드러나도록 수정한다.
5. 정리 후 히스토리를 다시 확인한다.

## 안전 수칙

- `main`과 공유 브랜치에서는 히스토리를 재작성하지 않는다.
- 원격에 push하기 전의 개인 feature 브랜치에서만 수행한다.
- 이미 공유한 커밋을 rebase했다면 강제 push가 필요할 수 있으므로 팀 합의 없이 진행하지 않는다.
- 충돌이 발생하면 변경 목적을 확인하고 해결한 뒤 `git rebase --continue`를 사용한다.
