---
description: 코드 변경사항과 문서를 간단히 동기화합니다 (light)
allowed-tools: Bash(git:*), Read, Write, Edit, Glob
---

코드 작업 완료 후 README와 주요 문서를 간단히 업데이트해줘.

## 실행 단계

1. **변경사항 파악**
   ```bash
   git diff --name-only
   git diff --staged --name-only
   ```

2. **README.md 업데이트**
   - 변경된 기능 반영
   - 사용법 업데이트
   - 버전 정보 확인

3. **결과 보고**
   뭘 바꿨는지 간단히 알려줘.

---

꼼꼼한 동기화가 필요하면 `/sync-full` 사용.
