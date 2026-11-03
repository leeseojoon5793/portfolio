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

## 2. 설정 파일을 만들었는데 사이트가 안 바뀐 문제

- **관찰:** `site/hugo.toml`에 사이트 제목을 넣고 push했는데, 공개 사이트 제목이 그대로 `hugo-papermod`였습니다.
- **원인:** 수업 스크립트가 만든 `.github-pages.json`의 `"config"` 값이 `"pages.json"` 하나뿐이라, 배포 빌드가 `hugo.toml`을 읽지 않았습니다.
- **수정:** 설정 목록에 `hugo.toml`을 앞에 추가했습니다. Hugo는 왼쪽 파일의 값을 우선 적용합니다.

```json
"config": "hugo.toml,pages.json",
```

- **재확인:** 다시 push한 뒤 Actions가 성공했고, 공개 사이트 제목이 "이서준 포트폴리오"로 바뀐 것을 확인했습니다.

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