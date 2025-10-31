# Google OAuth Setup for Righter

## Status: Ready to Configure

The Google Workspace MCP server is installed and configured. You just need to add your OAuth credentials.

## Why This Solution Works

We're using **taylorwilsdon/google_workspace_mcp** instead of a-bonus/google-docs-mcp because:
- Uses **Desktop OAuth** (no redirect URI issues!)
- Modern OAuth flow (not the deprecated OOB flow)
- Production-ready with comprehensive Google Docs support
- Includes Drive, Gmail, Calendar, Sheets, Slides as bonuses

## Step 1: Create Google Cloud OAuth Credentials

1. **Go to Google Cloud Console**: https://console.cloud.google.com/

2. **Create or Select a Project**:
   - Click the project dropdown at the top
   - Click "New Project" or select existing
   - Name it something like "Righter MCP"

3. **Enable Required APIs**:
   - Go to "APIs & Services" → "Library"
   - Search for and enable these APIs:
     - Google Docs API
     - Google Drive API
     - (Optional: Gmail, Calendar, Sheets, Slides if you want those features)

   Quick links:
   - Docs: https://console.cloud.google.com/apis/library/docs.googleapis.com
   - Drive: https://console.cloud.google.com/apis/library/drive.googleapis.com

4. **Create OAuth Credentials**:
   - Go to "APIs & Services" → "Credentials"
   - Click "Create Credentials" → "OAuth Client ID"
   - If prompted, configure the OAuth consent screen:
     - Choose "External" (unless you have a Google Workspace account)
     - Fill in app name: "Righter MCP"
     - Add your email as developer contact
     - Skip scopes (we'll add them later)
     - Add your email as test user
   - Back to Create Credentials → OAuth Client ID
   - Application type: **Desktop Application** (this is key!)
   - Name: "Righter Desktop Client"
   - Click "Create"

5. **Save Your Credentials**:
   - You'll see a popup with Client ID and Client Secret
   - Copy both values (you'll need them in the next step)

## Step 2: Add Credentials to Righter Configuration

Copy the template and add your credentials:

```bash
cp .mcp.json.template .mcp.json
```

Then edit `/Users/ben/Work/righter/.mcp.json` and replace the placeholders:

```json
{
  "mcpServers": {
    "google-workspace": {
      "command": "uv",
      "args": [
        "--directory",
        "${HOME}/mcp-servers/google-workspace",
        "run",
        "main.py"
      ],
      "env": {
        "GOOGLE_OAUTH_CLIENT_ID": "YOUR_ACTUAL_CLIENT_ID.apps.googleusercontent.com",
        "GOOGLE_OAUTH_CLIENT_SECRET": "YOUR_ACTUAL_CLIENT_SECRET",
        "OAUTHLIB_INSECURE_TRANSPORT": "1"
      },
      "description": "Google Workspace integration with Desktop OAuth - supports Docs, Drive, Gmail, Calendar, Sheets, Slides"
    }
  }
}
```

**Note:** `.mcp.json` is gitignored to protect your credentials.

## Step 3: Test the Integration

After adding your credentials, restart Claude Code and try:

```bash
/refine https://docs.google.com/document/d/YOUR_DOC_ID/edit
```

**First time authentication flow:**
1. The MCP server will output an authorization URL
2. Open it in your browser
3. Sign in with your Google account
4. Click "Allow" to grant permissions
5. Google will show an authorization code
6. Copy and paste the code back
7. Authentication is saved for future sessions!

## What You Can Do

Once authenticated, the `/refine` command will:
- Read the Google Doc content via MCP
- Run all 6 editing agents (tone, authenticity, clarity, structure, ben-voice)
- Create revision tabs in the Google Doc:
  - Original (Tab 1) - stays safe
  - Revision 1 (Tab 2) - first iteration
  - Revision 2 (Tab 3) - second iteration (if conflicts found)
  - Etc.
- Let you review in Google Docs browser
- Keep iterating until no conflicts remain

## Files Changed

- `/Users/ben/Work/righter/.mcp.json` - Updated MCP configuration
- `~/mcp-servers/google-workspace/` - Installed MCP server

## Troubleshooting

**"Access blocked: This app's request is invalid"**
- Make sure you selected "Desktop Application" (not "Web Application")
- Double-check the Client ID and Secret are correct

**"The out-of-band (OOB) flow has been blocked"**
- This shouldn't happen with Desktop OAuth, but if it does:
  - Verify you're using the taylorwilsdon server (not a-bonus)
  - Check that your credentials are for "Desktop Application"

**"Credentials not found"**
- Make sure you edited `.mcp.json` with your actual credentials
- Restart Claude Code after editing the config

**MCP server not starting**
- Check that uv is installed: `which uv`
- Verify dependencies: `cd ~/mcp-servers/google-workspace && uv sync`
- Test manually: `cd ~/mcp-servers/google-workspace && uv run main.py`

## Security Notes

- `OAUTHLIB_INSECURE_TRANSPORT=1` allows http://localhost for development
- Your credentials are stored locally in `~/.google_workspace_mcp/credentials/`
- Never commit `.mcp.json` with real credentials to version control
- The `.mcp.json` file is ignored by git (it's in .gitignore by default for Claude Code projects)

## Next Steps

After this works:
1. Test with a simple Google Doc
2. Try the full `/refine` workflow
3. Test the revision tabs feature
4. Enjoy your multi-agent writing system!

## Links

- Google Cloud Console: https://console.cloud.google.com/
- MCP Server Repo: https://github.com/taylorwilsdon/google_workspace_mcp
- FastMCP Docs: https://gofastmcp.com/
