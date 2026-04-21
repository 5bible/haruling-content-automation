# HaruLing Content Automation

K-콘텐츠 뉴스를 자동으로 수집하고, Claude AI가 분석하여 주간 보고서를 생성하는 자동화 도구입니다.

## 🎯 기능

- 📰 RSS 뉴스 수집 (Google News + 한국 언론사 총 7개 피드)
- 🤖 Claude AI 직접 분석 (외부 API 불필요)
- 📝 Obsidian vault에 .md 파일 자동 저장

## 🔄 작동 방식

1. Claude Desktop에서 실행 요청
2. Claude가 RSS 피드 7개에서 뉴스 수집 (최대 10개)
3. Claude가 K-콘텐츠 트렌드 분석 및 보고서 작성
4. Desktop Commander로 Obsidian에 자동 저장

## 📁 구조

```
haruling-content-automation/
├── CLAUDE.md              ← Claude 자동화 지시사항
├── README.md              ← 이 파일
├── .gitignore
└── config/
    ├── news_sources.yaml  ← RSS 피드 목록
    └── prompts.yaml       ← 분석 프롬프트 템플릿
```

## 🚀 실행 방법

Claude Desktop에서 아래와 같이 요청하세요:

```
HaruLing 주간 K-콘텐츠 보고서를 생성해줘
```

Claude가 CLAUDE.md의 지시에 따라 자동으로 수집 → 분석 → 저장까지 수행합니다.

## 📂 저장 위치

```
C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\
Week {N} - K-Content Trends [{year}].md
```
