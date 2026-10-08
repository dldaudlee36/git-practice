# Git 브랜치 협업 실습 작업 기록 (GIT_WORK.md)

## 1. 저장소 및 PR 정보

- **GitHub 원격 저장소 주소**: [https://github.com/dldaudlee36/git-practice](https://github.com/dldaudlee36/git-practice)
- **로컬 실습 디렉터리**:
  - 민수 역할: `D:\CHO\git-practice-minsu`
  - 지윤 역할: `D:\CHO\git-practice-jiyun`

### PR(Pull Request) 목록 및 상태
1. **PR #1 (민수 작업 브랜치 병합)**
   - **URL**: [https://github.com/dldaudlee36/git-practice/pull/1](https://github.com/dldaudlee36/git-practice/pull/1)
   - **Base / Head**: `main` ← `feature/minsu`
   - **작업 내용**: `minsu.md` 생성 후 PR 제출, 이후 추가 보완 커밋(`d769392`) 반영
   - **병합 상태**: Merged (`Create a merge commit`, SHA: `24f6c96`)
2. **PR #2 (지윤 작업 브랜치 병합)**
   - **URL**: [https://github.com/dldaudlee36/git-practice/pull/2](https://github.com/dldaudlee36/git-practice/pull/2)
   - **Base / Head**: `main` ← `feature/jiyun`
   - **작업 내용**: `jiyun.md` 생성 및 화면 검토 문서화
   - **병합 상태**: Merged (`Create a merge commit`, SHA: `0fb5d61`)
3. **PR #3 (점검표 추가 브랜치 병합)**
   - **URL**: [https://github.com/dldaudlee36/git-practice/pull/3](https://github.com/dldaudlee36/git-practice/pull/3)
   - **Base / Head**: `main` ← `feature/checklist`
   - **작업 내용**: 양쪽 병합 완료 후 지윤 폴더의 최신 `main`에서 `checklist.md` 추가
   - **병합 상태**: Merged (`Create a merge commit`, SHA: `2409c0b`)

---

## 2. 실습 진행 단계 및 실제 터미널 입출력 기록

### [단계 1] 저장소 클론 및 작업 브랜치 분기

#### 1) 두 로컬 폴더로 clone
```powershell
PS D:\CHO> git clone https://github.com/dldaudlee36/git-practice.git D:\CHO\git-practice-minsu
Cloning into 'D:\CHO\git-practice-minsu'...
PS D:\CHO> git clone https://github.com/dldaudlee36/git-practice.git D:\CHO\git-practice-jiyun
Cloning into 'D:\CHO\git-practice-jiyun'...
```

#### 2) 민수 폴더에서 feature/minsu 생성 및 커밋
```powershell
PS D:\CHO\git-practice-minsu> git checkout -b feature/minsu
Switched to a new branch 'feature/minsu'

# minsu.md 작성 후 커밋
PS D:\CHO\git-practice-minsu> git add minsu.md
PS D:\CHO\git-practice-minsu> git commit -m "docs: 민수 작업 문서 추가"
[feature/minsu 77031f4] docs: 민수 작업 문서 추가
 1 file changed, 5 insertions(+)
 create mode 100644 minsu.md
```

#### 3) 지윤 폴더에서 feature/jiyun 생성 및 커밋
```powershell
PS D:\CHO\git-practice-jiyun> git checkout -b feature/jiyun
Switched to a new branch 'feature/jiyun'

# jiyun.md 작성 후 커밋
PS D:\CHO\git-practice-jiyun> git add jiyun.md
PS D:\CHO\git-practice-jiyun> git commit -m "docs: 지윤 작업 문서 추가"
[feature/jiyun b677d1c] docs: 지윤 작업 문서 추가
 1 file changed, 5 insertions(+)
 create mode 100644 jiyun.md
```

---

### [단계 2] 로컬 브랜치 전환 및 로컬 merge 방향 확인

#### 1) 민수 폴더에서 main 이동 후 merge 확인
- **브랜치 전환 위치**: `feature/minsu` → `main`
- **확인 내용**: `main` 브랜치에서는 아직 `minsu.md`가 보이지 않음 (`README.md`만 존재)
- **로컬 merge 방향**: `main` 브랜치에서 `feature/minsu`를 merge하므로, 변경을 받는 브랜치는 **`main`** 브랜치임
```powershell
PS D:\CHO\git-practice-minsu> git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

PS D:\CHO\git-practice-minsu> Get-ChildItem
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----      2026-10-08   14:54             70 README.md

PS D:\CHO\git-practice-minsu> git merge feature/minsu
Updating 2e6c651..77031f4
Fast-forward
 minsu.md | 5 +++++
 1 file changed, 5 insertions(+)
 create mode 100644 minsu.md

PS D:\CHO\git-practice-minsu> git checkout feature/minsu
Switched to branch 'feature/minsu'
```

#### 2) 지윤 폴더에서 main 이동 후 merge 확인
```powershell
PS D:\CHO\git-practice-jiyun> git checkout main
Switched to branch 'main'

PS D:\CHO\git-practice-jiyun> git merge feature/jiyun
Updating 2e6c651..b677d1c
Fast-forward
 jiyun.md | 5 +++++
 1 file changed, 5 insertions(+)
 create mode 100644 jiyun.md

PS D:\CHO\git-practice-jiyun> git checkout feature/jiyun
Switched to branch 'feature/jiyun'
```

---

### [단계 3] 작업 브랜치 Push, PR 생성 및 보완 커밋 반영

#### 1) 민수/지윤 작업 브랜치 푸시
```powershell
PS D:\CHO\git-practice-minsu> git push -u origin feature/minsu
To https://github.com/dldaudlee36/git-practice.git
 * [new branch]      feature/minsu -> feature/minsu
branch 'feature/minsu' set up to track 'origin/feature/minsu'.

PS D:\CHO\git-practice-jiyun> git push -u origin feature/jiyun
To https://github.com/dldaudlee36/git-practice.git
 * [new branch]      feature/jiyun -> feature/jiyun
branch 'feature/jiyun' set up to track 'origin/feature/jiyun'.
```

#### 2) GitHub PR #1, PR #2 생성
- PR #1: `docs: 민수 작업 브랜치 병합 요청` (`feature/minsu` → `main`)
- PR #2: `docs: 지윤 작업 브랜치 병합 요청` (`feature/jiyun` → `main`)

#### 3) 민수 작업 브랜치에 보완 커밋 추가 후 push (PR #1 자동 반영 확인)
```powershell
PS D:\CHO\git-practice-minsu> git add minsu.md
PS D:\CHO\git-practice-minsu> git commit -m "docs: 민수 작업 문서 보완 커밋 추가"
[feature/minsu d769392] docs: 민수 작업 문서 보완 커밋 추가
 1 file changed, 1 insertion(+)

PS D:\CHO\git-practice-minsu> git push origin feature/minsu
To https://github.com/dldaudlee36/git-practice.git
   77031f4..d769392  feature/minsu -> feature/minsu
```
- 결과: 기존 열려있던 PR #1에 `d769392` 커밋이 자동으로 추가 반영됨을 확인.

---

### [단계 4] PR 검토, Merge Commit 병합 및 로컬 동기화(Pull)

#### 1) GitHub에서 변경사항 검토 및 병합
- PR #1의 Files changed 검토 (`minsu.md` 확인 및 자체 검토 코멘트 작성)
- `Create a merge commit`으로 PR #1 병합 완료 (Merge SHA: `24f6c96`)
- PR #2의 Files changed 검토 (`jiyun.md` 확인 및 자체 검토 코멘트 작성)
- `Create a merge commit`으로 PR #2 병합 완료 (Merge SHA: `0fb5d61`)

#### 2) 민수 폴더에서 main으로 이동 및 git pull
```powershell
PS D:\CHO\git-practice-minsu> git checkout main
Switched to branch 'main'

PS D:\CHO\git-practice-minsu> git pull origin main
From https://github.com/dldaudlee36/git-practice
 * branch            main       -> FETCH_HEAD
   2e6c651..0fb5d61  main       -> origin/main
Updating 77031f4..0fb5d61
Fast-forward
 jiyun.md | 5 +++++
 minsu.md | 1 +
 2 files changed, 6 insertions(+)
 create mode 100644 jiyun.md

PS D:\CHO\git-practice-minsu> Get-ChildItem
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----      2026-10-08   14:56            173 jiyun.md
-a----      2026-10-08   14:56            234 minsu.md
-a----      2026-10-08   14:54             70 README.md
```

#### 3) 지윤 폴더에서 main으로 이동 및 git pull
```powershell
PS D:\CHO\git-practice-jiyun> git checkout main
Switched to branch 'main'

PS D:\CHO\git-practice-jiyun> git pull origin main
From https://github.com/dldaudlee36/git-practice
 * branch            main       -> FETCH_HEAD
   2e6c651..0fb5d61  main       -> origin/main
Updating b677d1c..0fb5d61
Fast-forward
 minsu.md | 6 ++++++
 1 file changed, 6 insertions(+)
 create mode 100644 minsu.md

PS D:\CHO\git-practice-jiyun> Get-ChildItem
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----      2026-10-08   14:55            173 jiyun.md
-a----      2026-10-08   14:56            234 minsu.md
-a----      2026-10-08   14:54             70 README.md
```
- 결과: 양쪽 폴더의 `main`에 민수 파일(`minsu.md`)과 지윤 파일(`jiyun.md`)이 모두 정상 동기화됨을 확인.

---

### [단계 5] 지윤 폴더에서 feature/checklist 작업, PR #3 병합 및 브랜치 정리

#### 1) 지윤 폴더의 최신 main에서 브랜치 생성 및 작업
```powershell
PS D:\CHO\git-practice-jiyun> git checkout -b feature/checklist
Switched to a new branch 'feature/checklist'

PS D:\CHO\git-practice-jiyun> git add checklist.md
PS D:\CHO\git-practice-jiyun> git commit -m "docs: 협업 점검표 추가"
[feature/checklist 1f7784e] docs: 협업 점검표 추가
 1 file changed, 8 insertions(+)
 create mode 100644 checklist.md

PS D:\CHO\git-practice-jiyun> git push -u origin feature/checklist
To https://github.com/dldaudlee36/git-practice.git
 * [new branch]      feature/checklist -> feature/checklist
branch 'feature/checklist' set up to track 'origin/feature/checklist'.
```

#### 2) PR #3 생성 및 Create a merge commit 병합
- PR #3: `docs: 협업 점검표(checklist.md) 추가`
- 병합 완료: SHA `2409c0b`

#### 3) 두 폴더에서 pull 및 완료 브랜치 삭제(정리)
```powershell
# 지윤 폴더:
PS D:\CHO\git-practice-jiyun> git checkout main
PS D:\CHO\git-practice-jiyun> git pull origin main
Updating 0fb5d61..2409c0b
Fast-forward
 checklist.md | 8 ++++++++
 1 file changed, 8 insertions(+)
 create mode 100644 checklist.md

PS D:\CHO\git-practice-jiyun> git branch -d feature/jiyun
Deleted branch feature/jiyun (was b677d1c).
PS D:\CHO\git-practice-jiyun> git branch -d feature/checklist
Deleted branch feature/checklist (was 1f7784e).

# 민수 폴더:
PS D:\CHO\git-practice-minsu> git checkout main
PS D:\CHO\git-practice-minsu> git pull origin main
Updating 0fb5d61..2409c0b
Fast-forward
 checklist.md | 8 ++++++++
 1 file changed, 8 insertions(+)
 create mode 100644 checklist.md

PS D:\CHO\git-practice-minsu> git branch -d feature/minsu
Deleted branch feature/minsu (was d769392).
```

---

## 3. 핵심 질문 답변

### Q1. main에서 `git merge feature/minsu`를 실행하면 어느 브랜치가 변경을 받는가?
> **답변**: 현재 체크아웃되어 있는 **`main` 브랜치**가 변경을 받습니다. Git의 `git merge <가져올브랜치>` 명령어는 대상 브랜치의 커밋 내역을 현재 위치(HEAD)하고 있는 브랜치로 끌어와서 병합하기 때문입니다.

### Q2. GitHub에서 PR을 병합한 뒤에도 각 폴더에서 pull해야 하는 이유는 무엇인가?
> **답변**: GitHub에서 PR을 병합하여 생성된 머지 커밋은 원격 저장소(`origin/main`)에만 존재하며, 각 로컬 저장소로 자동 동기화되지 않기 때문입니다. 따라서 각 로컬 폴더에서 `git pull origin main`을 실행하여 원격의 최신 커밋 이력을 로컬 `main`으로 가져와야 최신 상태를 유지하고, 이후 새 브랜치를 생성하여 작업할 때 충돌이나 누락을 방지할 수 있습니다.
