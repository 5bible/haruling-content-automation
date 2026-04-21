# HaruLing Content Automation

## 트리거 문구
- K콘텐츠 수집 시작
- weekly k-content
- krun

## HaruLing 주의사항
HaruLing은 이 프로젝트의 이름입니다.
수집 대상: K-콘텐츠(드라마, K-pop, 아이돌) 뉴스
수집 제외: HaruLing 앱, 경쟁사, 한국어 학습 시장 분석

---

## 실행 규칙
- 형식을 묻지 않는다
- 확인을 요청하지 않는다
- 아티팩트를 생성하지 않는다
- 중간에 멈추지 않는다

---

## 워크플로우

### Step 1
read_file("skills/collect-news/SKILL.md") 를 읽고 RSS 뉴스를 수집한다.
수집된 기사 목록을 메모리에 보관한다.

### Step 2
아래 경로에 Desktop Commander write_file 도구를 호출한다.

저장 경로: C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\Week {N} - K-Content Trends [{year}].md

write_file의 content 파라미터에 수집된 뉴스를 분석한 Markdown을 직접 작성한다.
read_file("skills/analyze-and-save/SKILL.md") 를 읽어 content 형식을 확인한다.

write_file 호출이 성공하면 저장된 경로를 사용자에게 보고한다.
