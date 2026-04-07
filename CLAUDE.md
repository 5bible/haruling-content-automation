# HaruLing Content Automation - Claude Automation Guide

## 📊 프로젝트 개요

HaruLing 한국어 학습 서비스를 위한 K-콘텐츠 뉴스 자동화 시스템입니다.

**목표**: 매주 K-콘텐츠(드라마, 가요, 아이돌) 뉴스를 수집 → 분석 → Obsidian에 저장

---

## 🤖 Claude의 자동화 작업 (매주 월요일 10시 UTC)

### Step 1: RSS 뉴스 수집
**할 일**: config/news_sources.yaml의 모든 RSS 피드에서 뉴스 수집

**피드 위치**: 
\\\
config/news_sources.yaml
  - google_news: K-drama, K-pop, Korean entertainment, Hallyu
  - korean_media: News1, Soompi, AllKpop
\\\

**요구사항**:
- 지난 7일간의 뉴스만 수집
- 최대 10개 기사
- 중복 제거
- 필수 정보: title, source, link, published, summary

**결과**: 뉴스 기사 리스트 (JSON 형식)

---

### Step 2: Google Gemini로 분석
**할 일**: 수집된 뉴스를 분석하여 주간 보고서 생성

**프롬프트**: config/prompts.yaml 참고 (또는 아래 기본 프롬프트 사용)

**분석 지시**:
당신은 K-콘텐츠 마케팅 전문가입니다. 다음 뉴스를 분석해주세요:

1. **트렌드 핵심 요약** (3-5줄)
2. **카테고리별 분석**
   - 드라마/영화
   - 가요/뮤직
   - 아이돌/엔터테인먼트
3. **외국인 학습자 관점**: 언어/문화 학습 포인트
4. **HaruLing 콘텐츠 아이디어** (3-5가지)

**결과**: Markdown 형식의 주간 보고서

---

### Step 3: Obsidian에 저장
**할 일**: Desktop Commander를 통해 Obsidian vault에 파일 저장

**저장 경로** (Windows):
\\\
C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\
\\\

**파일명**:
\\\
Week {week_number} - K-Content Trends [{year}].md
예: Week 14 - K-Content Trends [2026].md
\\\

**파일 형식**: Markdown (.md)

---

## 🔧 환경 설정

### .env 파일
\\\.env
GOOGLE_API_KEY=your_api_key_here
OBSIDIAN_VAULT_PATH=C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠
\\\

### 필수 환경변수
- \GOOGLE_API_KEY\: Google Gemini API 키
- \OBSIDIAN_VAULT_PATH\: Windows Obsidian vault 경로

---

## 📅 자동화 스케줄

**실행**: 매주 월요일 10시 UTC (또는 필요시 수동 실행)

---

## 🔄 전체 워크플로우

\\\
[매주 월요일 10시 UTC]
  ↓
1. RSS 피드에서 뉴스 수집 (10개)
  ↓
2. Google Gemini API로 분석
  ↓
3. Markdown 보고서 생성
  ↓
4. Desktop Commander로 Obsidian에 저장
  ↓
[완료 및 알림]
\\\

---

## 📁 설정 파일 구조

### config/news_sources.yaml
- google_news: 4개 RSS 피드
- korean_media: 3개 RSS 피드

### config/prompts.yaml
- 분석용 프롬프트 템플릿

---

## 🔍 주의사항

1. **API 키 보안**: .env 파일은 GitHub에 올리지 않음 (.gitignore 적용)
2. **Obsidian 경로**: Windows 환경 경로 반드시 확인
3. **네트워크**: Google Gemini API 호출 필요
4. **인코딩**: 모든 파일 UTF-8 인코딩

---

## ✅ 작업 완료 체크리스트

- [ ] RSS 뉴스 10개 수집
- [ ] Google Gemini로 분석 완료
- [ ] Markdown 보고서 생성
- [ ] Obsidian에 파일 저장됨
- [ ] 파일명이 Week {N} - K-Content Trends [{year}].md 형식
- [ ] Obsidian에서 파일 자동 인식됨
