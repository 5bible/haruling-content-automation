# SKILL: 분석 + Obsidian 저장 (analyze-and-save)

## 📌 스킬 설명
collect-news 결과를 분석하고, 작성 즉시 Obsidian에 저장합니다.
분석과 저장을 한 단계에서 처리하여 내용 유실을 방지합니다.
CLAUDE.md의 Step 2에서 read_file로 이 파일을 읽은 후 실행됩니다.

## 🎯 목표
K-콘텐츠에 관심 있는 외국인 학습자가 흥미롭게 읽을 수 있는
주간 트렌드 보고서를 작성하고 즉시 Obsidian에 저장합니다.

---

## 📋 실행 절차

### 1단계: 주차 번호 계산
현재 날짜 기준 ISO 8601 주차 번호를 계산합니다.
기준: 해당 연도의 첫 번째 목요일이 포함된 주 = Week 1
예시: 2026-04-21 → Week 17, 연도 2026

### 2단계: 보고서 Markdown 작성
collect-news가 수집한 K-콘텐츠 기사만을 바탕으로 아래 형식으로 작성합니다.

작성 관점: K-콘텐츠를 좋아하는 외국인 팬이자 한국어 교육자
주의: HaruLing 앱, 경쟁사, 시장 분석 내용은 절대 포함하지 않음
주의: 수집된 K-콘텐츠 기사(드라마, K-pop, 아이돌) 내용만 사용할 것

보고서 형식:

---
title: "Week {N} - K-Content Trends [{year}]"
date: {YYYY-MM-DD}
tags: [K-콘텐츠, 주간트렌드, 외국인학습자]
---

# 이번 주 K-콘텐츠, 외국인들은 뭐에 빠졌을까? (Week {N})
작성일: {YYYY-MM-DD} | 수집 기사 수: {N}개

## 이번 주 가장 핫한 K-콘텐츠
(외국인 팬들이 가장 열광한 것 중심, 3~5줄)

## 카테고리별 화제
### 드라마/영화
### 가요/K-pop
### 아이돌/엔터

## 외국인이 "이거 뭐야?!" 했을 한국 문화 포인트
(뉴스에 등장한 낯선 한국 문화 표현, 짧은 설명 포함)

## 이 뉴스로 배울 수 있는 한국어 표현
(실제 뉴스에서 나온 표현 2~3가지, 뜻과 예시)

## 이번 주 뉴스 목록
| 제목 | 출처 | 링크 |
|------|------|------|

### 3단계: 작성 완료 즉시 PowerShell로 저장 (보고서를 채팅에 출력하기 전에 저장)

보고서 작성이 완료되면 채팅에 출력하기 전에 아래 PowerShell을 즉시 실행합니다.
Windows-MCP PowerShell 도구를 호출하여 실행합니다.

파일명: Week {N} - K-Content Trends [{year}].md
저장 경로: C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\

PowerShell 명령:
$path = "C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\Week {N} - K-Content Trends [{year}].md"
$content = (작성한 보고서 Markdown 전문)
[System.IO.File]::WriteAllText($path, $content, [System.Text.Encoding]::UTF8)
if (Test-Path $path) { Write-Host "저장 완료: $path" } else { Write-Host "저장 실패" }

### 4단계: 결과 보고
저장 성공 시 사용자에게 아래 내용을 보고합니다:
- 저장된 파일 경로
- 파일명
- 수집된 기사 수 및 주요 내용 요약 3줄

---

## 절대 하지 말 것
- 보고서에 HaruLing 앱/경쟁사/시장분석 내용 포함 금지
- 채팅에 보고서를 출력하고 저장 생략 금지
- 다른 파일명 형식 사용 금지
- PowerShell 도구 호출 없이 저장 완료 처리 금지
