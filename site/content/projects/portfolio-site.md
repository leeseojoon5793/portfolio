---
title: "개인 포트폴리오 사이트 구축 (대표 활동)"
date: 2026-11-03
weight: 1
description: "Hugo와 GitHub Actions로 개인 소개 사이트를 만들고 GitHub Pages에 자동 배포"
summary: "Hugo PaperMod 테마로 소개 사이트를 만들고, main에 push할 때마다 GitHub Actions가 빌드·배포하도록 구성"
tags: ["Hugo", "GitHub Actions", "GitHub Pages", "Git"]
ShowToc: true
---

## 개요

| 항목 | 내용 |
|---|---|
| 기간 | 2026년 11월 (초급프로젝트 과제 1) |
| 상태 | 진행 중 — 11월 7일 제출 예정 |
| 형태 | **개인 활동** (설정·콘텐츠 작성·배포·검증 모두 본인 수행) |
| 결과물 | 이 사이트, [GitHub 저장소](https://github.com/leeseojoon5793/portfolio) |

## 목적

수업에서 배운 정적 웹 배포를 실제로 적용해서, **코드를 push하면 사람이 손대지 않아도 사이트가 다시 빌드·배포되는 구조**를 직접 만들어 보는 것이 목표였습니다. 동시에 제 소개와 활동을 한곳에 정리해 둘 공간이 필요했습니다.

## 내가 한 일

개인 활동이라 아래 작업을 모두 직접 했습니다.

- Hugo Themes에서 PaperMod 테마를 골라 ZIP으로 받고, 수업 제공 스크립트(`prepare_github_pages.py`)로 배포 준비
- 로컬 폴더를 `main` 브랜치로 Git 초기화하고 GitHub 저장소에 연결
- GitHub Pages의 Source를 GitHub Actions로 설정
- 배포 빌드가 내 설정 파일(`site/hugo.toml`)을 읽지 않던 문제를 찾아 `.github-pages.json` 수정
- `site/hugo.toml`에 한국어 설정, 프로필 화면, 아바타, 메뉴, 이동 버튼, GitHub 링크 구성
- 소개·프로젝트·학습 기록 페이지 작성
- 스크립트가 넣은 예시 글과 로컬 빌드 결과(`site/public`)를 정리

## 수행 과정

1. **테마 선택** — 프로필형 첫 화면(`profileMode`), 검색, 다크모드가 기본 제공되고 Node 같은 추가 도구 없이 Hugo만으로 빌드되는 PaperMod를 골랐습니다.
2. **배포 준비** — ZIP을 풀고 수업 스크립트를 실행해 `site/` 폴더와 배포 워크플로(`.github/workflows/hugo-pages.yml`)를 만들었습니다.
3. **저장소 연결과 첫 배포** — `main` 브랜치로 push하고 Actions에서 빌드·배포 성공을 확인했습니다.
4. **설정과 콘텐츠 작성** — 설정 한 가지, 페이지 섹션 하나마다 커밋하고, 로컬 미리보기(`hugo server`)와 공개 사이트에서 결과를 확인했습니다.

### 선택 이유: 설정을 `site/hugo.toml`에 따로 작성

스크립트가 만든 `pages.json`에는 배포 주소와 테마 경로가 들어 있습니다. 이 파일은 그대로 두고 제 설정은 `hugo.toml`에 따로 썼습니다. 그리고 빌드 설정 목록을 `hugo.toml,pages.json` 순서로 바꿨습니다. Hugo는 왼쪽 파일 값을 우선하므로, 스크립트가 넣은 기본 제목(`hugo-papermod`)은 제 설정으로 덮이고 배포 주소는 스크립트 값이 유지됩니다.

### 선택 이유: 메뉴 링크에 `pageRef` 사용

이 사이트는 `github.io/portfolio/`처럼 저장소 이름이 붙은 하위 경로에 배포됩니다. 메뉴 주소를 `/about/`처럼 직접 쓰면 `github.io/about/`으로 이동해 깨질 수 있습니다. 그래서 실제 페이지를 가리키는 `pageRef`를 써서 Hugo가 하위 경로까지 포함한 주소를 만들도록 했습니다.

## 결과

- **공개 사이트:** [leeseojoon5793.github.io/portfolio](https://leeseojoon5793.github.io/portfolio/)
- **자동 배포:** `main`에 push하면 GitHub Actions가 자동으로 실행되어 1~2분 안에 사이트가 갱신됩니다. 저장소의 [Actions 기록](https://github.com/leeseojoon5793/portfolio/actions)에서 실행 결과를 확인할 수 있습니다.
- **화면 구성:** 홈 프로필(이름·소개·아바타·GitHub 링크) → 소개 / 프로젝트 / 학습 기록 페이지로 이동하는 메뉴와 버튼이 동작합니다.
- **설정 확인:** 페이지가 한국어(`lang="ko"`)로 생성되고, 다크모드 전환이 동작합니다.

## 배운 점과 개선 방향

- **배운 점:** 설정 파일을 만들기만 해서는 반영되지 않을 수 있다는 것을 배웠습니다. `site/hugo.toml`을 처음 push했을 때 제목이 바뀌지 않았고, 원인은 배포 빌드가 읽는 설정 목록에 그 파일이 빠져 있었기 때문이었습니다. 이후로는 **수정 → push → 공개 화면에서 직접 확인**하는 순서를 지키고 있습니다.
- **한계:** 아직 텍스트 위주라 활동 결과를 보여 주는 화면 캡처가 적고, 모바일 화면과 키보드 조작은 충분히 검증하지 못했습니다.
- **다음 개선:** 390px·768px 화면과 키보드 이동을 직접 점검해서 고치고, 팀 프로젝트가 진행되는 대로 결과 화면과 회고를 추가하겠습니다.