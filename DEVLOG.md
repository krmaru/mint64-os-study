# DEVLOG


## 2026-09-01

### 오늘 한 것

* 운영체제 공부 프로젝트 시작
* Git 설치 및 기본 설정 확인
* 기본 브랜치를 `main`으로 설정
* GitHub SSH 키 생성
* GitHub에 SSH 공개키 등록
* Mac과 GitHub SSH 인증 확인
* GitHub `mint64-os-study` Public Repository 생성

### 이해한 것

* Git과 GitHub는 서로 다른 역할을 한다.
* SSH 공개키와 개인키의 역할이 다르다.
* Git commit에는 작성자 이름과 이메일 정보가 기록된다.

### 다음 시작점

* Mac에 로컬 프로젝트 폴더 생성
* Git 저장소 초기화
* GitHub 저장소와 연결


## 2026-09-02

### 오늘 한 것

* `~/Projects/mint64-os-study` 프로젝트 폴더 생성
* `git init`으로 로컬 Git 저장소 초기화
* 저장소 전용 GitHub noreply 이메일 설정
* `README.md`, `DEVLOG.md` 생성
* 프로젝트 README 작성

### 이해한 것

* `git init`을 실행하면 `.git` 디렉터리가 생성되고 해당 폴더가 Git 저장소가 된다.
* 새로 만든 파일은 처음에는 `Untracked` 상태이다.

### 다음 시작점

* `README.md`와 `DEVLOG.md`를 Git에 추가
* 첫 commit 생성
* GitHub 원격 저장소 연결
* 첫 push


## 2026-09-03

### 오늘 한 것

* 로컬 `mint64-os-study` 저장소와 GitHub 원격 저장소 연결 확인
* `git add`, `git commit`, `git push` 과정을 직접 수행
* GitHub에서 `README.md`, `DEVLOG.md`, `GIT_GUIDE.md`가 정상적으로 올라간 것을 확인
* Git/GitHub 사용법과 주요 명령어를 `GIT_GUIDE.md`에 정리
* Git의 기본 작업 흐름을 실제로 연습

### 이해한 것

* `git add`는 다음 commit에 포함할 변경사항을 Staging Area에 올리는 과정이다.
* `git commit`은 Staging된 변경사항을 로컬 Git History에 기록하는 과정이다.
* `git push`는 로컬에서 만든 commit을 GitHub 원격 저장소로 전송하는 과정이다.
* `git diff`는 아직 Staging하지 않은 변경사항을 확인하고, `git diff --staged`는 다음 commit에 들어갈 변경사항을 확인할 때 사용한다.
* Git과 GitHub는 같은 것이 아니며, Git은 로컬 변경 이력 관리 도구이고 GitHub는 Git 저장소를 원격에서 보관·공유하는 서비스이다.
* Commit message는 정해진 답을 쓰는 것이 아니라 실제 변경사항을 의미 있게 요약해서 작성해야 한다.
* GitHub 기록의 목적은 commit 수를 늘리는 것이 아니라 학습·구현·실패·디버깅 과정을 추적 가능하게 만드는 것이다.

### 막힌 것

* 없음

### 다음 시작점

* Stage 0의 다음 단계인 운영체제 개발환경 점검부터 시작
* Mac에 필요한 개발도구가 현재 어느 정도 설치되어 있는지 확인
* QEMU, NASM, Make, x86/x86-64 Cross Compiler 환경 구성 방향 확인


## 2026-09-04

### 오늘 한 것

* 『64비트 멀티코어 OS 원리와 구조』 2장 개발환경 구축을 시작하기 전에 현재 M4 Mac에서 사용할 개발환경 방향을 검토함.
* Windows 가상환경 + Cygwin 방식과 macOS에서 직접 Cross Compiler, NASM, Make, QEMU를 사용하는 방식을 비교함.
* 책을 기반으로 Mac에서 공부한 비공식 GitHub 자료도 참고하여 macOS 환경에서의 개발 가능성을 확인함.
* 별도 Windows 노트북 구매와 Parallels 사용 여부도 검토했으나 아직 확정하지 않음.

### 이해한 것

* Host가 Apple Silicon ARM64 Mac이어도 Cross Compiler와 QEMU를 이용하면 Target은 책과 동일한 x86/x86-64 OS로 유지할 수 있음.
* Cygwin은 Windows에서 Unix/Linux 계열 개발환경을 제공하기 위한 도구이며, macOS는 원래 Unix 계열 환경이므로 반드시 필요한 것은 아님.
* Mac에서 직접 개발할 경우 OS 코드 자체보다 Cross Compiler, NASM, Make, QEMU 등 개발도구의 호환성을 먼저 검증해야 함.
* 비공식 학습자의 Mac 개발 기록은 참고자료로 사용할 수 있지만, 책 저자의 공식 개발환경과 동일한 기준으로 보아서는 안 됨.

### 막힌 것

* M4 Mac에서 책의 전체 개발 흐름을 얼마나 수정 없이 따라갈 수 있을지는 아직 실제로 검증하지 않음.
* Windows/Cygwin 방식과 macOS 네이티브 방식 중 최종 개발환경을 아직 확정하지 않음.

### 다음 시작점

* 『64비트 멀티코어 OS 원리와 구조』 2장을 기준으로 M4 Mac에서 필요한 개발도구를 하나씩 확인하고 실제 개발환경 구축을 시작하기.
* 우선 NASM, Make, QEMU, x86/x86-64 Cross Compiler의 현재 설치 여부와 사용 가능 여부부터 확인하기.
