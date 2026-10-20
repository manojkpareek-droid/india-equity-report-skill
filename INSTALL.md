# Installation Guide

## Quick Install (Recommended)

### For Claude.ai Users

1. **Download the skill package**
   ```bash
   git clone https://github.com/[your-username]/india-equity-report-skill.git
   ```

2. **Upload to Claude**
   - Open Claude.ai
   - Start a new conversation
   - Drag and drop the entire `india-equity-report` folder into the chat
   - Claude will automatically install it

3. **Verify**
   ```
   Test message: "Analyze RELIANCE"
   ```
   The skill should trigger automatically.

---

## Manual Installation

### Prerequisites
- Claude.ai account with file upload enabled
- OR local access to Claude Code installation directory

### Step 1: Download Files

**Option A: Git Clone**
```bash
git clone https://github.com/[your-username]/india-equity-report-skill.git
cd india-equity-report-skill
```

**Option B: Download ZIP**
1. Go to https://github.com/[your-username]/india-equity-report-skill
2. Click "Code" → "Download ZIP"
3. Extract to a local directory

### Step 2: Locate Skills Directory

**For Claude.ai:**
Skills are managed in `/mnt/skills/user/` (virtual filesystem)

**For Claude Code (local):**
```bash
# macOS/Linux
~/Library/Application Support/Claude/skills/user/

# Windows
%APPDATA%\Claude\skills\user\
```

### Step 3: Copy Skill Files

**Method 1: Via Claude (Recommended)**
1. Open Claude.ai
2. Type: "I want to add a custom skill"
3. Upload the `india-equity-report` folder
4. Claude handles the rest

**Method 2: Manual Copy**
```bash
cp -r india-equity-report /path/to/skills/user/
```

### Step 4: Verify Installation

**Check if skill is loaded:**
```
In Claude: "List my custom skills"
```

Expected output:
```
Your custom skills:
1. india-equity-report - Generate detailed Buy/Sell/Hold equity 
   research reports for NSE/BSE stocks
2. [other skills...]
```

**Test the skill:**
```
Create an equity report for RELIANCE
```

You should see Claude:
1. Read `/mnt/skills/user/india-equity-report/SKILL.md`
2. Fetch live data
3. Generate a comprehensive report

---

## Troubleshooting Installation

### Issue: Skill Not Found

**Symptom:**
```
Claude: "I don't have an india-equity-report skill"
```

**Fix:**
1. Verify folder structure:
   ```
   india-equity-report/
   ├── SKILL.md (with YAML frontmatter)
   ├── references/
   │   ├── analysis-frameworks.md
   │   ├── data-sources.md
   │   └── report-template.md
   ```

2. Check YAML frontmatter in SKILL.md:
   ```yaml
   ---
   name: india-equity-report
   description: Generate a detailed Buy/Sell/Hold...
   ---
   ```
   
   Must have `---` delimiters above and below.

3. Re-upload the folder.

### Issue: Skill Triggers on Wrong Queries

**Symptom:**
Skill activates when you ask about US stocks or unrelated topics.

**Fix:**
Edit `SKILL.md` frontmatter to narrow description:
```yaml
description: Generate a detailed Buy/Sell/Hold equity research 
report for INDIAN stock market (NSE/BSE listed companies ONLY). 
Use this skill ONLY when the user asks about Indian stocks...
```

### Issue: Permission Errors

**Symptom:**
```
Error: Cannot write to /mnt/skills/user/
```

**Fix:**
This shouldn't happen in Claude.ai. If using local Claude Code:
```bash
# Check permissions
ls -la ~/Library/Application\ Support/Claude/skills/

# Fix permissions
chmod -R 755 ~/Library/Application\ Support/Claude/skills/user/
```

### Issue: Skill Loads But Doesn't Execute

**Symptom:**
Claude acknowledges the skill but doesn't use it.

**Fix:**
1. Check if skill file is readable:
   ```
   In Claude: "View /mnt/skills/user/india-equity-report/SKILL.md"
   ```

2. If file displays correctly, the issue is trigger matching. 
   Be more explicit:
   ```
   Use the india-equity-report skill to analyze RELIANCE
   ```

---

## Updating the Skill

### Pull Latest Version

**If installed via Git:**
```bash
cd india-equity-report-skill
git pull origin main
```

**If downloaded as ZIP:**
Download latest ZIP and replace the folder.

### Re-upload to Claude

1. Remove old version:
   ```
   In Claude: "Remove the india-equity-report skill"
   ```

2. Upload new version:
   Drag and drop the updated folder.

---

## Uninstallation

### Via Claude.ai

```
Remove the india-equity-report skill
```

### Manual Removal

```bash
# macOS/Linux
rm -rf ~/Library/Application\ Support/Claude/skills/user/india-equity-report/

# Windows
rd /s /q %APPDATA%\Claude\skills\user\india-equity-report\
```

---

## Advanced Configuration

### Custom Skill Location

To install in a different location (e.g., for organization-wide deployment):

1. Edit Claude's config file (location varies by OS)
2. Add custom skills path:
   ```json
   {
     "skills": {
       "paths": [
         "/custom/path/to/skills",
         "/mnt/skills/user"
       ]
     }
   }
   ```

### Environment Variables

For programmatic access or CI/CD:

```bash
export CLAUDE_SKILLS_PATH="/opt/claude-skills"
export CLAUDE_SKILL_AUTO_UPDATE=true
```

---

## System Requirements

### Minimum
- Claude.ai account (free tier works)
- Internet connection for data fetching
- Modern browser (Chrome, Firefox, Safari, Edge)

### Recommended
- Claude Pro (faster responses, longer context)
- Stable internet (15+ Mbps for quick data fetches)
- 2GB+ free disk space (for storing generated reports)

### Network Access
Skill fetches data from:
- screener.in
- bseindia.com
- nseindia.com
- google.com (for Finance data)
- tickertape.in
- trendlyne.com

Ensure firewall/proxy allows these domains.

---

## Support

If installation issues persist:

1. **Check documentation**: [README.md](README.md)
2. **Search issues**: [GitHub Issues](https://github.com/[username]/india-equity-report-skill/issues)
3. **Ask for help**: [GitHub Discussions](https://github.com/[username]/india-equity-report-skill/discussions)
4. **Report bug**: [New Issue](https://github.com/[username]/india-equity-report-skill/issues/new)

---

**Installation complete! 🎉**

Next step: [Complete the Walkthrough](WALKTHROUGH.md) to generate your first report.
