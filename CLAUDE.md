# HaruLing Content Automation - Claude 오케스트레이터

## 실행 원칙 (최우선 적용)

트리거 문구 인식 시 아래 규칙을 즉시 적용합니다:
1. 형식을 묻지 않습니다 — 항상 Markdown(.md) 고정
2. 확인을 요청하지 않습니다 — 자동 실행
3. 채팅 출력으로 완료하지 않습니다 — Obsidian 저장 후 완료
4. 중간에 멈추지 않습니다

---

## 트리거 문구
- K콘텐츠 수집 시작
- weekly k-content
- krun

---

## HaruLing 이름 주의사항
HaruLing은 이 자동화 프로젝트의 이름입니다.
수집 대상은 K-콘텐츠(드라마, K-pop, 아이돌) 뉴스이며,
HaruLing 앱, 경쟁사, 한국어 학습 시장 분석이 아닙니다.

---

## 전체 워크플로우 (2단계)

```
[트리거 인식]
  ↓
Step 1: K-콘텐츠 뉴스 수집
  → read_file("skills/collect-news/SKILL.md") 읽고 실행
  → 드라마/K-pop/아이돌 뉴스 수집
  → 결과 JSON을 컨텍스트에 보관
  ↓
Step 2: 분석 + Obsidian 저장 (한 번에 처리)
  → read_file("skills/analyze-and-save/SKILL.md") 읽고 실행
  → Step 1 결과로 보고서 작성 후 즉시 PowerShell로 Obsidian 저장
  → 채팅에 보고서 출력 전에 저장 먼저 실행
  ↓
[완료: 저장 경로 보고]
```

---

## 스킬 파일 경로

| 스킬 | 경로 |
|------|------|
| 뉴스 수집 | skills/collect-news/SKILL.md |
| 분석+저장 | skills/analyze-and-save/SKILL.md |

---

## 환경 설정

- 저장 형식: Markdown(.md) 고정
- 저장 경로: C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\
- 파일명: Week {N} - K-Content Trends [{year}].md
- 인코딩: UTF-8

---

## 절대 하지 말 것

- HaruLing 앱/경쟁사/시장 분석 뉴스 수집
- "어떤 형식으로 할까요?" 묻기
- 채팅 출력으로 저장 완료 처리
- PowerShell 호출 없이 저장 완료 처리
