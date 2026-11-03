# 이서준 포트폴리오

Hugo와 GitHub Actions로 만든 개인 소개 사이트입니다.

- 사이트: https://leeseojoon5793.github.io/portfolio/
- 저장소: https://github.com/leeseojoon5793/portfolio
- 테마: [Hugo PaperMod](https://github.com/adityatelange/hugo-PaperMod) (출처와 라이선스는 [CREDITS.md](CREDITS.md))

## 필요 도구

| 도구 | 버전 | 용도 |
|---|---|---|
| Hugo (extended) | 로컬 0.169.0 / 배포 0.167.0 | 사이트 빌드 |
| Git | 2.55.0 | 버전 관리, push |
| Python | 3.14.6 | 수업 배포 준비 스크립트 실행 |
| 수업 스크립트 | `prepare_github_pages.py` 3.1 | 배포 워크플로·`site/` 생성 |

배포 빌드는 `.github/workflows/hugo-pages.yml`에 고정된 Hugo 0.167.0으로 실행됩니다.

## 설치 (Windows)

PowerShell에서 실행합니다. 설치 후에는 **터미널(또는 VS Code)을 완전히 껐다 다시 열어야** 새 명령을 인식합니다.

```powershell
winget install Hugo.Hugo.Extended
winget install Git.Git
winget install Python.Python.3.12
```

설치 확인:

```powershell
hugo version
git --version
python --version
```

다른 운영체제는 [Hugo 설치 안내](https://gohugo.io/installation/)를 참고하세요.

## 로컬에서 확인

```powershell
git clone https://github.com/leeseojoon5793/portfolio.git
cd portfolio/site
hugo server --config pages.json,hugo.toml
```

브라우저에서 http://localhost:1313/portfolio/ 를 엽니다. 파일을 저장하면 자동으로 새로고침됩니다. 종료는 `Ctrl + C`.

> 설정 파일은 `pages.json,hugo.toml` 순서로 적어야 합니다. Hugo는 **뒤에 적은 파일이 우선**이라, 순서가 바뀌면 `site/hugo.toml`의 제목 등이 스크립트 기본값으로 덮어써집니다.

## 빌드

```powershell
cd site
hugo --gc --minify --config pages.json,hugo.toml
```

결과는 `site/public/`에 생성됩니다(`.gitignore`로 제외됨). 배포용 빌드는 GitHub Actions가 `.github/pages_build.py --build`로 따로 실행합니다.

## 수정할 파일 위치

| 바꾸려는 것 | 파일 |
|---|---|
| 사이트 제목, 메뉴, 홈 프로필 문구·버튼, GitHub 링크 | `site/hugo.toml` |
| 소개 페이지 | `site/content/about.md` |
| 프로젝트 목록 안내 / 각 프로젝트 | `site/content/projects/_index.md` / `site/content/projects/*.md` |
| 학습 기록 글 | `site/content/posts/*.md` |
| 검색 페이지 | `site/content/search.md` |
| 프로필 아바타 | `site/assets/images/avatar.svg` |
| 추가 스타일(초점 표시, 줄바꿈 등) | `site/assets/css/extended/custom.css` |
| 테마 화면 덮어쓰기(GitHub 아이콘 링크) | `site/layouts/_partials/social_icons.html` |
| 배포 빌드가 읽는 설정 파일 순서 | `.github-pages.json`의 `"config"` |
| 배포 워크플로(수업 스크립트가 생성) | `.github/workflows/hugo-pages.yml` |

`site/themes/template/`(테마 복사본)과 최상위의 `assets/`, `layouts/`(테마 원본)는 직접 수정하지 않습니다. 테마 화면을 바꿀 때는 `site/layouts/`에 같은 경로로 파일을 만들어 덮어씁니다.

## 수정 후 재배포

최상위 폴더에서 실행합니다.

```powershell
git add <수정한 파일>
git commit -m '변경 내용을 설명하는 메시지'
git push origin main
```

1. 저장소 [Actions](https://github.com/leeseojoon5793/portfolio/actions) 탭에서 `Deploy Hugo to GitHub Pages` 실행의 `build`, `deploy`가 모두 성공(초록 체크)인지 확인합니다. 보통 1~2분 걸립니다.
2. 실패(빨간 X)하면 실행을 눌러 빨간 단계의 로그를 확인합니다.
3. 공개 사이트를 **시크릿 창** 또는 강력 새로고침(`Ctrl + Shift + R`)으로 열어 변경이 반영됐는지 확인합니다. GitHub Pages와 브라우저 캐시 때문에 일반 창에서는 잠시 이전 화면이 보일 수 있습니다.

### 최초 1회 설정

저장소 `Settings → Pages → Build and deployment → Source`를 **GitHub Actions**로 설정합니다. 설정 전에 push해서 실행이 실패했다면, 설정 후 Actions에서 **Re-run all jobs**로 다시 실행합니다.