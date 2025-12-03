---
description: 오늘 하루 Claude Code로 뭘 했는지 활동 요약을 보여줍니다
---

오늘 하루 동안 Claude Code로 무엇을 했는지 **세션별로** 분석해서 보여줘.

## 실행 단계

1. **오늘 수정된 세션 파일 찾기**
   ```bash
   # 오늘 수정된 세션 파일들 찾기 (agent 파일 제외)
   find ~/.claude/projects/ -name "*.jsonl" -mtime 0 ! -name "agent-*" -exec ls -la {} \;
   ```

2. **각 세션별 요약 추출**
   - 각 세션 파일에서 `"type":"summary"` 항목을 찾아 세션 주제 파악
   - 세션 파일명에서 프로젝트명 추출 (경로에서 파싱)
   ```bash
   grep '"type":"summary"' [세션파일] | jq -r '.summary'
   ```

3. **히스토리에서 오늘 프롬프트 수 집계**
   ```bash
   # 오늘 자정 timestamp prefix 계산 (밀리초 기준 앞 5자리)
   TODAY_PREFIX=$(date -d "today 00:00:00" +%s | cut -c1-5)

   # 오늘 timestamp prefix로 필터링
   grep -a "\"timestamp\":${TODAY_PREFIX}" ~/.claude/history.jsonl | jq -r '.project | split("/") | .[-1]' 2>/dev/null | sort | uniq -c | sort -rn
   ```

   **중요**: timestamp prefix는 매일 바뀌므로 반드시 동적으로 계산해야 함

4. **결과를 세션 기반 마크다운으로 출력**

```markdown
## 📊 오늘의 Claude Code 활동 (YYYY-MM-DD)

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

5. **세션 시간순 정렬**
   - 파일 수정 시간 기준으로 정렬해서 시간 흐름대로 보여주기

지금 바로 위 단계들을 실행해서 세션별로 정리된 결과를 보여줘.
