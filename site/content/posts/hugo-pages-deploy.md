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