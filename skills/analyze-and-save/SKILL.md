# SKILL: analyze-and-save

CLAUDE.md의 Step 2에서 read_file로 이 파일을 읽는다.
이 스킬의 목적은 Desktop Commander write_file 도구를 호출하는 것이다.
아티팩트 생성, 채팅 출력은 하지 않는다.

---

## write_file content 형식

현재 날짜로 주차 번호를 계산한다 (ISO 8601 기준).
예: 2026-04-21 → Week 17, year 2026

write_file의 content 파라미터에 아래 Markdown을 수집된 뉴스로 채워서 전달한다:

---
title: "Week {N} - K-Content Trends [{year}]"
date: {YYYY-MM-DD}
tags: [K-콘텐츠, 주간트렌드, 외국인학습자]
---

# 이번 주 K-콘텐츠, 외국인들은 뭐에 빠졌을까? (Week {N})
> 작성일: {YYYY-MM-DD} | 수집 기사 수: {n}개

## 🔥 이번 주 가장 핫한 K-콘텐츠
(내용 작성)

## 📺 카테고리별 화제
### 드라마/영화
### 가요/K-pop
### 아이돌/엔터

## 🌏 외국인이 "이거 뭐야?!" 했을 한국 문화 포인트
(내용 작성)

## 💬 이 뉴스로 배울 수 있는 한국어 표현
(내용 작성)

## 📰 이번 주 뉴스 목록
| 제목 | 출처 | 링크 |
|------|------|------|
(기사 목록)

---

작성 관점: K-콘텐츠를 좋아하는 외국인 팬이자 한국어 교육자
HaruLing 앱, 경쟁사, 시장 분석 내용 포함 금지
