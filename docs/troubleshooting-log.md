# Troubleshooting Log

이 문서는 Git 작업 중 발생할 수 있는 문제를 재현하고 해결한 과정을 기록한다. 각 기록은 상황, 참여자, 명령, 결과, 선택 이유와 협업 시 주의점을 포함한다.

## 참여 현황

| 시나리오 | 실행 담당 | 기록·검토 참여 | 상태 |
| --- | --- | --- | --- |
| `git commit --amend` | 육민우 | 팀원 확인 필요 | 기록 대기 |
| `git reset --soft HEAD~1` | 엄태동 | 팀원 확인 필요 | 기록 대기 |
| `git revert` | 박세헌 | 이주성 | 기록 대기 |
| `git stash / git stash pop` | 정빈 | 정빈 | 완료 |

> amend, reset, revert 기록은 각 담당자가 실제 수행 결과를 확인한 뒤 이 문서에 추가한다. 수행하지 않은 결과를 추정해 작성하지 않는다.

---

## 시나리오 1: git commit --amend

### 참여자

- 실행 담당: 육민우
- 기록·검토: 팀원 확인 필요

### 상태

- [ ] 실제 실습 완료
- [ ] 실행 명령과 결과 기록
- [ ] 협업 시 주의점 확인

### 기록할 내용

- 최근 로컬 커밋의 메시지 또는 내용을 수정한 상황
- `git commit --amend` 실행 전후 커밋 해시와 메시지
- 원격에 공유되지 않은 커밋에서 수행했는지 여부

---

## 시나리오 2: git reset --soft HEAD~1

### 참여자

- 실행 담당: 엄태동
- 기록·검토: 팀원 확인 필요

### 상태

- [ ] 실제 실습 완료
- [ ] 실행 명령과 결과 기록
- [ ] 협업 시 주의점 확인

### 기록할 내용

- 잘못 만든 로컬 커밋을 취소하면서 변경 사항은 유지해야 했던 상황
- `git reset --soft HEAD~1` 전후 `git log --oneline`과 `git status` 결과
- 원격에 push된 커밋에는 reset을 사용하지 않는 이유

---

## 시나리오 3: git revert

### 참여자

- 실행 담당: 박세헌
- 기록·검토: 이주성

### 상태

- [ ] 실제 실습 완료
- [ ] 실행 명령과 결과 기록
- [ ] 되돌리기 커밋 링크 추가

### 기록할 내용

- 원격에 공유된 커밋을 안전하게 취소해야 했던 상황
- 원본 커밋과 `git revert <commit>`으로 생성된 되돌리기 커밋
- 공유 히스토리를 유지하기 위해 reset 대신 revert를 선택한 이유

---

## 시나리오 4: git stash / git stash pop

### 참여자

- 실행 및 기록: 정빈 (jeongbeen, @b0e2)

### 상황

`docs/troubleshooting-log.md` 초안을 작성하던 중, 아직 커밋하지 않은 변경을 보존한 채 `main`으로 이동해 최신 기준 상태를 확인해야 했다.

### 시도한 명령과 절차

```bash
git status --short
git stash push -m "practice: save troubleshooting draft"
git stash list
git switch main
git switch feature/jeongbeen-final-evidence
git stash pop
```

### 결과

- 커밋되지 않은 트러블슈팅 문서 변경이 stash에 임시 보관됐다.
- 작업 트리가 깨끗해져 다른 브랜치로 안전하게 이동할 수 있었다.
- 원래 feature 브랜치로 돌아와 `git stash pop`을 실행하자 변경 내용이 복원됐다.
- pop 이후 적용된 stash 항목은 목록에서 제거됐다.

실제 확인 결과는 다음과 같았다.

```text
stash@{0}: On feature/jeongbeen-final-evidence: practice: save troubleshooting draft
Dropped refs/stash@{0} (02ebc4130b998ccd8d63316c6b784492dbec7e48)
```

`git stash list`를 다시 실행했을 때 항목이 출력되지 않았고, `git status --short`에는 복원된 `docs/troubleshooting-log.md` 수정이 표시됐다.

### 왜 이 방법을 선택했는가

작업이 완성되지 않아 임시 커밋을 만들고 싶지 않았고, 현재 변경을 잃지 않은 채 다른 브랜치로 이동해야 했기 때문이다. stash는 커밋 히스토리에 불완전한 작업을 남기지 않고 작업 디렉터리를 잠시 비울 수 있다.

### 주의할 점

- untracked 파일까지 보관하려면 `git stash -u`를 사용한다.
- `git stash pop` 중 현재 브랜치의 변경과 겹치면 충돌이 발생할 수 있다.
- 중요한 작업은 stash에 장기간 방치하지 않고, 복원 후 정상 반영 여부를 확인한다.
- `git stash list`와 `git stash show -p`로 보관 내용을 확인한 뒤 복원한다.
