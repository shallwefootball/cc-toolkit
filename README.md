# Amos's Claude Code Plugins

Useful Claude Code plugins collection.

## Available Plugins

### analyze-repo

GitHub 레포지토리를 클론하고 구조를 분석하여 마크다운 문서로 정리합니다.

**Features:**
- 두 가지 실행 모드:
  - URL 제공: GitHub 레포지토리 자동 클론 (`~/Documents/clone/` 디렉토리에)
  - URL 없이 실행: 현재 디렉토리가 git 레포면 바로 분석
- 레포지토리 메타데이터 수집 (Stars, Forks, 라이선스, 마지막 커밋 등)
- 프로젝트 구조 및 기술 스택 분석
- 핵심 컴포넌트와 아키텍처 분석
- `REPO-ANALYSIS.md` 파일 자동 생성 (한국어/영어 혼용)

### open-intellij

현재 디렉토리를 IntelliJ IDEA CE에서 엽니다.

**Features:**
- 현재 작업 디렉토리를 IntelliJ IDEA CE로 바로 열기
- 간단한 원라이너 커맨드

## Installation

### Option 1: Using Plugin Marketplace (Recommended)

```bash
# Add the marketplace
/plugin marketplace add shallwefootball/amos-cc-plugins

# Install the plugins you need
/plugin install analyze-repo@amos-cc-plugins
/plugin install open-intellij@amos-cc-plugins
```

### Option 2: Manual Installation

1. Clone this repository:
```bash
git clone https://github.com/shallwefootball/amos-cc-plugins.git
cd amos-cc-plugins
```

2. Copy the plugin to your Claude Code commands directory:
```bash
# For global installation (available in all projects)
cp -r analyze-repo/commands/* ~/.claude/commands/
cp -r open-intellij/commands/* ~/.claude/commands/

# For project-specific installation
cp -r analyze-repo/commands/* /path/to/your/project/.claude/commands/
cp -r open-intellij/commands/* /path/to/your/project/.claude/commands/
```

## Usage

### analyze-repo

**Mode 1: Analyze remote repository**
```bash
/analyze-repo https://github.com/owner/repo-name
```

The command will:
1. Clone the repository to `~/Documents/clone/[repo-name]`
2. Analyze the codebase structure
3. Generate `REPO-ANALYSIS.md` in the repository root

**Mode 2: Analyze current directory**
```bash
/analyze-repo
```

The command will:
1. Check if current directory is a git repository
2. Analyze the codebase structure
3. Generate `REPO-ANALYSIS.md` in the current directory

**Example output structure:**
```markdown
# [Repository Name] 분석

## 레포지토리 정보
- **GitHub URL**: ...
- **Stars**: ⭐ ...
- **Last Commit**: 📅 ...

## 개요
[프로젝트 설명]

## 기술 스택
[언어, 프레임워크, 라이브러리]

## 프로젝트 구조
[디렉토리 구조]

## 핵심 컴포넌트
[주요 파일과 모듈]

## 아키텍처
[아키텍처 패턴, 데이터 흐름]
```

### open-intellij

```bash
/intellij
```

Opens the current directory in IntelliJ IDEA CE.

## Requirements

- [Claude Code](https://code.claude.com/) CLI installed
- Git for cloning repositories
- GitHub CLI (`gh`) for repository metadata (optional, for analyze-repo)
- IntelliJ IDEA CE (for open-intellij)

## Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest new plugins
- Submit pull requests

## License

MIT

---

Made with Claude Code
