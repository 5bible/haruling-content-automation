# HaruLing Content Automation - Claude 오케스트레이터

## 📊 프로젝트 개요
HaruLing 한국어 학습 서비스를 위한 K-콘텐츠 주간 뉴스 자동화 시스템

**역할 분리**
- 이 파일(CLAUDE.md) : 전체 흐름 조율 — 무엇을, 어떤 순서로
- skills/ 폴더      : 각 단계의 구체적 실행 방법

---

## 🔄 전체 워크플로우

```
[실행 트리거: "하루링 콘텐츠 주간 보고서 생성해줘"]
  ↓
Step 1: 뉴스 수집
  - read_file("skills/collect-news/SKILL.md") 로 지시사항 읽기
  - 지시에 따라 RSS 수집 실행
  - 결과(JSON)를 컨텍스트에 보관
  ↓
Step 2: 분석 및 보고서 작성
  - read_file("skills/analyze-content/SKILL.md") 로 지시사항 읽기
  - Step 1의 JSON 결과를 그대로 사용하여 보고서 작성
  - 완성된 Markdown을 컨텍스트에 보관
  ↓
Step 3: Obsidian 저장
  - read_file("skills/save-to-obsidian/SKILL.md") 로 지시사항 읽기
  - Step 2의 Markdown을 지정 경로에 저장
  ↓
[완료: 저장된 파일 경로를 사용자에게 보고]
```

---

## 📦 스킬 간 데이터 전달 방식

각 스킬의 결과는 별도 파일 저장 없이 **Claude 컨텍스트(대화 메모리)에서 직접 전달**됩니다.

- Step 1 → Step 2 : 수집된 기사 JSON 목록을 컨텍스트에 유지
- Step 2 → Step 3 : 완성된 Markdown 보고서 전문을 컨텍스트에 유지
- 중간 임시 파일 생성 불필요

---

## 📋 스킬 파일 경로

| 스킬 | 파일 경로 |
|------|-----------|
| 뉴스 수집 | skills/collect-news/SKILL.md |
| 분석 및 작성 | skills/analyze-content/SKILL.md |
| Obsidian 저장 | skills/save-to-obsidian/SKILL.md |

---

## ⚙️ 환경 설정

- Obsidian 저장 경로: `C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\`
- 파일명 형식: `Week {N} - K-Content Trends [{year}].md`
- 인코딩: UTF-8

---

## ✅ 완료 조건

- [ ] RSS 피드에서 뉴스 수집 완료 (최대 10개)
- [ ] 주간 보고서 Markdown 작성 완료 (Week 번호 포함)
- [ ] Obsidian vault에 파일 저장 완료
- [ ] 사용자에게 저장 경로 및 파일명 보고

---

## 🚨 저장 단계 필수 주의사항

Step 3 실행 시, 보고서를 채팅창에 출력하는 것으로 완료하지 않습니다.
반드시 Desktop Commander write_file 도구를 직접 호출하여 Obsidian에 파일을 저장해야 합니다.
도구 호출 성공 응답을 받은 후에만 완료로 간주합니다.
