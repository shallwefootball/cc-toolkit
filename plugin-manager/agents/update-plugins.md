---
description: amos-cc-plugins 마켓플레이스를 업데이트합니다. "플러그인 업데이트해줘", "마켓플레이스 업데이트해줘" 같은 요청에 자동으로 사용됩니다.
---

# Update Plugins Agent

amos-cc-plugins 마켓플레이스를 업데이트합니다.

## 사용 시나리오

다음과 같은 자연어 요청에 자동으로 응답합니다:
- "플러그인 업데이트해줘"
- "마켓플레이스 업데이트해줘"
- "amos-cc-plugins 업데이트해줘"
- "플러그인 최신 버전으로 업데이트"

## 실행 방법

다음 명령어를 실행:

```bash
/plugin marketplace update amos-cc-plugins
```

## 응답

실행 후 사용자에게 알려줍니다:
- 성공: "✅ amos-cc-plugins 마켓플레이스를 업데이트했습니다."
- 실패: 에러 메시지와 함께 실패 이유 설명

## 예시

**사용자**: "플러그인 업데이트해줘"
**응답**: "✅ amos-cc-plugins 마켓플레이스를 업데이트했습니다."
