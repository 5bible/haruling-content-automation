# SKILL: Obsidian 저장 (save-to-obsidian)

## 📌 스킬 설명
analyze-content에서 완성된 Markdown 보고서를 Obsidian vault에 저장합니다.
CLAUDE.md의 Step 3에서 read_file로 이 파일을 읽은 후 실행됩니다.

## ⚡ 핵심 원칙
보고서를 채팅창에 출력하거나 보여주는 것으로 이 단계를 완료하지 않습니다.
반드시 PowerShell 도구를 호출하여 파일을 실제로 저장해야 완료입니다.

---

## 🔧 입력값
- analyze-content 스킬이 컨텍스트에 보관한 완성된 Markdown 보고서 전문
- 보고서의 title 프론트매터 (파일명 결정에 사용)

---

## 📋 실행 절차

### 1단계: 파일명 결정
analyze-content 보고서의 title 프론트매터 값을 파일명으로 사용합니다.
- 형식: `Week {N} - K-Content Trends [{year}].md`
- 예시: `Week 17 - K-Content Trends [2026].md`

### 2단계: 저장 경로
```
C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\
```

### 3단계: 파일 저장 (PowerShell 도구 호출 — 필수)
Windows-MCP PowerShell 도구를 아래 형식으로 즉시 호출합니다:

```powershell
$content = @'
(보고서 Markdown 전문을 여기에 그대로 삽입)
'@
$path = "C:\Users\user\Documents\Obsidian Vault\40. HaruLing\3.뉴스콘텐츠\Week {N} - K-Content Trends [{year}].md"
[System.IO.File]::WriteAllText($path, $content, [System.Text.Encoding]::UTF8)
Write-Host "저장 완료: $path"
Test-Path $path
```

Desktop Commander write_file 대신 반드시 PowerShell을 사용합니다.
Desktop Commander는 타임아웃이 발생할 수 있어 사용하지 않습니다.

### 4단계: 완료 보고
PowerShell 실행 결과가 True이면 성공입니다.
사용자에게 저장된 파일 전체 경로와 파일명을 보고합니다.

---

## ⚠️ 주의사항
- Desktop Commander write_file 사용 금지 (타임아웃 발생)
- PowerShell [System.IO.File]::WriteAllText 사용 (UTF-8 인코딩 보장)
- 저장 후 Test-Path로 파일 존재 확인 필수
- 저장 경로가 없을 경우 오류 메시지 출력 (경로 자동 생성 금지)
