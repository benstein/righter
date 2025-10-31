# Google Docs MCP Server Setup

This directory is configured to use the `@a-bonus/google-docs-mcp` server for Google Docs integration.

## Prerequisites

- Node.js 18+ installed
- Google account
- Access to Google Cloud Console

## Setup Steps

### 1. Install the MCP Server

```bash
# Clone the repository
git clone https://github.com/a-bonus/google-docs-mcp.git ~/mcp-servers/google-docs
cd ~/mcp-servers/google-docs

# Install dependencies
npm install

# Build the TypeScript code
npm run build
```

This installs it to `~/mcp-servers/google-docs/` (you can choose a different location if preferred).

### 2. Create Google Cloud Project & Enable APIs

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or use existing)
3. Enable these APIs:
   - Google Docs API
   - Google Drive API

**To enable APIs:**
- Go to "APIs & Services" > "Library"
- Search for "Google Docs API" → Enable
- Search for "Google Drive API" → Enable

### 3. Create OAuth 2.0 Credentials

1. In Google Cloud Console, go to "APIs & Services" > "Credentials"
2. Click "Create Credentials" > "OAuth client ID"
3. Choose application type: **Desktop app**
4. Name it: "Claude Code - Righter"
5. Click "Create"
6. Download the credentials JSON file

### 4. Set Up Credentials in MCP Server Directory

```bash
# Move downloaded credentials file to MCP server directory
mv ~/Downloads/client_secret_*.json ~/mcp-servers/google-docs/credentials.json
```

**Important:** The credentials file must be in the MCP server directory and named exactly `credentials.json`

### 5. First-Time Authorization

Run the server once to complete OAuth flow:

```bash
cd ~/mcp-servers/google-docs
node ./dist/server.js
```

This will:
1. Open a browser for Google authentication
2. Ask you to grant permissions
3. Generate `token.json` in the same directory
4. Exit automatically once complete

### 6. Update MCP Configuration

Update the `.mcp.json` file in this directory to point to your installation:

```json
{
  "mcpServers": {
    "google-docs": {
      "command": "node",
      "args": ["${HOME}/mcp-servers/google-docs/dist/server.js"]
    }
  }
}
```

**Note:** The credentials.json and token.json are automatically read from the MCP server directory.

### 7. Test the Integration

```bash
cd /Users/ben/Work/righter
claude

# Try reading a Google Doc
/refine https://docs.google.com/document/d/YOUR_DOC_ID
```

If authentication is successful, the orchestrator will:
- Read your document
- Ask context questions
- Create revision tabs in the same document
- Return URLs for you to review

## Security Notes

✅ **Credentials stay local**: All authentication files are stored on your machine
✅ **OAuth 2.0**: You control what permissions are granted
✅ **Open source**: The MCP server code is auditable on GitHub
✅ **No third-party access**: Credentials are never sent to anyone but Google

## Troubleshooting

### MCP Server Not Found

```bash
# Verify installation
ls ~/mcp-servers/google-docs/dist/server.js

# If missing, rebuild
cd ~/mcp-servers/google-docs
npm run build
```

### Credentials File Not Found

```bash
# Check file exists
ls ~/mcp-servers/google-docs/credentials.json

# Verify it's valid JSON
cat ~/mcp-servers/google-docs/credentials.json | jq .
```

### Authentication Fails

1. Delete token file: `rm ~/mcp-servers/google-docs/token.json`
2. Run authorization again: `cd ~/mcp-servers/google-docs && node ./dist/server.js`
3. Make sure APIs are enabled in Google Cloud Console
4. Check OAuth consent screen is configured

### Check MCP Status

In Claude Code:
```
/mcp
```

Should show "google-docs" server with status "connected"

## What Gets Created

After setup, you'll have:

```
~/mcp-servers/google-docs/
  ├── dist/server.js      (compiled MCP server)
  ├── credentials.json    (your OAuth client credentials)
  └── token.json          (generated after first auth)

/Users/ben/Work/righter/
  └── .mcp.json           (MCP server configuration pointing to above)
```

## Features Available

Once configured, the orchestrator can:

✅ Read content from Google Docs URLs
✅ List existing tabs in documents
✅ Create new tabs for revisions
✅ Write formatted content to tabs
✅ Preserve original content safely
✅ Allow side-by-side comparison

## Usage

See [HOW_TO_USE.md](HOW_TO_USE.md) for workflow details.

Quick example:
```bash
cd /Users/ben/Work/righter
claude
/refine https://docs.google.com/document/d/ABC123/edit
```

Orchestrator will create revision tabs you can review in Google Docs!

## Support

- MCP Server: https://github.com/a-bonus/google-docs-mcp
- Issues: Check GitHub issues for common problems
- Google OAuth: https://developers.google.com/identity/protocols/oauth2
