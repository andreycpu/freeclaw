# Security

## How FreeClaw handles your data

- **Zero storage:** Your API keys and bot tokens are never stored, transmitted, or logged by FreeClaw
- **Client-side only:** All script generation happens in your browser using JavaScript. No server-side processing
- **No network requests:** The FreeClaw website makes zero requests with your data. Only Google Fonts CSS is loaded externally
- **Direct downloads:** Generated scripts download Node.js and Git directly from official sources (nodejs.org, github.com) over HTTPS
- **Input sanitization:** All user inputs are sanitized before being embedded in generated scripts to prevent injection

## What the generated script does

The setup script that you download contains your API keys embedded as text. It:

1. Downloads Node.js from nodejs.org (HTTPS)
2. Downloads Git from github.com (Windows only, HTTPS)
3. Installs OpenClaw via npm
4. Writes your configuration to ~/.openclaw/
5. Starts the OpenClaw gateway

The script makes no callbacks to FreeClaw servers.

## Reporting vulnerabilities

If you find a security issue, please open a GitHub issue or contact the maintainer directly.
