# 출처와 이용 조건

## 외부 자료

| 자료 | 사용 위치 | 출처 | 이용 조건 |
|---|---|---|---|
| Hugo PaperMod 테마 | 최상위 `assets/`·`layouts/`·`i18n/` (원본), `site/themes/template/` (빌드용 복사본) | https://github.com/adityatelange/hugo-PaperMod (master ZIP, 2026-11-03 다운로드) | MIT License, © nanxiaobei and adityatelange. 원본 [`LICENSE`](LICENSE) 유지 |
| Hugo | 사이트 빌드 도구 | https://gohugo.io | Apache License 2.0 |
| 배포 준비 스크립트 | `prepare_github_pages.py`, `.github/pages_build.py`, `.github/workflows/hugo-pages.yml`, `site/pages.json`, `.github-pages.json` | 초급프로젝트 수업 제공 (버전 3.1) | 수업 과제용 |

## 직접 작성 / AI 도움 구분

| 파일 | 구분 | 설명 |
|---|---|---|
| `site/hugo.toml` | 본인 + AI 도움 | AI(Claude)가 설정 예시를 제안, 본인이 단계별로 적용·확인 |
| `.github-pages.json`의 `config` 순서 | 본인 + AI 도움 | 공개 사이트 점검으로 문제 발견, Hugo 공식 문서로 원인 확인 후 수정 |
| `site/content/` 전체 글 | 본인 + AI 도움 | 본인 경험·프로젝트 정보를 바탕으로 AI가 초안 작성, 본인이 사실 확인·수정 |
| `site/assets/images/avatar.svg` | AI 생성 | AI가 작성한 SVG 아바타 (얼굴 사진 대신 사용) |
| `site/assets/css/extended/custom.css` | AI 도움 | AI가 작성, 본인이 화면 폭·키보드로 동작 확인 |
| `site/layouts/_partials/social_icons.html` | PaperMod 파생 + AI 도움 | PaperMod 원본 파셜(MIT)을 바탕으로 이름 표기·`aria-label` 수정 |
| `README.md`, `CREDITS.md` | 본인 + AI 도움 | AI가 초안 작성, 본인이 명령을 직접 실행해 확인 |