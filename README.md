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