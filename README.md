# 깃허브 기초 실습 가이드

> **목표**  
> 로컬에 Git 설치 → 초대받은 GitHub 저장소 클론 → Visual Studio에서 C 예제 빌드/실행 → 변경사항 `add/commit/push` → 브랜치 생성 → Pull Request(PR) 생성까지 한 번에 경험합니다.

---

## 0) 준비물 체크리스트

- [ ] Windows PC
- [ ] 관리자 권한(설치용)
- [ ] GitHub 계정 (없다면 https://github.com 가입)
- [ ] **저장소 초대 수락** (이메일 또는 GitHub 알림에서 **Accept invitation** 클릭)
- [ ] Visual Studio 2022 이상 (워크로드 **“Desktop development with C++”** 설치)

---

## 1) Git 설치 및 최초 설정

1. **Git for Windows 설치**
   - https://git-scm.com/download/win 접속 → 설치(기본옵션 권장)
   - 설치 중 **Git Credential Manager**(GCM) 체크 상태 유지

2. **버전/사용자 정보 확인** (PowerShell 또는 명령 프롬프트)
   ```powershell
   git --version
   git config --global user.name "홍길동"
   git config --global user.email "you@example.com"
   git config --list
   ```

3. (선택) 기본 브랜치 이름을 `main`으로 고정하고 싶다면:
   ```powershell
   git config --global init.defaultBranch main
   ```

---

## 2) 저장소 클론(복제) 받기

> 저장소 주소: `https://github.com/epass1123/git.git`  

```powershell
# 작업할 폴더로 이동(예: D:\work)
cd D:\work

# 저장소 클론
git clone https://github.com/<ORG>/<REPO>.git

# 저장소 폴더로 이동
cd .\<REPO>

# 최신 내용 동기화(습관화)
git pull origin main
```

> 처음 `push`할 때 GitHub 로그인 창(Git Credential Manager)이 뜨면 GitHub 계정으로 로그인하세요.

---

```c
#include <stdio.h>

int main(void) {
    printf("Hello, Git & C!\n");
    return 0;
}
```

---

## 3) 첫 수정 → add/commit/push

1. 코드 수정 (예: 출력 문구 변경)
   ```c
   printf("Hello, <본인이름>!\n");
   ```

2. 변경사항 확인/스테이징/커밋/푸시
   ```powershell
   git status
   git add .
   git commit -m "chore: update hello message"
   git push origin main
   ```

> **Tip**: 실무에서는 `main` 직접 푸시 대신, **브랜치 → PR → 리뷰/머지** 흐름을 사용합니다.

---

## 4) 브랜치 생성 후 작업하기

1. 브랜치 생성 & 이동
   ```powershell
   git checkout -b feature/hello-name
   ```

2. 코드 추가/수정 (예: 추가 printf)
   ```c
   printf("Today I practiced Git branch & PR.\n");
   ```

3. 변경사항 커밋 & 브랜치 푸시
   ```powershell
   git add .
   git commit -m "feat: add practice message in main.c"
   git push -u origin feature/hello-name
   ```

---

## 5) GitHub에서 Pull Request(PR) 만들기

1. GitHub 저장소 페이지 접속 → 상단에 **“Compare & pull request”** 클릭  
2. PR 제목/설명 작성(변경 내용, 의도 간단히)
3. **Create pull request** 클릭
4. (옵션) **Reviewers**에 강사 지정, 댓글로 질문 남기기
5. 리뷰 후 **Merge** 버튼으로 `main`에 병합
6. 병합 후 원격 브랜치 **Delete branch**로 정리

---

## 6) 동기화(pull)와 브랜치 정리

```powershell
git checkout main
git pull origin main
git branch -d feature/hello-name
```

---

## 7) 명령어 요약(치트시트)

```powershell
# 최초 1회
git config --global user.name "홍길동"
git config --global user.email "you@example.com"

# 클론 & 최신화
git clone https://github.com/<ORG>/<REPO>.git
cd .\<REPO>
git pull origin main

# 작업 흐름
git checkout -b feature/hello-name
# (코드 수정)
git add .
git commit -m "feat: ..."
git push -u origin feature/hello-name

# PR은 GitHub 웹에서 생성
# 머지 후 정리
git checkout main
git pull origin main
git branch -d feature/hello-name
```

---

## 8) 자주 겪는 이슈 해결

- **권한 에러(403/권한 없음)**  
  → 저장소 **초대 수락** 여부 확인. 강사에게 Collaborator 권한 요청.

- **첫 push 시 로그인 창**  
  → GitHub 계정 로그인(브라우저 창). 실패하면 `제어판 → 자격 증명 관리자`에서 GitHub 관련 자격증명 삭제 후 재시도.

- **브랜치가 안 보임**  
  → `git branch -a`로 로컬/원격 목록 확인 → `git fetch --all` 후 재확인.

- **라인 엔딩(개행) 차이 경고**  
  → 윈도우 기본 CRLF 정상. 팀 규칙 있을 경우 안내에 따름.

---

## 9) 실습 미션(제출 기준)

- [ ] `feature/hello-name` 브랜치 생성
- [ ] `main.c`에 본인 이름과 오늘 날짜를 출력하는 한 줄 추가
- [ ] 의미 있는 커밋 메시지로 커밋
- [ ] 원격 브랜치 푸시
- [ ] GitHub에서 PR 작성(제목/설명 포함)
- [ ] 리뷰 요청(강사 지정) → 머지

**예시 출력**
```
Hello, Git & C!
Hello, 홍길동!
Today I practiced Git branch & PR.
```
