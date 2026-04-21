# HaruLing Content Automation - Claude 오케스트레이터

## ⚡ 실행 원칙 (최우선 적용)

### 🔑 트리거 문구
아래 문구 중 하나를 입력받으면 즉시 자동 실행합니다:
- `K콘텐츠 수집 시작`
- `weekly k-content`
- `krun`

### ⚠️ HaruLing은 이 자동화 프로젝트의 이름입니다
- HaruLing에 대한 뉴스를 수집하는 것이 아닙니다
- HaruLing 앱, 경쟁사, 한국어 학습 시장 분석이 아닙니다
- 수집 대상은 오직 K-콘텐츠(드라마, K-pop, 아이돌, 한국 문화) 뉴스입니다

### 실행 규칙
1. 형식을 묻지 않습니다 — 출력 형식은 항상 Markdown(.md)으로 고정
2. 확인을 요청하지 않습니다 — Step 1 → 2 → 3을 자동 실행
3. 채팅 출력으로 완료하지 않습니다 — Obsidian에 파일 저장 후 완료
4. 중간에 멈추지 않습니다

---

## 📊 프로젝트 개요
K-콘텐츠(드라마·K-pop·아이돌)에 관심 있는 **외국인 한국어 학습자**를 위해
매주 K-콘텐츠 뉴스를 수집·분석하여 Obsidian에 주간 보고서를 저장하는 자동화 시스템

---

## 🔄 전체 워크플로우

트리거 문구 인식 즉시 아래 순서를 자동 실행합니다.

```
[트리거 인식]
  ↓
Step 1: K-콘텐츠 뉴스 수집
  - read_file로 skills/collect-news/SKILL.md 읽기
  - 드라마·K-pop·아이돌 뉴스 수집 (HaruLing 관련 뉴스 수집 아님)
  - 결과(JSON)를 컨텍스트에 보관
  ↓
Step 2: 외국인 학습자 관점으로 분석 및 보고서 작성
  - read_file로 skills/analyze-content/SKILL.md 읽기
  - Step 1 JSON으로 Markdown 보고서 작성
  - 완성된 Markdown을 컨텍스트에 보관
  ↓
Step 3: Obsidian 저장
  - read_file로 skills/save-to-obsidian/SKILL.md 읽기
  - write_file 도구로 Obsidian에 직접 저장
  ↓
[완료: 저장된 파일 경로를 사용자에게 보고]
```

---

## 📦 스킬 간 데이터 전달 방식

각 스킬의 결과는 **Claude 컨텍스트에서 직접 전달**됩니다.
- Step 1 → Step 2 : 수집된 기사 JSON 목록
- Step 2 → Step 3 : 완성된 Markdown 보고서 전문
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

- 출력 형식: Markdown(.md) 고정
- Obsidian 저장 경로: `C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\`
- 파일명 형식: `Week {N} - K-Content Trends [{year}].md`
- 인코딩: UTF-8

---

## 🚨 절대 하지 말아야 할 것

- ❌ HaruLing 앱·회사·경쟁사에 대한 뉴스 수집
- ❌ 한국어 학습 시장, 경쟁사 분석
- ❌ "어떤 형식으로 할까요?" 라고 묻기
- ❌ 보고서를 채팅창에 출력하고 완료 처리
- ❌ write_file 도구 호출 없이 저장 완료 처리

---

## ✅ 완료 조건

- [ ] K-콘텐츠(드라마·K-pop·아이돌) 뉴스 수집 완료
- [ ] 외국인 학습자 관점 보고서 작성 완료
- [ ] write_file로 Obsidian vault에 파일 저장 완료
- [ ] 사용자에게 저장된 파일 전체 경로 보고
