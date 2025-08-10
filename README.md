# Crush Terminal Quick Start Guide

Welcome to Crush! This guide will help you get up and running quickly with all the essential features.

## 📚 Table of Contents

- [📍 Configuration Location](#-configuration-location)
- [🚀 Getting Started](#-getting-started)
- [🎯 Core Features](#-core-features)
- [🛠️ AI Tools](#️-ai-tools-what-crush-can-do)
- [⌨️ Essential Keyboard Shortcuts](#️-essential-keyboard-shortcuts)
- [🔒 Safety Features](#-safety-features)
- [💡 Pro Tips](#-pro-tips)
- [🎯 Common Workflows](#-common-workflows)
- [📝 Configuration Examples](#-configuration-examples)
- [🔥 Recommended OpenRouter Models](#-recommended-openrouter-models)
- [🏠 Running Models Locally](#-running-models-locally)
- [🆘 Getting Help](#-getting-help)

## 📍 Configuration Location

Crush uses **JSON** configuration (not YAML). The config file is loaded from these locations (in order of priority):

1. **Local Project Config** (highest priority)
   - `.crush.json` or `crush.json` in your project directory

2. **Global User Config**
   - **macOS/Linux**: `~/.config/crush/crush.json`
   - **Windows**: `%USERPROFILE%\AppData\Local\crush\crush.json`

### Basic Config Example
```json
{
  "providers": {
    "anthropic": {
      "api_key": "$ANTHROPIC_API_KEY"
    }
  },
  "models": {
    "preferred": "claude-3-5-sonnet-latest"
  },
  "options": {
    "theme": "dark"
  }
}
```

## 🚀 Getting Started

### Installation
```bash
# Homebrew (macOS/Linux)
brew install charmbracelet/tap/crush

# npm
npm install -g @charmland/crush

# Go
go install github.com/charmbracelet/crush@latest
```

### First Run
1. Set your API key: `export ANTHROPIC_API_KEY=your-key-here`
2. Start Crush: `crush`
3. Type your question and press Enter!

## 🎯 Core Features

### 1. **AI Chat Interface** 
**Access**: Just type in the main window  
**When to use**: Ask questions, request code changes, get explanations  
**Key shortcuts**:
- `Enter` - Send message
- `Shift+Enter` or `Ctrl+J` - Add newline without sending
- `Ctrl+O` - Open external editor for longer messages

### 2. **File Attachments**
**Access**: `Ctrl+F` or type `/` in the message box  
**When to use**: Give the AI context about specific files  
**Tips**: 
- Crush auto-loads context files like `.cursorrules`, `CRUSH.md`, `CLAUDE.md`
- Remove attachments with `Ctrl+R+{number}` or `Ctrl+R+R` for all

### 3. **Session Management**
**Access**: `Ctrl+N` (new session), `Ctrl+S` (switch session)  
**When to use**: Separate different tasks or topics  
**Benefits**: Keep conversation history organized, switch between contexts

### 4. **Model Switching**
**Access**: `Ctrl+P` then select "Switch Model"  
**When to use**: Change between different AI models mid-conversation  
**Popular models**:
- `claude-3-5-sonnet-latest` - Best for complex coding
- `gpt-4o` - Great all-rounder
- `gemini-2.0-flash-exp` - Fast responses

### 5. **Commands Palette**
**Access**: `Ctrl+P`  
**When to use**: Access any feature quickly  
**Available commands**:
- New Session
- Switch Session
- Switch Model
- Summarize Session (compress long conversations)
- Toggle Sidebar
- Open File Picker
- Toggle Thinking Mode (for reasoning models)
- Toggle Yolo Mode (auto-accept permissions - use carefully!)
- Initialize Project (create CRUSH.md)

## 🛠️ AI Tools (What Crush Can Do)

The AI has access to these tools to help you:

| Tool | What it does | Example use |
|------|-------------|-------------|
| **bash** | Run shell commands | Install packages, run tests |
| **view** | Read files | Examine code before changes |
| **edit** | Modify files | Fix bugs, refactor code |
| **write** | Create new files | Generate new components |
| **ls** | List directories | Explore project structure |
| **glob** | Find files by pattern | Find all `*.test.js` files |
| **grep** | Search in files | Find where a function is used |
| **fetch** | Get web content | Fetch documentation |

## ⌨️ Essential Keyboard Shortcuts

### Global
- `Ctrl+C` - Quit Crush
- `Ctrl+G` - Toggle help menu
- `Ctrl+P` - Commands palette
- `Tab` - Switch focus between panels

### Chat Specific
- `Ctrl+N` - New session
- `Ctrl+F` - Add file attachment
- `Ctrl+D` - Toggle details view (see tool usage)
- `Esc` - Cancel current operation

## 🔒 Safety Features

### Permission System
- **Default**: Crush asks before running commands or editing files
- **Allowed Tools**: Configure auto-allowed tools in config
- **YOLO Mode**: `crush -y` or toggle with `Ctrl+P` (auto-accepts all - be careful!)

### Ignored Files
Crush automatically ignores:
- `.git`, `node_modules`, `dist`, `build` directories
- Binary files and common build artifacts
- Respects `.gitignore` and `.crushignore`

## 💡 Pro Tips

### 1. Project Context Files
Create a `CRUSH.md` file in your project root with:
- Project overview
- Coding conventions
- Important context the AI should know

### 2. Quick File Context
Type `/` in the message box to quickly add files to context

### 3. External Editor
Press `Ctrl+O` to compose in your favorite editor ($EDITOR)

### 4. Session Summarization
Long conversation? Use `Ctrl+P` → "Summarize Session" to compress it

### 5. Debug Mode
Having issues? Run with `crush -d` for debug logging

## 🎯 Common Workflows

### Starting a New Feature
1. `Ctrl+N` - New session for the feature
2. `Ctrl+F` - Attach relevant files
3. Describe what you want to build
4. Review and approve changes

### Debugging Code
1. Attach the problematic file with `/filename`
2. Describe the issue
3. Let Crush analyze and suggest fixes
4. Use `Ctrl+D` to see what tools it's using

### Code Review
1. Attach files to review
2. Ask "Review this code for improvements"
3. Crush will analyze and suggest enhancements

## 📝 Configuration Examples

### Multi-Provider Setup
```json
{
  "providers": {
    "anthropic": {
      "api_key": "$ANTHROPIC_API_KEY"
    },
    "openai": {
      "api_key": "$OPENAI_API_KEY"
    }
  },
  "models": {
    "preferred": "claude-3-5-sonnet-latest",
    "fallback": "gpt-4o"
  }
}
```

### Auto-Allow Safe Tools
```json
{
  "permissions": {
    "allowed_tools": ["view", "ls", "glob", "grep"]
  }
}
```

### LSP Integration (Advanced)
```json
{
  "lsp": {
    "typescript": {
      "command": ["typescript-language-server", "--stdio"]
    }
  }
}
```

## 🔥 Recommended OpenRouter Models

### OpenRouter Setup
**Quick start**: Just set your OpenRouter API key as an environment variable:
```bash
export OPENROUTER_API_KEY=your-key-here
```

**Optional**: For more control, configure in your `crush.json` file:
```json
{
  "providers": {
    "openrouter": {
      "api_key": "$OPENROUTER_API_KEY",
      "base_url": "https://openrouter.ai/api/v1"
    }
  }
}
```

**💡 Pro Tip**: Check [OpenRouter Rankings](https://openrouter.ai/rankings) to see real-time performance comparisons and find the best models for your specific needs. The rankings show actual user preferences for coding, reasoning, and creative tasks.

### Top Model Picks

```
📊 Performance Comparison (Our Favorites)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

⚡ GLM-4.5                   █████████████████░░░ Smart & Fast
   glm-4.5                  Great balance
                            
💨 GLM-4.5-Air               ████████████░░░░░░░░ Speed Demon
   glm-4.5-air              Lightning fast
                            
🌙 Kimi K2                  █████████████████████ The New Beast
   moonshotai/kimi-k2       Massive context, beats everyone
                            
🏆 Qwen QwQ 32B             ████████████████████ Reasoning King
   qwen/qwq-32b             Deep thinking shows its work
                            
🚀 Qwen3 Coder              ███████████████████░ Code Master  
   qwen/qwen-3-coder        Built for programming
                            
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        Speed  ←────────────────────→  Intelligence
```

#### 1. **[GLM-4.5](https://openrouter.ai/glm-4.5)** ⚡
**Model ID**: `glm-4.5`  
**Best for**: Balanced tasks needing both speed and intelligence.

#### 2. **[GLM-4.5-Air](https://openrouter.ai/glm-4.5-air)** 💨
**Model ID**: `glm-4.5-air`  
**Best for**: Rapid iteration and quick fixes when speed matters most.

#### 3. **[Kimi K2](https://openrouter.ai/moonshotai/kimi-k2)** 🌙
**Model ID**: `moonshotai/kimi-k2`  
**Best for**: The new top model - handles massive context windows and complex reasoning perfectly.

#### 4. **[Qwen QwQ 32B](https://openrouter.ai/qwen/qwq-32b)** 🏆
**Model ID**: `qwen/qwq-32b`  
**Best for**: Deep reasoning tasks where you want to see the thinking process.

#### 5. **[Qwen3 Coder](https://openrouter.ai/qwen/qwen-3-coder)** 🚀
**Model ID**: `qwen/qwen-3-coder`  
**Best for**: Pure coding tasks with excellent language support.

### Model Selection Strategy
```json
{
  "models": {
    "preferred": "qwen/qwq-32b",    // For complex work
    "fallback": "glm-4.5-air"       // For quick tasks
  }
}
```

**Pro tip**: Use `Ctrl+P` → "Switch Model" to adapt to your task:
- ⚡ Quick fixes → GLM-4.5-Air
- 🏗️ System design → GLM-4.5  
- 🌙 Complex projects → Kimi K2
- 🧩 Deep debugging → QwQ (shows thinking!)
- 💻 Writing code → Qwen3 Coder

## 🏠 Running Models Locally

For local model support, Crush works with Ollama, LM Studio, and llama.cpp. Simply point to your local server in the config:

```json
{
  "providers": {
    "ollama": {
      "base_url": "http://localhost:11434/v1",
      "api_key": "not-needed"
    }
  }
}
```

Popular local models: `qwen2.5-coder`, `deepseek-coder`, `codellama`. Check [Ollama](https://ollama.com) for quick setup.

## 🆘 Getting Help

- **In-app help**: `Ctrl+G`
- **View logs**: `crush logs`
- **Debug mode**: `crush -d`
- **GitHub Issues**: Report bugs at the Crush repository

## 🎉 You're Ready!

```bash
crush
```