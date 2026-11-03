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