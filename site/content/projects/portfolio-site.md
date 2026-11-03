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