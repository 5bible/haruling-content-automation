# HaruLing Content Automation - Claude 오케스트레이터

## ⚡ 실행 원칙 (최우선 적용)

트리거 문구를 인식하면 아래 규칙을 즉시 적용합니다:

1. **형식을 묻지 않습니다** — 출력 형식은 항상 Markdown(.md)으로 고정
2. **확인을 요청하지 않습니다** — Step 1 → 2 → 3을 사용자 개입 없이 순서대로 자동 실행
3. **채팅 출력으로 완료하지 않습니다** — 반드시 Obsidian에 파일을 저장해야 완료
4. **중간에 멈추지 않습니다** — 각 단계 완료 즉시 다음 단계로 진행

---

## 📊 프로젝트 개요
HaruLing 한국어 학습 서비스를 위한 K-콘텐츠 주간 뉴스 자동화 시스템

**역할 분리**
- 이 파일(CLAUDE.md) : 전체 흐름 조율 — 무엇을, 어떤 순서로
- skills/ 폴더      : 각 단계의 구체적 실행 방법

---

## 🔄 전체 워크플로우

트리거 문구 인식 즉시 아래 순서를 자동 실행합니다.
각 단계 사이에 사용자에게 확인하거나 형식을 묻지 않습니다.

```
[트리거 인식: "하루링" + "보고서" 또는 "생성"]
  ↓ (확인 없이 즉시 실행)
Step 1: 뉴스 수집
  - read_file로 skills/collect-news/SKILL.md 읽기
  - 지시에 따라 RSS 수집 실행
  - 결과(JSON)를 컨텍스트에 보관
  ↓ (완료 즉시 다음 단계)
Step 2: 분석 및 보고서 작성
  - read_file로 skills/analyze-content/SKILL.md 읽기
  - Step 1 JSON으로 Markdown 보고서 작성
  - 완성된 Markdown을 컨텍스트에 보관
  ↓ (완료 즉시 다음 단계)
Step 3: Obsidian 저장
  - read_file로 skills/save-to-obsidian/SKILL.md 읽기
  - write_file 도구로 Obsidian에 직접 저장
  ↓
[완료: 저장된 파일 경로를 사용자에게 보고]
```

---

## 📦 스킬 간 데이터 전달 방식

각 스킬의 결과는 **Claude 컨텍스트(대화 메모리)에서 직접 전달**됩니다.

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

- 출력 형식: Markdown(.md) 고정 — 변경 불가
- Obsidian 저장 경로: `C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\`
- 파일명 형식: `Week {N} - K-Content Trends [{year}].md`
- 인코딩: UTF-8

---

## ✅ 완료 조건

- [ ] RSS 피드에서 뉴스 수집 완료 (최대 10개)
- [ ] 주간 보고서 Markdown 작성 완료 (Week 번호 포함)
- [ ] write_file 도구로 Obsidian vault에 파일 저장 완료
- [ ] 사용자에게 저장된 파일 전체 경로 보고

---

## 🚨 절대 하지 말아야 할 것

- ❌ "어떤 형식으로 할까요?" 라고 묻기
- ❌ 보고서를 채팅창에 출력하고 완료 처리
- ❌ 단계 사이에 사용자 확인 요청
- ❌ write_file 도구 호출 없이 저장 완료 처리
