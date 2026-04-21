# SKILL: RSS 뉴스 수집 (collect-news)

## 📌 스킬 설명
K-콘텐츠 관련 RSS 피드에서 최신 뉴스를 수집합니다.
CLAUDE.md의 Step 1에서 read_file로 이 파일을 읽은 후 실행됩니다.

## 🔧 입력값
수집 설정은 config/news_sources.yaml의 collection_settings를 따릅니다:
- items_per_week : 10 (최대 수집 기사 수)
- max_age_days   : 7  (수집 기준 기간)
- languages      : english, korean (수집 대상 언어)

RSS 피드 목록도 동일 파일의 feeds 섹션을 사용합니다 (총 7개).

## 📋 실행 절차

1. config/news_sources.yaml 파일을 read_file로 읽어 피드 URL 전체 목록 확인
2. 각 URL에 순서대로 접근하여 피드 파싱
3. 각 기사에서 아래 정보 추출
   - title    : 기사 제목
   - source   : 언론사명
   - link     : 원문 URL
   - published: 발행일시
   - summary  : 요약 (없으면 본문 첫 2문장 사용)
4. 발행일 기준 최근 7일(max_age_days) 이내 기사만 필터링
5. 중복 제거 (동일 제목 또는 동일 링크 기준)
6. 최대 10개(items_per_week) 선별 — 균형 기준:
   - 피드 수(7개) 기준으로 최대한 균등하게 선택 (피드당 1~2개 목표)
   - 동일 피드에서 3개 이상 선택은 다른 피드 기사가 없을 때만 허용
   - 우선순위: 최신 기사 > 요약이 풍부한 기사

## 📤 출력값
아래 형식의 JSON 목록을 Claude 컨텍스트에 보관:

```json
[
  {
    "title": "기사 제목",
    "source": "출처명",
    "link": "https://...",
    "published": "2026-04-21",
    "summary": "기사 요약 내용"
  }
]
```

## ⚠️ 예외 처리
- 특정 피드 접근 실패 시: 해당 피드 건너뛰고 나머지 계속 수집
- 수집 기사 5개 미만 시: 사용자에게 경고 메시지 출력 후 분석 단계 진행
- 요약 없는 기사: 본문 첫 2문장으로 대체
- 인코딩: UTF-8 사용
