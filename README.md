# Claude Code Plugins

Useful Claude Code plugins collection by wecouldbe.

## Available Plugins

### analyze-repo

GitHub 레포지토리를 클론하고 구조를 분석하여 마크다운 문서로 정리합니다.

**Features:**
- GitHub 레포지토리 자동 클론 (`~/Documents/clone/` 디렉토리에)
- 레포지토리 메타데이터 수집 (Stars, Forks, 라이선스, 마지막 커밋 등)
- 프로젝트 구조 및 기술 스택 분석
- 핵심 컴포넌트와 아키텍처 분석
- `REPO-ANALYSIS.md` 파일 자동 생성

## Installation

### Option 1: Using Plugin Marketplace (Recommended)

```bash
# Add the marketplace
/plugin marketplace add wecouldbe/claude-code-plugins

# Install the plugin you need
/plugin install analyze-repo
```

### Option 2: Manual Installation

1. Clone this repository:
```bash
git clone https://github.com/wecouldbe/claude-code-plugins.git
cd claude-code-plugins
```

2. Copy the plugin to your Claude Code commands directory:
```bash
# For global installation (available in all projects)
cp -r analyze-repo/commands/* ~/.claude/commands/

# For project-specific installation
cp -r analyze-repo/commands/* /path/to/your/project/.claude/commands/
```

## Usage

### analyze-repo

```bash
/analyze-repo https://github.com/owner/repo-name
```

The command will:
1. Clone the repository to `~/Documents/clone/[repo-name]`
2. Analyze the codebase structure
3. Generate `REPO-ANALYSIS.md` in the repository root

Example output structure:
```markdown
# [Repository Name] Analysis

## Repository Information
- **GitHub URL**: ...
- **Stars**: ⭐ ...
- **Last Commit**: 📅 ...

## Overview
[Project description]

## Tech Stack
[Languages, frameworks, libraries]

## Project Structure
[Directory structure]

## Core Components
[Key files and modules]

## Architecture
[Design patterns and data flow]
```

## Requirements

- [Claude Code](https://code.claude.com/) CLI installed
- GitHub CLI (`gh`) for repository metadata (optional)
- Git for cloning repositories

## Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest new plugins
- Submit pull requests

## License

MIT

---

Made with Claude Code
