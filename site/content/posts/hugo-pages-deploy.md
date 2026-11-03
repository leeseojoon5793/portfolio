---
title: "Hugo 사이트를 GitHub Actions로 배포하며 겪은 일"
date: 2026-11-03
description: "포트폴리오 사이트를 배포하면서 확인한 설정과 문제 해결 기록"
summary: "Pages Source 설정, 설정 파일이 반영되지 않던 문제, 하위 경로 링크 처리"
tags: ["Hugo", "GitHub Actions", "배포"]
ShowToc: true
---

## 1. Pages Source를 GitHub Actions로

저장소 `Settings → Pages → Build and deployment → Source`를 **GitHub Actions**로 바꿔야 워크플로의 배포 단계가 동작합니다. 이 설정 전에 push하면 첫 실행이 실패할 수 있어서, 설정을 먼저 바꾼 뒤 push했습니다.

## 2. 설정 파일을 만들었는데 사이트 제목이 안 바뀐 문제

- **관찰:** `site/hugo.toml`에 사이트 제목을 넣고 push했는데, 공개 사이트 제목이 그대로 `hugo-papermod`였습니다.
- **1차 원인과 수정:** 수업 스크립트가 만든 `.github-pages.json`의 `"config"` 값이 `"pages.json"` 하나뿐이라 배포 빌드가 `hugo.toml`을 읽지 않았습니다. 목록에 `hugo.toml`을 추가했고, 이후 메뉴와 프로필 설정은 정상 반영됐습니다.
- **다시 관찰:** 공개 사이트를 점검해 보니 메뉴는 바뀌었는데 사이트 이름과 탭 제목은 여전히 `hugo-papermod`였습니다.
- **2차 원인:** Hugo 공식 문서를 확인해 보니, 설정 파일을 여러 개 주면 **뒤에 적은 파일의 값이 앞의 값을 덮어씁니다.** 순서를 `hugo.toml,pages.json`으로 적어서 `pages.json`의 기본 제목이 제 제목을 덮어쓰고 있었습니다.
- **수정:** 순서를 바꿔 제 설정 파일이 마지막에 오게 했습니다.

```json
"config": "pages.json,hugo.toml",
```

- **재확인:** push 후 Actions 성공을 확인했습니다. 일반 창에서는 캐시 때문에 이전 제목이 잠깐 보였지만, 시크릿 창에서 사이트 이름·탭 제목·하단 저작권 줄이 모두 "이서준 포트폴리오"로 바뀐 것을 확인했습니다.
## 3. 저장소 이름이 붙는 주소에서 링크 처리

이 사이트 주소는 `leeseojoon5793.github.io/portfolio/`처럼 저장소 이름(`/portfolio/`)이 붙습니다. 링크를 `/about/`처럼 `/`로 시작하게 쓰면 `github.io/about/`으로 이동해 페이지를 찾지 못합니다.

- **상단 메뉴:** 주소 대신 실제 페이지를 가리키는 `pageRef`를 써서, Hugo가 `/portfolio/about/`처럼 하위 경로를 붙인 주소를 만들게 했습니다.

```toml
[[menu.main]]
  name = "소개"
  pageRef = "/about"
```

- **홈 버튼:** 홈에만 있는 버튼이라 `url = "about/"`처럼 `/` 없이 써서, 홈 주소 뒤에 이어 붙도록 했습니다.

## 4. 확인 순서

1. `main`에 push
2. 저장소 **Actions** 탭에서 실행이 성공(초록 체크)했는지 확인
3. 공개 사이트를 강력 새로고침(`Ctrl + Shift + R`)해서 변경이 반영됐는지 확인
4. 메뉴를 하나씩 눌러 주소에 `/portfolio/`가 들어가는지 확인