# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 저장소 목적

`kt-cloud-stack/stack-release`는 STACK 플랫폼(OpenStack + Kubernetes 기반 클라우드)의 릴리즈 노트를 관리하는 저장소입니다. 릴리즈 노트 본문은 GitHub Releases에 저장되며, 시각화용 HTML 파일을 함께 관리합니다.

## 릴리즈 관리 명령어

```bash
# 릴리즈 목록 조회
gh release list --repo kt-cloud-stack/stack-release

# 특정 릴리즈 내용 확인
gh release view <TAG> --repo kt-cloud-stack/stack-release

# 새 릴리즈 생성 (노트 파일로)
gh release create <TAG> --repo kt-cloud-stack/stack-release \
  --title "<TAG>" \
  --notes-file release-notes.md \
  --latest

# 기존 릴리즈 내용 수정
gh release edit <TAG> --repo kt-cloud-stack/stack-release \
  --notes-file release-notes.md
```

## 릴리즈 태그 명명 규칙

`YYYY.MM` 형식 사용 (예: `2026.05`, `2025.09`).  
태그는 GitHub에서 직접 생성하며, 모든 태그는 `main` 브랜치의 동일 커밋(`226beba`)을 가리킵니다.

## 릴리즈 노트 구조

GitHub Release 본문은 아래 섹션 순서를 따릅니다:

```
# STACK 통합 릴리스 노트 · {YYYY.MM}

**릴리스 일자:** YYYY-MM-DD
**하이라이트:** {한 줄 요약}

## 신규 기능
### OS / Kubernetes / OpenStack / CI/CD 및 운영 자동화
(카테고리별 테이블)

## 변경 사항
(항목 | 변경 내용 테이블 — 새 버전은 **볼드** 처리)

## 버그 수정

## 주의 및 영향도

## 📚 업그레이드 가이드

## 주요 구성 요소 버전
### OS / Kubernetes / OpenStack (Epoxy 2025.1) / CI/CD Tools
```

OpenStack 버전 테이블은 `구성 요소 | 차트 버전 | 이미지 버전` 3열 구조입니다.  
KTC 커스텀 이미지는 이미지 버전에 `**볼드**` 처리로 표시합니다.

## HTML 시각화 파일

`release-{YYYY.MM}.html` 형식으로 각 릴리즈의 시각화 페이지를 생성합니다.

- 순수 HTML/CSS/JS (빌드 도구 없음, 외부 의존성은 Google Fonts CDN만 사용)
- 다크 테마, 고정 사이드바 네비게이션, 스크롤 연동 활성 메뉴
- KTC 커스텀 컴포넌트는 주황색 `KTC` 배지로 표시
- 변경 사항은 이전 버전(회색) → 새 버전(초록) 비교 레이아웃

## KTC 커스텀 컴포넌트 식별

OpenStack 구성 요소 중 KTC가 직접 빌드/패치한 이미지는 이름에 `-ktc` 또는 `ktc-` 접두사가 포함됩니다.  
현재 커스텀 컴포넌트: `libvirt` (`ktc-openstack-helm`), `Neutron` (이미지 태그에 `-ktc.` 포함).
