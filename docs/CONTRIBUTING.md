# Contributing Guide

이 문서는 팀 프로젝트에서 일관된 Git 협업 방식을 유지하기 위한 규칙을 정의합니다.

모든 팀원은 아래 규칙을 기준으로 Issue 생성, 브랜치 작업, 커밋, Pull Request, 코드 리뷰, 충돌 해결을 진행합니다.

---

## 1. 브랜치 전략

우리 팀은 **GitHub Flow**를 사용합니다.

### main 브랜치

- `main` 브랜치는 항상 정상적으로 동작하는 상태를 유지합니다.
- `main` 브랜치에는 직접 push하지 않습니다.
- 모든 변경 사항은 Pull Request를 통해 병합합니다.
- Pull Request는 최소 1명의 승인을 받은 후 병합합니다.

### feature 브랜치

모든 작업은 `main`에서 새로운 feature 브랜치를 생성하여 진행합니다.

```text
main
 └─ feature/...
```

작업이 완료되면 Pull Request를 생성하고, 코드 리뷰와 승인을 거친 후 `main`에 병합합니다.

### GitHub Flow를 선택한 이유

GitHub Flow는 브랜치 구조가 단순해 팀원들이 각자의 작업을 독립적으로 진행하기 쉽습니다.
Pull Request와 코드 리뷰를 중심으로 작업하기 때문에 변경 사항을 확인하고 협의한 뒤 안전하게 병합할 수 있습니다.
이번 프로젝트의 핵심 목표인 Issue, Branch, PR, Review 기반 협업을 연습하기에 적합합니다.

---

## 2. 브랜치 네이밍 규칙

브랜치 이름은 다음 형식을 사용합니다.

```text
feature/<name>-<topic>
```

예시:

```text
feature/jeongbeen-collaboration-guide
feature/minwoo-conflict-resolution
feature/taedong-troubleshooting-log
```

### 작성 기준

- 모두 소문자를 사용합니다.
- 단어 구분은 `-`를 사용합니다.
- 브랜치 이름만 보고 작업 내용을 어느 정도 유추할 수 있도록 작성합니다.
- 한 브랜치에서는 하나의 작업 단위만 처리하는 것을 권장합니다.

### 좋은 예시

```text
feature/taedong-string-utils
feature/jeongbeen-add-contributing-guide
feature/minwoo-input-validation
```

### 피해야 할 예시

```text
feature/test
feature/work
feature/final
feature/update
```

---

## 3. Issue 기반 작업

모든 작업은 가능하면 Issue를 먼저 생성한 후 진행합니다.

Issue에는 최소한 다음 내용을 작성합니다.

- 작업 내용
- 완료 조건
- 참고 사항

예시:

```text
[Feature] 문자열 뒤집기 함수 구현
```

```markdown
## 작업 내용

- 입력받은 문자열을 뒤집어 반환하는 함수를 구현합니다.

## 완료 조건

- reverse_string 함수 구현
- 정상 입력 확인
- 사용 예시 작성
```

작업 브랜치와 Pull Request는 해당 Issue를 기준으로 생성합니다.

## 4. 커밋 메시지 컨벤션

커밋 메시지는 다음 형식을 사용합니다.

```text
<type>: <subject>
```

예시:

```text
feat: add string reverse utility
fix: handle empty string input
docs: add pull request guidelines
refactor: simplify validation logic
```

### Type

| Type       | 설명                          |
| ---------- | ----------------------------- |
| `feat`     | 새로운 기능 추가              |
| `fix`      | 버그 수정                     |
| `docs`     | 문서 수정                     |
| `refactor` | 기능 변경 없이 코드 구조 개선 |
| `test`     | 테스트 코드 추가 또는 수정    |
| `chore`    | 기타 설정 및 유지보수 작업    |

### 커밋 메시지 작성 규칙

- 변경 대상과 내용을 알 수 있도록 작성합니다.
- 지나치게 긴 문장은 사용하지 않습니다.
- 하나의 커밋에는 가능한 한 하나의 목적만 포함합니다.
- 변경 내용을 구체적으로 표현합니다.

### 좋은 예시

```text
feat: add string length utility
fix: prevent error on empty input
docs: document branch naming convention
refactor: extract common validation logic
```

### 금지 예시

다음과 같이 변경 내용을 유추하기 어려운 메시지는 사용하지 않습니다.

```text
update
fix
temp
wip
final
edit file
bug fix
```

---

## 5. Pull Request 규칙

모든 feature 브랜치는 Pull Request를 통해 `main`에 병합합니다.

### Pull Request 생성 조건

작업을 완료한 후 다음 사항을 확인합니다.

- 작업과 관련된 Issue가 존재하는지 확인합니다.
- 로컬에서 변경 사항이 정상적으로 동작하는지 확인합니다.
- 불필요한 파일이 포함되지 않았는지 확인합니다.
- 의미 있는 커밋 메시지를 사용했는지 확인합니다.

### Pull Request 제목

PR 제목만 보고 변경 내용을 알 수 있도록 작성합니다.

예시:

```text
feat: add string utility functions
docs: add contributing guide
fix: handle invalid numeric input
```

### Pull Request 본문 필수 항목

모든 PR에는 최소한 다음 내용을 포함합니다.

#### 연결 이슈

```text
Closes #<issue-number>
```

예시:

```text
Closes #3
```

#### 변경 사항 (What)

무엇을 변경했는지 작성합니다.

#### 변경 이유 (Why)

왜 해당 변경이 필요한지 작성합니다.

#### 테스트/검증 방법 (How)

어떤 방법으로 정상 동작을 확인했는지 작성합니다.

예시:

```markdown
## 연결 이슈

- Closes #3

## 변경 사항 (What)

- 문자열을 뒤집는 reverse_string 함수를 추가했습니다.
- 문자열 길이를 반환하는 string_length 함수를 추가했습니다.

## 변경 이유 (Why)

- 문자열 관련 기본 유틸리티 기능을 제공하기 위해 추가했습니다.

## 테스트/검증 방법 (How)

- Python에서 각 함수를 직접 실행했습니다.
- 일반 문자열과 빈 문자열 입력을 확인했습니다.
```

---

## 6. Pull Request 병합 조건

PR은 아래 조건을 충족한 경우에만 `main`에 병합합니다.

- 최소 1명의 팀원이 Approve 했을 것
- 실질적인 코드 리뷰가 최소 1개 이상 존재할 것
- 리뷰어와 작성자 사이에 최소 1회 이상 상호작용이 있을 것
- 필요한 수정 사항이 반영되었을 것
- 미해결 리뷰 대화가 없을 것
- 충돌이 발생한 경우 충돌을 해결했을 것

---
