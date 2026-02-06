# FreeClaw - Complete Project Brief

## Overview

FreeClaw is a **one-click setup wizard** that allows non-technical users to deploy their own AI chatbot (OpenClaw) on their personal computer. The entire setup should work without any technical knowledge - user downloads a file, double-clicks, and their bot is running in Telegram.

## Goal

**Zero friction setup.** A user with NO technical background should be able to:
1. Visit the website
2. Go through a simple wizard (pick platform, enter API keys)
3. Download ONE file
4. Double-click that file
5. Have their AI bot running in Telegram within 2-3 minutes
6. Bot auto-starts when they log into their computer

## Current State

- **Website:** https://ornate-creponne-5dd1f6.netlify.app/
- **GitHub Repo:** https://github.com/andreycpu/freeclaw (private)
- **Hosting:** Netlify (auto-deploys from GitHub)
- **Tech Stack:** Pure HTML/CSS/JavaScript (single index.html file)

## The Problem We're Solving

OpenClaw requires:
- Node.js installed
- Git installed (for some npm dependencies)
- npm install openclaw
- Config file setup
- Running `openclaw gateway start`

This is too complex for non-technical users. FreeClaw bundles everything.

## Windows Setup Script Requirements

The downloaded `.bat` file must:

### 1. Download & Bundle Dependencies (Portable, No System Install)
- **Node.js 22.13.0+** (OpenClaw requires >=22.12.0)
  - Download: `https://nodejs.org/dist/v22.13.0/node-v22.13.0-win-x64.zip`
  - Extract to `%USERPROFILE%\freeclaw\node\`
  
- **Git (MinGit portable)**
  - Download: `https://github.com/git-for-windows/git/releases/download/v2.43.0.windows.1/MinGit-2.43.0-64-bit.zip`
  - Extract to `%USERPROFILE%\freeclaw\git\`

### 2. Set PATH for Session
Both `node` and `git\cmd` must be in PATH before running npm:
```batch
set "PATH=%CD%\node;%CD%\git\cmd;%PATH%"
```

### 3. Install OpenClaw
```batch
call node\npm.cmd init -y
call node\npm.cmd install openclaw
```

### 4. Write Config Files
The wizard collects:
- Platform (Telegram)
- AI Provider (Anthropic/OpenAI/Google/Groq)
- API Key
- Bot Token (from BotFather)
- Bot Username
- User's name
- Personality style
- Custom instructions

These get embedded into the .bat file and written to:
- `config.yaml` - OpenClaw configuration
- `SOUL.md` - Bot personality
- `USER.md` - Info about the user
- `AGENTS.md` - Workspace guide

### 5. Create Auto-Start Script
Create `Start.bat` that:
- Sets PATH to include local node and git
- Runs `openclaw gateway start`
- Copy to Windows Startup folder for auto-start on login

### 6. Start Bot & Open Telegram
- Run openclaw gateway in background
- Open Telegram to the bot chat: `https://t.me/{botUsername}`

### 7. User Experience Requirements
- Hide all scary terminal output (PowerShell progress, npm warnings)
- Show clean progress messages only
- Window must stay open to show status
- Clear success/error messages

## Mac/Linux Setup Script

Similar approach but using shell script:
- Download Node.js tarball
- Install Homebrew if needed (Mac)
- Same flow: download, extract, npm install, config, start

## Website Wizard Flow

### Step 1: Platform Selection
- Telegram (primary, fully supported)
- Discord (secondary)
- WhatsApp (secondary)
- Slack (secondary)

### Step 2: AI Model Selection
- Anthropic Claude (recommended)
- OpenAI GPT-4
- Google Gemini
- Groq

### Step 3: Setup Guide
- Shows how to get API key for selected provider
- Shows how to create Telegram bot via BotFather
- Input fields for API key and bot token

### Step 4: Personality
- User enters their name
- Selects personality style (Chill, Professional, Friendly, Witty, Minimal)
- Optional custom instructions

### Step 5: Download
- Generates .bat (Windows) or .command (Mac) with all config embedded
- Download button

### Step 6: Run Instructions
- Simple checklist: "Double-click the file"
- Shows what to expect

### Step 7: Done
- Success message
- Donate button (Polar)
- Share on X button

## Donation Integration

**Polar Product ID:** `b3f01423-1476-4359-9a0b-34bc397aac58`

Donate button should open:
```
https://polar.sh/checkout?productId=b3f01423-1476-4359-9a0b-34bc397aac58
```

## Design Requirements

- Dark theme (bg: #0a0a0f)
- Purple/blue gradient accents
- Glass morphism cards
- Clean, minimal, modern
- Mobile responsive
- Friendly and non-intimidating for non-techies

## Config File Formats

### config.yaml
```yaml
model: anthropic/claude-sonnet-4-20250514

providers:
  anthropic:
    apiKey: "sk-ant-xxxxx"

channels:
  telegram:
    botToken: "123456:ABC-xxxxx"
    allowedUsers: ["*"]
```

### SOUL.md
```markdown
# SOUL.md - Who You Are

## Identity
You are a personal AI assistant for {userName}. Your personality style is **{style}**.

## Core Behavior
{styleDescription}

## Special Instructions
{customInstructions}
```

## Known Issues to Fix

1. **PATH not persistent** - When user opens new terminal, node/git not in PATH
   - Solution: Start.bat must set PATH before running openclaw
   
2. **npm post-install scripts need node in PATH** - Some packages run scripts that call `node` directly
   - Solution: Set PATH BEFORE npm install

3. **Node version** - OpenClaw requires Node 22.12+, we were using 20.11
   - Solution: Use Node 22.13.0

4. **Git required** - Some npm dependencies use git
   - Solution: Bundle MinGit portable

## File Structure

```
%USERPROFILE%\freeclaw\
├── node\                 # Portable Node.js
│   ├── node.exe
│   ├── npm.cmd
│   └── ...
├── git\                  # Portable Git
│   └── cmd\
│       └── git.exe
├── node_modules\         # npm packages
│   └── .bin\
│       └── openclaw.cmd
├── config.yaml           # OpenClaw config
├── SOUL.md              # Bot personality
├── USER.md              # User info
├── AGENTS.md            # Workspace guide
└── Start.bat            # Launcher script
```

## Testing Checklist

- [ ] Fresh Windows PC with nothing installed can run setup
- [ ] Node.js downloads and extracts correctly
- [ ] Git downloads and extracts correctly
- [ ] npm install openclaw succeeds without errors
- [ ] Config files written correctly
- [ ] Bot starts and runs
- [ ] Telegram opens to correct bot
- [ ] Bot responds to messages
- [ ] Auto-start works after reboot
- [ ] Donate button works
- [ ] Mac setup works

## Repository Info

- **Repo:** andreycpu/freeclaw
- **Branch:** master
- **Main file:** index.html (everything is in one file)
- **Hosting:** Netlify (auto-deploy from GitHub)

## Contact

- **Owner:** Andrey (@Andrey__HQ on X)
- **Support:** Email or DM links on the website
