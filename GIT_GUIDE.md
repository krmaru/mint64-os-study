# Git / GitHub 사용 및 학습 정리

# 1. 앞으로 실제로 사용하는 방법

운영체제 공부를 시작할 때 먼저 프로젝트 폴더로 이동한다.

```bash
cd ~/Projects/mint64-os-study
```

## ① 공부 시작 전 상태 확인

```bash
git status
```

현재 어떤 파일이 수정되어 있는지, 이전 공부에서 commit하지 않은 변경사항이 남아 있는지 확인한다.

---

## ② 공부·코딩·문서 작성

코드나 문서를 수정한다.

작업 중간이나 작업이 끝난 뒤 다시 확인한다.

```bash
git status
```

실제로 어떤 내용이 바뀌었는지 확인하려면:

```bash
git diff
```

---

## ③ 이번 commit에 넣을 파일 선택

예를 들어 `DEVLOG.md`만 넣으려면:

```bash
git add DEVLOG.md
```

여러 파일을 함께 넣으려면:

```bash
git add README.md DEVLOG.md
```

Git 사용에 익숙해질 때까지는 무조건:

```bash
git add .
```

을 사용하는 습관은 피한다.

이번 commit에 어떤 파일을 넣는지 직접 판단하는 연습을 한다.

---

## ④ Staging 상태 확인

```bash
git status
```

다음과 같이 표시되는 파일들이 이번 commit에 포함될 예정이다.

```text
Changes to be committed:
```

실제로 어떤 변경사항이 commit될지도 확인할 수 있다.

```bash
git diff --staged
```

---

## ⑤ Commit 만들기

먼저 스스로 질문한다.

> 이번 변경에서 실제로 무엇을 했는가?

그 내용을 한 문장으로 정리한다.

```bash
git commit -m "커밋 메시지"
```

예:

```bash
git commit -m "docs: update DEVLOG"
```

```bash
git commit -m "study: understand real mode addressing"
```

```bash
git commit -m "feat: print message from boot sector"
```

```bash
git commit -m "debug: investigate boot failure"
```

---

## ⑥ GitHub로 올리기

```bash
git push
```

`git commit`까지는 내 Mac의 로컬 Git에만 기록된다.

`git push`를 해야 GitHub에도 commit이 올라간다.

---

## ⑦ 마지막 확인

```bash
git status
```

모든 변경사항을 정상적으로 commit했다면:

```text
nothing to commit, working tree clean
```

이라고 표시된다.

최근 commit을 확인하려면:

```bash
git log --oneline
```

을 사용한다.

---

## 매일 기본 루틴

```text
프로젝트 폴더 이동
        ↓
git status
        ↓
공부 / 코딩 / 문서 수정
        ↓
git status
        ↓
git diff
        ↓
git add <파일>
        ↓
git status
        ↓
git diff --staged
        ↓
git commit
        ↓
git push
        ↓
git status
```

처음에는 조금 번거롭더라도 이 순서를 반복한다.

Git에 익숙해지면 필요한 단계만 자연스럽게 선택해서 사용하면 된다.

---

## GitHub에서 직접 수정한 뒤 로컬 push가 거절될 때

GitHub 웹에서 `README.md` 등의 파일을 직접 수정하면 그 변경도 하나의 원격 commit으로 기록된다.

이후 로컬에서 별도의 commit을 만든 뒤 바로 `git push`하면 다음과 같이 push가 거절될 수 있다.

    ! [rejected] main -> main (fetch first)

이는 GitHub에는 존재하지만 현재 로컬에는 없는 commit이 있기 때문이다.

### 해결 순서

    git fetch origin
    git rebase origin/main
    git push

| 명령어 | 역할 |
| --- | --- |
| `git fetch origin` | GitHub의 최신 commit 정보를 가져온다. 현재 작업 파일은 바로 변경하지 않는다. |
| `git rebase origin/main` | 내 로컬 commit을 최신 `origin/main` 뒤에 다시 이어 붙인다. |
| `git push` | 정리된 로컬 commit을 GitHub에 업로드한다. |

예를 들어 다음과 같이 로컬과 GitHub의 기록이 갈라졌다면,

    GitHub : A → B → C
    Local  : A → B → D

`git fetch origin`과 `git rebase origin/main` 이후에는 다음과 같이 정리된다.

    A → B → C → D'

`D'`는 기존 `D`와 내용은 같지만, rebase 과정에서 위치가 바뀌면서 새로운 commit hash를 가지게 된다.

### 미리 예방하기

GitHub 웹이나 다른 컴퓨터에서 저장소를 수정한 적이 있다면 로컬 작업을 시작하기 전에 다음 명령으로 최신 상태를 먼저 반영할 수 있다.

    git pull --rebase

이 명령은 원격 변경사항을 먼저 반영한 뒤 로컬 commit을 그 뒤에 이어 붙이는 방식으로 동작한다.

> 원격에 내가 모르는 변경사항이 있을 때는 무작정 `git push --force`를 사용하지 않는다.


# 2. Git 명령어 정리

모든 명령어를 외울 필요는 없다.

우선 `status → diff → add → commit → push`의 흐름을 익히고, 나머지는 필요할 때 찾아본다.

| 구분             | 명령어                             | 용도                                         | 주의                         |
| -------------- | ------------------------------- | ------------------------------------------ | -------------------------- |
| 프로젝트 이동        | `cd ~/Projects/mint64-os-study` | 운영체제 프로젝트 폴더로 이동                           | Git 명령 실행 전 현재 위치 확인       |
| 상태 확인          | `git status`                    | 변경·Staging 상태와 현재 branch 확인                | 가장 자주 사용                   |
| 간단한 상태 확인      | `git status -sb`                | Git 상태를 짧게 표시                              | Git에 익숙해진 뒤 사용             |
| 변경 내용 확인       | `git diff`                      | 아직 Staging하지 않은 변경 내용 확인                   | commit 전 확인 권장             |
| Staging 내용 확인  | `git diff --staged`             | 다음 commit에 들어갈 변경사항 확인                     | `git add` 후 사용             |
| 파일 Staging     | `git add <파일명>`                 | 특정 파일을 다음 commit에 포함                       | 초반에는 파일을 직접 지정             |
| 여러 파일 Staging  | `git add <파일1> <파일2>`           | 여러 파일을 함께 Staging                          | 관련된 변경인지 확인                |
| 전체 Staging     | `git add .`                     | 현재 위치의 변경사항을 한꺼번에 Staging                  | 원하지 않는 파일까지 포함될 수 있음       |
| Staging 취소     | `git restore --staged <파일명>`    | 파일을 Staging Area에서 제외                      | 파일의 수정 내용 자체는 유지           |
| 수정 되돌리기        | `git restore <파일명>`             | 파일을 마지막 commit 상태로 되돌림                     | **작성한 수정 내용이 사라질 수 있음**    |
| Commit         | `git commit -m "메시지"`           | Staging된 변경사항을 로컬 Git History에 기록          | 실제 변경 내용을 표현할 것            |
| GitHub 업로드     | `git push`                      | 로컬 commit을 GitHub로 전송                      | commit이 먼저 있어야 함           |
| 최초 Push        | `git push -u origin main`       | 로컬 `main`과 GitHub `origin/main`을 연결하며 push | 보통 최초 1회 사용                |
| Commit 목록      | `git log --oneline`             | commit 기록을 간단하게 확인                         | 학습 이력 확인에 유용               |
| Commit 상세 확인   | `git show <커밋해시>`               | 특정 commit의 변경 내용 확인                        | hash 전체가 아니라 앞부분만으로도 가능    |
| 원격 저장소 확인      | `git remote -v`                 | 연결된 GitHub 저장소 주소 확인                       | `origin` 확인에 사용            |
| GitHub 정보 가져오기 | `git fetch`                     | 원격의 최신 정보를 가져오되 바로 합치지는 않음                 | 상태 확인용으로 비교적 안전            |
| GitHub 변경 반영   | `git pull`                      | 원격 변경사항을 받아 현재 branch에 반영                  | 다른 PC나 GitHub에서 수정했을 때 유용  |
| Branch 확인      | `git branch`                    | branch 목록과 현재 branch 확인                    | 현재는 주로 `main` 사용           |
| Branch 이동      | `git switch <브랜치명>`             | 다른 branch로 이동                              | 수정사항이 남아 있으면 이동이 제한될 수 있음  |
| 새 Branch       | `git switch -c <브랜치명>`          | 새 branch를 만들고 이동                           | 기능 실험 시 유용                 |
| 임시 보관          | `git stash`                     | commit하지 않은 변경사항을 임시로 치움                   | 나중에 branch 활용 시 유용         |
| 임시 변경 복원       | `git stash pop`                 | stash한 변경사항을 다시 적용                         | 충돌이 생길 수도 있음               |
| 저장소 복제         | `git clone <주소>`                | GitHub 저장소를 새로운 컴퓨터에 내려받음                  | 현재 Mac에서는 이미 저장소가 있으므로 불필요 |
| 사용자 이름 확인      | `git config user.name`          | 현재 저장소에서 사용되는 Git 이름 확인                    | commit 작성자 정보              |
| 이메일 확인         | `git config user.email`         | 현재 저장소에서 사용되는 commit 이메일 확인                | 이 프로젝트는 noreply 이메일 사용     |
| Git 저장소 위치 확인  | `git rev-parse --show-toplevel` | 현재 Git 프로젝트의 최상위 경로 확인                     | 터미널 위치가 헷갈릴 때 유용           |

## 당분간 함부로 사용하지 않을 명령어

| 명령어                | 위험                              |
| ------------------ | ------------------------------- |
| `git reset --hard` | 작성 중인 변경사항을 잃을 수 있음             |
| `git clean`        | Git이 추적하지 않는 파일을 삭제할 수 있음       |
| `git push --force` | GitHub의 기존 History를 덮어쓸 수 있음    |
| `git branch -D`    | 아직 합쳐지지 않은 branch를 강제로 삭제할 수 있음 |

이 명령어들은 필요해졌을 때 정확한 상태를 확인한 뒤 사용한다.

---

# 3. Git과 GitHub의 차이

## Git

내 컴퓨터에서 파일의 변경 이력을 관리하는 프로그램이다.

다음을 관리한다.

* 어떤 파일이 바뀌었는가
* 어떤 변경사항을 하나의 기록으로 묶었는가
* 언제 어떤 상태를 기록했는가
* 이전 상태와 무엇이 달라졌는가

Git은 GitHub가 없어도 사용할 수 있다.

## GitHub

Git으로 관리하는 저장소를 인터넷에 보관하고 공유하는 서비스이다.

따라서:

```text
Git
= 로컬에서 변경 이력 관리

GitHub
= Git 저장소를 인터넷에 저장·공유
```

라고 구분한다.

---

# 4. 지금까지 배운 Git의 전체 흐름

```text
파일 생성 / 수정
        ↓
Working Directory
        ↓
git add
        ↓
Staging Area
        ↓
git commit
        ↓
Local Git History
        ↓
git push
        ↓
GitHub
```

가장 중요한 세 명령어는 다음과 같다.

```text
git add
= 다음 commit에 넣을 변경사항 선택

git commit
= 로컬 Git History에 기록

git push
= 로컬 commit을 GitHub로 전송
```

따라서:

```text
git add ≠ 저장
git commit ≠ GitHub 업로드
git push ≠ 새로운 commit 생성
```

이다.

---

# 5. 현재 프로젝트 구조

운영체제 공부 프로젝트의 기본 위치:

```text
~/Projects/mint64-os-study
```

절대 경로:

```text
/Users/krmaru/Projects/mint64-os-study
```

기본 구조:

```text
mint64-os-study/
├── .git/
├── README.md
├── DEVLOG.md
└── GIT_GUIDE.md
```

`GIT_GUIDE.md`는 Git/GitHub 사용법과 학습 내용을 정리하기 위한 문서이다.

---

# 6. `git init`과 `.git`

처음 만든:

```text
mint64-os-study/
```

는 일반 폴더였다.

그 안에서:

```bash
git init
```

을 실행하면서 Git Repository가 되었다.

```text
일반 폴더
   ↓
git init
   ↓
.git 생성
   ↓
Git Repository
```

`.git`은 숨김 디렉터리이다.

그 안에는 Git History, branch, repository 설정 등 Git이 저장소를 관리하기 위해 필요한 정보가 들어간다.

직접 수정하지 않는다.

---

# 7. 파일 상태

## Untracked

파일은 실제로 존재하지만 Git이 아직 관리 대상으로 추적하지 않는 상태이다.

예:

```text
Untracked files:
    README.md
```

새 파일을 만들면 처음에는 보통 Untracked 상태가 된다.

## Staged

다음 commit에 포함하기로 선택한 상태이다.

```bash
git add README.md
```

실행 후:

```text
Changes to be committed:
    new file: README.md
```

처럼 표시된다.

## Committed

Staging Area의 변경사항을 Git History에 하나의 기록으로 확정한 상태이다.

```bash
git commit -m "docs: add README and DEVLOG"
```

## Pushed

로컬에서 만들어진 commit을 GitHub 원격 저장소로 전송한 상태이다.

```bash
git push
```

---

# 8. Working Directory와 Staging Area

Git에서는 파일을 수정했다고 바로 commit되지 않는다.

```text
Working Directory
      ↓
   git add
      ↓
Staging Area
      ↓
 git commit
      ↓
Git History
```

## Working Directory

현재 실제로 편집하고 있는 파일이 존재하는 영역이다.

코드나 문서를 수정하면 Working Directory의 상태가 변한다.

## Staging Area

다음 commit에 어떤 변경사항을 넣을지 선택해 두는 공간이다.

예를 들어 파일 5개를 수정했다고 해서 반드시 5개를 하나의 commit에 넣어야 하는 것은 아니다.

관련된 파일만 골라 하나의 commit으로 만들 수 있다.

따라서 Staging Area의 핵심 의미는:

> 어떤 변경사항을 하나의 의미 있는 commit으로 묶을 것인가?

이다.

---

# 9. Commit

Commit은 단순한 저장 버튼이 아니다.

특정 변경사항을 하나의 의미 있는 기록으로 남기는 것이다.

최초 commit에서는:

```text
README.md
DEVLOG.md
```

를 하나의 초기 문서 구성 작업으로 묶었다.

Commit message:

```text
docs: add README and DEVLOG
```

결과:

```text
[main (root-commit) 27da45f] docs: add README and DEVLOG
```

각 부분의 의미는 다음과 같다.

```text
main
= 현재 branch

root-commit
= 저장소의 최초 commit

27da45f
= commit을 식별하는 hash의 일부

docs: add README and DEVLOG
= 사람이 작성한 commit message
```

---

# 10. Commit Message 작성법

Commit message는 Git이나 AI가 자동으로 정하는 정답이 아니다.

먼저 스스로 질문한다.

> 이번 변경에서 실제로 무엇을 했는가?

그 답을 한 줄로 기록한다.

## `feat:`

새로운 기능을 구현했을 때.

```text
feat: print message from boot sector
```

## `fix:`

문제의 원인을 찾아 수정했을 때.

```text
fix: correct GDT code segment descriptor
```

## `debug:`

문제를 조사하거나 디버깅했을 때.

반드시 해결할 필요는 없다.

```text
debug: investigate protected mode boot failure
```

## `study:`

개념 공부나 실험을 했을 때.

```text
study: understand real mode memory addressing
```

## `docs:`

README, DEVLOG 등 문서를 수정했을 때.

```text
docs: update DEVLOG
```

## `refactor:`

기능은 동일하지만 코드 구조를 개선했을 때.

```text
refactor: reorganize bootloader source
```

## 피해야 할 메시지

```text
update
test
today
commit
change
something
```

1년 뒤 `git log`만 보더라도 당시 무엇을 했는지 어느 정도 알 수 있어야 한다.

---

# 11. DEVLOG와 Commit의 차이

## Commit

코드와 파일이 어떻게 변경되었는지를 기록한다.

## DEVLOG

내가 무엇을 공부했고, 무엇을 이해했고, 어디에서 막혔는지를 기록한다.

예를 들어 부팅 실패 문제를 해결하지 못했다면 DEVLOG에는:

```text
### 오늘 한 것

- Boot Sector 실행 문제 조사

### 막힌 것

- QEMU가 Boot Sector를 실행하지 못하는 원인을 아직 찾지 못함

### 다음 시작점

- Boot Signature부터 다시 확인
```

이라고 기록할 수 있다.

Commit은:

```text
debug: investigate boot sector execution failure
```

처럼 남길 수 있다.

실패 역시 학습 과정의 일부이므로 기록할 가치가 있다.

---

# 12. DEVLOG 작성 시점

DEVLOG는 가능하면 **그날 공부가 끝난 뒤 작성한다.**

아직 공부가 진행 중인데 그날 무엇을 했는지가 확정되지 않은 상황에서 미리 마무리하지 않는다.

기본 형식:

```text
## YYYY-MM-DD

### 오늘 한 것

### 이해한 것

### 막힌 것

### 다음 시작점
```

모든 항목을 반드시 채울 필요는 없다.

특히 `다음 시작점`은 가능한 한 구체적으로 기록한다.

다음 공부를 시작할 때:

> 어디까지 했더라?

를 다시 찾는 시간을 줄이기 위해서이다.

---

# 13. 공부하지 못한 날

GitHub Contribution을 채우기 위해 의미 없는 코드나 주석을 추가하지 않는다.

실제로 공부하지 못했다면 필요에 따라 그대로 DEVLOG에 기록한다.

예:

```text
### 오늘 한 것

- 없음

### 이유

- 중간고사 준비

### 다음 시작점

- GDT Descriptor 구조 복습부터 재개
```

프로젝트의 목표는 GitHub 잔디를 채우는 것이 아니다.

1년 뒤 Git History와 DEVLOG에서 다음 과정이 보여야 한다.

```text
공부
→ 구현
→ 실패
→ 원인 추론
→ 디버깅
→ 해결
→ 이해의 증가
```

---

# 14. SSH와 GitHub

Mac과 GitHub는 SSH 방식으로 연결했다.

SSH에서는 공개키와 개인키를 사용한다.

## Private Key

Mac에만 보관한다.

절대로 다음 장소에 올리지 않는다.

* GitHub
* README
* DEVLOG
* 채팅
* 이메일
* 공개 문서

## Public Key

GitHub에 등록할 수 있다.

일반적인 공개키 파일:

```text
id_ed25519.pub
```

공개키 끝에는 이메일 등의 comment가 붙어 있을 수 있다.

인증에 사용되는 핵심 공개키 값과 사람이 알아보기 위한 comment는 역할이 다르다.

---

# 15. `known_hosts`

SSH 폴더에 있던:

```text
known_hosts
known_hosts.old
```

는 SSH 개인키가 아니다.

SSH로 이전에 접속한 서버의 식별 정보를 저장하는 파일이다.

GitHub에 처음 접속할 때:

```text
Are you sure you want to continue connecting?
```

이라는 질문에 `yes`라고 답하면 GitHub 서버 정보도 기록될 수 있다.

---

# 16. Git 사용자 정보

Git commit에는 작성자 정보가 기록된다.

확인:

```bash
git config user.name
```

```bash
git config user.email
```

## Global 설정

```bash
git config --global ...
```

여러 Git 저장소에서 기본적으로 사용하는 설정이다.

## Repository-local 설정

현재 저장소에만 적용한다.

```bash
git config user.email "..."
```

`--global`을 사용하지 않으면 현재 repository의 설정이 된다.

현재 프로젝트는 Public Repository이므로 개인 이메일 주소 대신 GitHub noreply 이메일을 repository-local 설정으로 사용한다.

---

# 17. Branch

현재 기본 branch는:

```text
main
```

이다.

현재 단계에서는 다음 정도로 이해한다.

> Branch는 독립적인 작업 흐름이다.

당장은 `main` 하나로 공부해도 충분하다.

실제로 별도의 기능 실험이나 개발이 필요해질 때 branch를 본격적으로 사용한다.

---

# 18. Remote와 `origin`

로컬 Git 저장소와 GitHub 저장소는 서로 다른 저장소이다.

GitHub 저장소 주소를 로컬 Git에 등록한 것을 Remote라고 한다.

현재 GitHub 원격 저장소에는 일반적인 별명인:

```text
origin
```

을 사용한다.

확인:

```bash
git remote -v
```

`origin` 자체가 GitHub를 의미하는 것은 아니다.

해당 원격 저장소에 붙인 별명이다.

---

# 19. 첫 Push의 `-u`

새 저장소의 최초 push에서는:

```bash
git push -u origin main
```

형태를 사용할 수 있다.

```text
origin
= 원격 저장소

main
= 전송할 branch

-u
= 이후 사용할 기본 연결 관계 설정
```

한 번 정상적으로 연결되고 나면 일반적으로:

```bash
git push
```

만 사용하면 된다.

---

# 20. 지금 단계에서 반드시 기억할 것

Git 명령어 전체를 외우는 것이 목표가 아니다.

우선 다음 흐름을 스스로 사용할 수 있어야 한다.

```text
수정
↓
status로 상태 확인
↓
diff로 변경 확인
↓
add로 선택
↓
commit으로 기록
↓
push로 GitHub에 전송
```

그리고 commit할 때마다 생각한다.

> 이 변경사항들을 왜 하나의 commit으로 묶는가?

Git을 잘 사용하는 것은 명령어를 많이 외우는 것보다 **개발 과정의 변경사항을 의미 있게 나누고 기록하는 능력**에 가깝다.

이 프로젝트에서는 commit 수나 GitHub Contribution 숫자보다, 1년 뒤 Git History와 DEVLOG를 통해 운영체제를 어떻게 공부하고 이해해 갔는지가 보이는 것을 우선한다.
