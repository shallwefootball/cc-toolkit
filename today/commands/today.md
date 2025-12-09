---
description: 오늘 하루 Claude Code로 뭘 했는지 활동 요약을 보여줍니다
---

Claude Code로 무엇을 했는지 **세션별로** 분석해서 보여줘.

## 실행 단계

1. **날짜 선택**
   먼저 AskUserQuestion 도구로 사용자에게 날짜를 물어봐:
   - 질문: "어느 날짜의 활동을 볼까요?"
   - 선택지: "오늘", "어제"

2. **선택한 날짜에 맞게 세션 파일 찾기**
   ```bash
   # 오늘 선택 시: -mtime 0
   find ~/.claude/projects/ -name "*.jsonl" -mtime 0 ! -name "agent-*" -exec ls -la {} \;

   # 어제 선택 시: -mtime 1
   find ~/.claude/projects/ -name "*.jsonl" -mtime 1 ! -name "agent-*" -exec ls -la {} \;
   ```

3. **각 세션별 요약 추출**
   - 각 세션 파일에서 `"type":"summary"` 항목을 찾아 세션 주제 파악
   - 세션 파일명에서 프로젝트명 추출 (경로에서 파싱)
   ```bash
   grep '"type":"summary"' [세션파일] | jq -r '.summary'
   ```

4. **히스토리에서 프롬프트 수 집계**
   ```bash
   # 오늘 선택 시
   DATE_PREFIX=$(date -d "today 00:00:00" +%s | cut -c1-5)

   # 어제 선택 시
   DATE_PREFIX=$(date -d "yesterday 00:00:00" +%s | cut -c1-5)

   # 해당 날짜 timestamp prefix로 필터링
   grep -a "\"timestamp\":${DATE_PREFIX}" ~/.claude/history.jsonl | jq -r '.project | split("/") | .[-1]' 2>/dev/null | sort | uniq -c | sort -rn
   ```

   **중요**: timestamp prefix는 매일 바뀌므로 반드시 동적으로 계산해야 함

5. **결과를 세션 기반 마크다운으로 출력**

```markdown
## 📊 Claude Code 활동 (YYYY-MM-DD)

### 총계
- 총 프롬프트: N개
- 작업한 프로젝트: N개
- 세션 수: N개

### 세션별 활동

#### 🖥️ project-a
| 시간 | 세션 | 주요 작업 |
|-----|------|---------|
| 09:30 | WiFi 모니터링 설정 | Grafana 대시보드 업데이트 |
| 14:00 | Docker 업데이트 | OpenWebUI 버전 업그레이드 |

#### 🚀 project-b
| 시간 | 세션 | 주요 작업 |
|-----|------|---------|
| 10:00 | TF-710 작업 | PR 생성 및 배포 |

### 프로젝트별 프롬프트 수
| 프로젝트 | 프롬프트 수 |
|---------|-----------|
| project-a | 30 |
```

6. **세션 시간순 정렬**
   - 파일 수정 시간 기준으로 정렬해서 시간 흐름대로 보여주기

지금 바로 위 단계들을 실행해서 세션별로 정리된 결과를 보여줘.
