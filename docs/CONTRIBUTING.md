# Contributing Guide

이 문서는 팀 프로젝트에서 일관된 Git 협업 방식을 유지하기 위한 규칙을 정의합니다.

모든 팀원은 아래 규칙을 기준으로 Issue 생성, 브랜치 작업, 커밋, Pull Request, 코드 리뷰, 충돌 해결을 진행합니다.

---

## 1. 브랜치 전략

우리 팀은 **GitHub Flow**를 사용합니다.

### main 브랜치

* `main` 브랜치는 항상 정상적으로 동작하는 상태를 유지합니다.
* `main` 브랜치에는 직접 push하지 않습니다.
* 모든 변경 사항은 Pull Request를 통해 병합합니다.
* Pull Request는 최소 1명의 승인을 받은 후 병합합니다.

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
feature/taedong-string-utils
feature/minsu-number-utils
feature/jiyoung-readme
```

### 작성 기준

* 모두 소문자를 사용합니다.
* 단어 구분은 `-`를 사용합니다.
* 브랜치 이름만 보고 작업 내용을 어느 정도 유추할 수 있도록 작성합니다.
* 한 브랜치에서는 하나의 작업 단위만 처리하는 것을 권장합니다.

### 좋은 예시

```text
feature/taedong-string-utils
feature/minsu-add-contributing-guide
feature/jiyoung-input-validation
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

* 작업 내용
* 완료 조건
* 참고 사항

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