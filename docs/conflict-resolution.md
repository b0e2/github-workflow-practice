# Conflict Resolution Log

## 충돌 기록 #1: CONTRIBUTING 협업 규칙 병합

### 1. 기본 정보

- 발생 날짜: 2026-09-17
- 충돌 파일: `docs/CONTRIBUTING.md`
- 현재 브랜치: `feature/taedong-code-review-guide`
- 병합한 브랜치: `origin/main`
- 충돌 해결자: 엄태동 박세헌
- 관련 팀원: 육민우
- 관련 PR: [PR #9](https://github.com/gitflow-practice-team/github-workflow-practice/pull/9)
- 해결 커밋: 

### 2. 충돌 상황

`feature/taedong-code-review-guide` 브랜치는 기존 `main`의  
`3. Issue 기반 작업` 다음 위치에 아래 내용을 추가했다.

- 7. 코드 리뷰 규칙
- 8. 리뷰 반영 규칙
- 9. 코드 리뷰 참여 기준

브랜치를 생성한 이후 최신 `main`에도 같은 위치에 다음 내용이 추가됐다.

- 4. 커밋 메시지 컨벤션
- 5. Pull Request 규칙
- 6. Pull Request 병합 조건

두 브랜치가 동일한 파일의 동일한 삽입 위치를 각각 수정했기 때문에  
Git이 두 변경 사항의 배치 순서를 자동으로 결정하지 못해 충돌이 발생했다.

### 3. 충돌 재현 절차

현재 feature 브랜치에서 최신 `main`을 가져와 병합했다.

```bash
git switch feature/taedong-code-review-guide
git fetch origin
git merge origin/main
```

다음과 같이 `docs/CONTRIBUTING.md`에서 충돌이 발생했다.

```text
Auto-merging docs/CONTRIBUTING.md
CONFLICT (content): Merge conflict in docs/CONTRIBUTING.md
Automatic merge failed; fix conflicts and then commit the result.
```

충돌 상태는 다음 명령으로 확인했다.

```bash
git status
```

### 4. 실제 충돌 내용

충돌 내용의 일부는 다음과 같았다.

```text
<<<<<<< feature/taedong-code-review-guide
## 7. 코드 리뷰 규칙

코드 리뷰는 단순히 오류를 찾는 과정이 아니라
팀원 간에 구현 의도를 공유하는 과정으로 진행합니다.

...
=======
## 4. 커밋 메시지 컨벤션

커밋 메시지는 다음 형식을 사용합니다.

...
>>>>>>> main
```

- Current Change: `feature/taedong-code-review-guide`에서 추가한 7~9번 내용
- Incoming Change: 최신 `main`에서 추가된 4~6번 내용

![CONTRIBUTING 충돌 발생 화면](images/conflict-1/conflict-before.png)

### 5. 비자명 충돌로 판단한 이유

이번 충돌은 같은 파일의 같은 hunk를 양쪽 브랜치에서 수정하여 발생했다.

어느 한쪽 변경만 선택하면 필요한 협업 규칙 일부가 사라진다.

- Current Change만 유지할 경우 4~6번 규칙이 사라진다.
- Incoming Change만 유지할 경우 7~9번 규칙이 사라진다.
- 양쪽 내용을 단순히 연결하면 문단 번호와 논리적인 순서가 깨진다.

따라서 두 변경의 목적을 이해하고 최종 문서 구조에 맞게  
내용을 재배치해야 했으므로 비자명 충돌로 판단했다.

### 6. 해결 전략

해결 방법으로 `keep both` 전략을 선택했다.

최신 `main`의 1~6번 내용을 유지하고, feature 브랜치에서 작성한  
7~9번 내용을 6번 문단 다음에 배치했다.

최종 문서의 순서는 다음과 같다.

```text
1. 브랜치 전략
2. 브랜치 네이밍 규칙
3. Issue 기반 작업
4. 커밋 메시지 컨벤션
5. Pull Request 규칙
6. Pull Request 병합 조건
7. 코드 리뷰 규칙
8. 리뷰 반영 규칙
9. 코드 리뷰 참여 기준
```

VS Code에서 양쪽 변경을 확인한 뒤 다음 작업을 진행했다.

1. 양쪽 변경 사항을 모두 유지했다.
2. 최신 `main`의 4~6번 내용을 3번 뒤에 배치했다.
3. feature 브랜치의 7~9번 내용을 6번 뒤에 배치했다.
4. 충돌 마커를 모두 제거했다.
5. 중복된 구분선과 Markdown 코드 블록을 정리했다.
6. 문단 번호가 1번부터 9번까지 이어지는지 확인했다.

### 7. 해결 및 커밋

충돌 해결 후 다음 명령을 실행했다.

```bash
git add docs/CONTRIBUTING.md
git status
git commit -m "docs: resolve contributing guide conflict"
git push
```

### 8. 검증 결과

다음 항목을 확인했다.

- [x] `<<<<<<<`, `=======`, `>>>>>>>` 충돌 마커가 제거됐다.
- [x] 최신 `main`의 4~6번 내용이 유지됐다.
- [x] feature 브랜치의 7~9번 내용이 유지됐다.
- [x] 문단 번호가 1번부터 9번까지 순서대로 배치됐다.
- [x] Markdown 코드 블록과 표가 정상적으로 표시됐다.
- [x] PR에서 충돌 표시가 사라졌다.
- [x] 다른 팀원에게 충돌 해결 결과의 리뷰를 요청했다.

충돌 마커가 남아 있지 않은지 다음 명령으로 확인했다.

```bash
git grep -n -e '<<<<<<<' -e '=======' -e '>>>>>>>'
```

명령 실행 결과 아무 내용도 출력되지 않았다.

### 9. 결과

양쪽 브랜치의 변경 사항을 모두 보존하면서  
`CONTRIBUTING.md`의 협업 규칙을 1번부터 9번까지 논리적인 순서로 통합했다.

- 관련 PR: [PR #9](https://github.com/gitflow-practice-team/github-workflow-practice/pull/9)
- 충돌 해결 커밋: `<커밋 링크>`
- 최종 병합 커밋: `<PR 병합 후 추가>`

### 10. 배운 점

같은 파일을 수정하더라도 담당 문단이 다르면 충돌이 발생하지 않을 것이라고 생각했지만,  
동일한 기준 위치에 각자의 내용을 삽입하면 Git은 두 내용의 배치 순서를 판단하지 못할 수 있다는 점을 알게 됐다.

또한 `Accept Both Changes`는 두 변경을 단순히 남기는 기능일 뿐,  
문서의 의미와 순서를 자동으로 정리해 주는 기능은 아니라는 점을 확인했다.

다음부터 여러 팀원이 하나의 문서를 분담할 때는 다음 사항을 먼저 합의한다.

- 각 팀원이 수정할 문단과 삽입 위치
- 문단 번호와 병합 순서
- 앞선 문서 PR이 병합된 후 최신 `main`을 반영할지 여부
- 충돌 발생 시 내용을 보존하고 재배치하는 기준