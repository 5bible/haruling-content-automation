# SKILL: Obsidian 저장 (save-to-obsidian)

## 📌 스킬 설명
analyze-content에서 완성된 Markdown 보고서를 Obsidian vault에 저장합니다.
CLAUDE.md의 Step 3에서 read_file로 이 파일을 읽은 후 실행됩니다.

---

## ⚡ 핵심 원칙
**보고서를 채팅창에 출력하거나 보여주는 것으로 이 단계를 완료하지 않습니다.**
반드시 아래 절차대로 Desktop Commander write_file 도구를 직접 호출하여 파일을 저장해야 합니다.
저장이 완료된 후에만 완료로 간주합니다.

---

## 🔧 입력값
- analyze-content 스킬이 컨텍스트에 보관한 완성된 Markdown 보고서 전문
- 보고서의 title 프론트매터 (파일명 결정에 사용)

---

## 📋 실행 절차 (반드시 순서대로 도구 호출)

### 1단계: 파일명 결정
analyze-content 보고서의 title 프론트매터 값을 파일명으로 사용합니다.
- 형식: `Week {N} - K-Content Trends [{year}].md`
- 예시: `Week 17 - K-Content Trends [2026].md`
- 주차 번호는 analyze-content에서 이미 계산 완료 — 재계산 불필요

### 2단계: 저장 전체 경로 조합
```
C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\Week {N} - K-Content Trends [{year}].md
```

### 3단계: 파일 존재 여부 확인 (도구 호출)
Desktop Commander get_file_info 도구를 호출하여 위 전체 경로를 확인합니다.
- 파일 없음 → 4단계로 바로 진행
- 파일 있음 → 사용자에게 덮어쓰기 여부를 묻고 승인 후 4단계 진행

### 4단계: 파일 저장 (도구 호출 — 필수)
Desktop Commander write_file 도구를 아래 인자로 즉시 호출합니다:
- path : `C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\Week {N} - K-Content Trends [{year}].md`
- content : analyze-content 보고서 전문 (Markdown 그대로)
- mode : rewrite

이 도구 호출 없이 이 단계를 완료로 처리하면 안 됩니다.

### 5단계: 완료 보고
write_file 호출이 성공한 후, 사용자에게 아래 정보를 출력합니다:
- ✅ 저장 완료 메시지
- 저장된 파일 전체 경로
- 파일명
- 수집 기사 수 및 주차 정보

---

## ⚠️ 주의사항
- 저장 전에 보고서를 채팅창에 출력하지 않습니다 (요청 시에만 출력)
- 저장 경로가 존재하지 않을 경우 오류 메시지 출력 (경로 자동 생성 금지)
- 덮어쓰기는 반드시 사용자 확인 후 진행
- 인코딩: UTF-8
