# Conflict Resolution Log

## 충돌 기록 #1: CONTRIBUTING 협업 규칙 병합

### 1. 기본 정보

- 발생 날짜: 2026-09-17
- 충돌 파일: `docs/CONTRIBUTING.md`
- 작업 브랜치: `feature/taedong-code-review-guide`
- PR 대상 브랜치: `main`
- 충돌 해결자: 엄태동, 박세헌
- 관련 팀원: 육민우
- 해결 환경: GitHub PR 충돌 해결 편집기
- 관련 PR: [PR #9](https://github.com/gitflow-practice-team/github-workflow-practice/pull/9)
- 충돌 해결 커밋: [094b594](https://github.com/gitflow-practice-team/github-workflow-practice/commit/094b59436b94f01791f6541aa90a1521f3361bf1)

- 최초 충돌 확인 당시 main: `4523cfe` (작업자 확인 기준)
- 충돌 해결 시 feature: `6e8eb1b`
- 충돌 해결 시 병합한 main: `fbc3ab3`
- main → feature 병합 커밋: `53b2624`
- 후속 수정·문서화 커밋: `094b594`
- PR #9의 main 최종 병합 커밋: `7fe6cb0`

브랜치 이름은 이후 작업으로 가리키는 커밋이 바뀔 수 있으므로,
당시 상태를 재현할 수 있도록 충돌 해결 직전 양쪽 커밋 해시를 함께 기록한다.

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

### 3. 충돌 확인 및 재현 기준

#### 실제 충돌 확인 과정

1. `feature/taedong-code-review-guide`에서 `main`으로 병합하는 PR #9를 확인했다.
2. GitHub에서 자동 병합할 수 없다는 충돌 안내를 확인했다.
3. PR의 `Resolve conflicts`를 눌러 충돌 해결 편집기를 열었다.
4. `docs/CONTRIBUTING.md`에서 양쪽 변경 내용과 충돌 마커를 확인했다.

이번 해결은 GitHub 웹 편집기에서 진행했다.
따라서 로컬에서 `git merge origin/main`을 실행했다는 내용이나
해당 명령의 터미널 출력은 실제 수행 기록에 포함하지 않는다.

#### 재현 기준

- 기준 파일: `docs/CONTRIBUTING.md`
- 비교할 상태: 1번에 기록한 충돌 해결 직전 feature 및 main 커밋
- 충돌 원인: 양쪽 브랜치가 `3. Issue 기반 작업` 다음의 동일한 위치에 서로 다른 문단을 추가함

충돌 해결 이후의 최신 브랜치끼리 병합하면 같은 충돌이 발생하지 않을 수 있다.
재현할 때는 기록한 충돌 전 커밋을 사용해야 한다.

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

따라서 두 변경의 목적을 이해하고 최종 문서 구조에 맞게 내용을 재배치해야 했으므로 비자명 충돌로 판단했다.

### 6. 해결 전략

양쪽 변경 사항을 모두 보존하는 `keep both` 전략을 선택했다.

- main에서 추가한 4~6번 규칙을 유지한다.
- feature 브랜치에서 추가한 7~9번 규칙을 유지한다.
- 7~9번을 6번 문단 다음에 배치한다.

GitHub 충돌 해결 편집기에서 양쪽 내용을 확인하고,
문서의 최종 순서가 다음과 같도록 직접 정리했다.

1. 브랜치 전략
2. 브랜치 네이밍 규칙
3. Issue 기반 작업
4. 커밋 메시지 컨벤션
5. Pull Request 규칙
6. Pull Request 병합 조건
7. 코드 리뷰 규칙
8. 리뷰 반영 규칙
9. 코드 리뷰 참여 기준

`Accept Both Changes`는 문단 번호에 맞게 내용을 자동 정렬하는 기능이 아니다.
따라서 양쪽 내용을 보존하는 것과 별개로 문단 순서, 중복 내용, Markdown 코드 블록 및 충돌 마커를 직접 정리했다.

### 7. 해결 결과 저장 및 로컬 반영

GitHub 충돌 해결 편집기에서 내용을 정리한 뒤
`Mark as resolved`와 `Commit merge`를 실행했다.

이 작업은 main의 변경과 충돌 해결 결과를 원격 feature 브랜치에 병합 커밋으로 반영하는 작업이다.
PR을 승인하여 feature 브랜치를 main에 최종 병합하는 작업과는 구분된다.

이후 로컬 feature 브랜치에서 pull하여 GitHub에 저장된 충돌 해결 결과를 가져왔다.

- GitHub에서 해결 결과 저장: 원격 feature 브랜치에 반영
- 로컬에서 pull: 원격 feature의 해결 결과를 로컬 feature에 반영
- PR 최종 병합: 다른 팀원의 리뷰와 승인 후 별도로 진행

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

---

## 충돌 기록 #2: README 프로젝트 소개와 학습 노트 목차 병합

### 1. 기본 정보

- 발생 날짜: 2026-09-18
- 충돌 파일: `README.md`
- 작업 브랜치: `feature/jeongbeen-final-evidence`
- PR 대상 브랜치: `main`
- 충돌 해결자: 정빈 (`@b0e2`)
- 관련 작업자: 이주성 (`@YiJuseong`, PR #21 작성자)
- 관련 PR: [PR #21](https://github.com/gitflow-practice-team/github-workflow-practice/pull/21), [PR #24](https://github.com/gitflow-practice-team/github-workflow-practice/pull/24)

### 2. 충돌 전 커밋

- 공통 기준 커밋: `6d4836469827ff63236262775efe30b2c0899382`
- feature 브랜치 커밋: `a93397fcf0d27ebec411466dafe319dfb647a699`
- 병합한 최신 main: `277b14d3f5318d372a188393e2d69b9c20bd0c52`
- 최신 main의 변경: PR #21 병합 커밋

브랜치 이름은 이후 다른 커밋을 가리킬 수 있으므로, 충돌 당시 상태를 재현할 수 있도록 양쪽 커밋 해시를 함께 기록했다.

### 3. 상황

`feature/jeongbeen-final-evidence` 브랜치는 기존 한 줄짜리 README 제목 바로 아래에 프로젝트 소개 문장을 추가했다.

```text
이 저장소는 Issue와 Pull Request를 활용한 Git 협업 실습 과정을 기록합니다.
```

동시에 PR #21은 같은 제목 바로 아래에 다른 프로젝트 소개 문장과 팀원별 학습 노트 목차, 관련 문서 링크를 추가했다. PR #21이 `main`에 먼저 병합된 후 feature 브랜치에서 최신 `origin/main`을 병합하자, 같은 파일의 같은 삽입 위치를 서로 다르게 수정한 두 변경을 Git이 자동으로 배치하지 못해 충돌이 발생했다.

### 4. 재현 명령

```bash
git fetch origin
git switch feature/jeongbeen-final-evidence
git merge origin/main
```

실행 결과는 다음과 같았다.

```text
자동 병합: README.md
충돌 (내용): README.md에 병합 충돌
자동 병합이 실패했습니다. 충돌을 바로잡고 결과물을 커밋하십시오.
```

`git status --short`에서는 `README.md`가 `UU` 상태로 표시됐다.

### 5. 실제 충돌 마커

```text
 <<<<<<< HEAD
이 저장소는 Issue와 Pull Request를 활용한 Git 협업 실습 과정을 기록합니다.
 =======
GitHub Flow 기반 협업 워크플로우를 연습하는 팀 저장소입니다.

## 학습 노트
...
 >>>>>>> origin/main
```

- `HEAD`: 정빈의 feature 브랜치에서 추가한 프로젝트 소개 문장
- `=======`: 두 변경 영역의 구분선
- `origin/main`: PR #21로 추가된 프로젝트 소개, 학습 노트 목차와 관련 문서 링크

### 6. 비자명 충돌로 판단한 이유

양쪽 브랜치는 같은 파일의 같은 hunk인 README 제목 직후를 서로 다르게 수정했다. 한쪽만 선택하면 다음 정보가 사라진다.

- feature 변경만 유지하면 팀원별 학습 노트 목차와 관련 문서 링크가 사라진다.
- main 변경만 유지하면 Issue와 Pull Request 중심의 프로젝트 설명이 사라진다.
- 두 변경을 단순 연결하면 소개 문장의 순서, 누락된 팀원 링크와 관련 문서 구성을 다시 검토해야 한다.

따라서 변경 목적을 이해하고 최종 문서 구조를 결정해야 하는 비자명 충돌에 해당한다.

### 7. 해결 전략

양쪽의 의미 있는 내용을 모두 유지하는 `keep both` 전략을 선택했다.

1. GitHub Flow 기반 저장소라는 소개를 먼저 배치했다.
2. Issue와 Pull Request를 활용한 실습 기록이라는 설명을 이어서 배치했다.
3. PR #21의 학습 노트 목차와 관련 문서 링크를 유지했다.
4. 팀원 5명이 모두 보이도록 박세헌의 학습 문서 링크를 추가했다.
5. 이번 작업에서 추가한 rebase 실습과 제출물 인덱스 링크를 관련 문서에 포함했다.
6. 모든 충돌 마커를 제거했다.

### 8. 해결 및 검증 명령

```bash
git grep -n -e '<<<<<<<' -e '=======' -e '>>>>>>>' -- README.md
git diff --check
git add README.md docs/conflict-resolution.md
git commit
git push
```

검증 결과 README에서 충돌 마커가 발견되지 않았고, 팀원 5명의 문서 링크와 핵심 문서 링크가 모두 유지됐다.

### 9. 결과

- 관련 PR: [PR #24](https://github.com/gitflow-practice-team/github-workflow-practice/pull/24)
- 충돌 해결 커밋: push 후 링크 추가
- 해결 결과: 프로젝트 소개, 팀원별 학습 노트와 핵심 문서 링크를 하나의 README 구조로 통합

### 10. 배운 점

서로 다른 문장을 추가하더라도 동일한 기준 줄 바로 다음에 삽입하면 Git이 순서를 결정하지 못해 충돌할 수 있다. 충돌 해결은 마커를 삭제하는 작업에 그치지 않고, 양쪽 변경의 목적을 파악해 정보 손실 없이 최종 구조를 결정하는 과정이다.

다음부터 공용 README를 수정할 때는 작업 전 최신 `main`을 확인하고, 담당 섹션과 삽입 위치를 팀원끼리 먼저 공유한다.
