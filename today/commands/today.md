---
description: 오늘 하루 Claude Code로 뭘 했는지 활동 요약을 보여줍니다
---

오늘 하루 동안 Claude Code로 무엇을 했는지 분석해서 보여줘.

## 실행 단계

1. **오늘 날짜의 timestamp prefix 계산**
   - 오늘 자정 기준 Unix timestamp (초 단위)의 앞 5자리를 구해
   - 예: `date +%s` 결과가 `1733180400`이면 prefix는 `17331` 또는 `17646`

2. **히스토리에서 오늘 항목 추출**
   ```bash
   # 오늘 timestamp prefix로 필터링 (binary file 대응)
   grep -a '"timestamp":17646' ~/.claude/history.jsonl | wc -l
   ```

3. **프로젝트별 집계**
   ```bash
   grep -a '"timestamp":17646' ~/.claude/history.jsonl | jq -r '.project | split("/") | .[-1]' 2>/dev/null | sort | uniq -c | sort -rn
   ```

4. **각 프로젝트별 주요 프롬프트 확인**
   - 각 프로젝트에서 어떤 작업을 했는지 프롬프트 내용 샘플링

5. **결과를 마크다운으로 출력**

```markdown
## 📊 오늘의 Claude Code 활동 (YYYY-MM-DD)

### 총계
- 총 프롬프트: N개
- 작업한 프로젝트: N개

### 프로젝트별 활동
| 프로젝트 | 프롬프트 수 |
|---------|-----------|
| project-a | 30 |

### 주요 작업 내용
- **project-a**: [주요 작업 요약]
```

지금 바로 위 단계들을 실행해서 결과를 보여줘.
