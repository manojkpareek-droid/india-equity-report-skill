# Complete Walkthrough: From Zero to Your First Equity Report

This guide takes you from installation to generating your first professional equity research report in **under 10 minutes**.

---

## 📋 Table of Contents

1. [Installation](#installation)
2. [First Report: Step-by-Step](#first-report)
3. [Understanding the Output](#understanding-output)
4. [Advanced Examples](#advanced-examples)
5. [Customization Guide](#customization)
6. [Troubleshooting](#troubleshooting)

---

## 🚀 Installation

### Step 1: Access Claude Code

1. **Log in to Claude.ai**
   - Go to [claude.ai](https://claude.ai)
   - Sign in with your account

2. **Enable Claude Code (if not already enabled)**
   - Click on your profile (bottom left)
   - Go to "Feature Preview"
   - Toggle on "Create files and execute code"

### Step 2: Download the Skill

**Option A: Using Git (Recommended)**
```bash
git clone https://github.com/[your-username]/india-equity-report-skill.git
cd india-equity-report-skill
```

**Option B: Manual Download**
1. Go to the [GitHub repository](https://github.com/[your-username]/india-equity-report-skill)
2. Click "Code" → "Download ZIP"
3. Extract the ZIP file

### Step 3: Deploy to Claude

**Option A: Direct Upload**
1. In Claude.ai, start a new conversation
2. Type: `/upload-skill`
3. Upload the entire `india-equity-report` folder
4. Claude will automatically install it to `/mnt/skills/user/`

**Option B: Manual Installation**
If you have file system access:
```bash
cp -r india-equity-report /mnt/skills/user/
```

### Step 4: Verify Installation

In Claude, type:
```
List my custom skills
```

You should see `india-equity-report` in the output.

---

## 📊 First Report: Step-by-Step

Let's generate a research report for **Reliance Industries** (a large, liquid NSE stock).

### Step 1: Initiate the Request

In Claude, simply type:
```
Analyze Reliance Industries
```

Or be more explicit:
```
Create an equity research report for RELIANCE (NSE ticker)
```

### Step 2: Watch Claude Work

You'll see Claude execute the following sequence:

```
1. ✅ Reading skill documentation
   [Claude accesses /mnt/skills/user/india-equity-report/SKILL.md]

2. ✅ Identifying stock
   Stock: Reliance Industries Limited
   Ticker: RELIANCE
   Exchange: NSE

3. ✅ Fetching live CMP
   [web_search: "RELIANCE NSE share price March 2026"]
   CMP: ₹2,850.00 (as of 15 Mar 2026)
   52W High: ₹3,024 | 52W Low: ₹2,440

4. ✅ Fetching financials
   [web_fetch: https://www.screener.in/company/RELIANCE/consolidated/]
   Retrieved: 5-year P&L, quarterly data, balance sheet

5. ✅ Fetching latest results
   [web_fetch: https://www.bseindia.com/stock-share-price/...]
   Retrieved: Q3 FY26 results (Jan 2026)

6. ✅ Fetching management commentary
   [web_search: "RELIANCE Q3 FY26 concall transcript"]
   Retrieved: Analyst call highlights

7. ✅ Fetching news
   [web_search: "RELIANCE news 2026"]
   Retrieved: 12 articles (ET Markets, Mint, Business Standard)

8. ✅ Fetching technical data
   [web_search: "RELIANCE technical analysis tradingview"]
   Retrieved: RSI, MACD, support/resistance levels

9. ✅ Running analysis frameworks
   - Financial health scorecard: PASS (14/14 metrics)
   - DuPont decomposition: ROE 9.8% (margin-driven)
   - ROIC vs WACC: 11.2% vs 9.8% = +140 bps spread
   - Forensic checks: 7/8 clean (1 minor flag)
   - TAM sizing: ₹45L Cr addressable market

10. ✅ Generating valuations
    - P/E re-rating: ₹3,150 (25x FY27E EPS ₹126)
    - EV/EBITDA: ₹3,180 (12x FY27E EBITDA)
    - DCF: ₹3,050 (10.2% WACC, 5.5% terminal growth)
    - Blended: ₹3,100-₹3,200

11. ✅ Quality check
    ✓ CMP is real number (₹2,850)
    ✓ All figures sourced
    ✓ No formulas in report
    ✓ All template sections present
    ✓ Scenario analysis included
    ✓ SEBI disclaimer added

12. ✅ Creating DOCX report
    [Using /mnt/skills/public/docx/SKILL.md]
    File: RELIANCE_Equity_Report_15Mar2026.docx
    Size: 3,245 words

13. ✅ Presenting report
    [present_files tool called]
```

**Total time: 3-5 minutes**

### Step 3: Review the Output

Claude will present:

1. **Downloadable DOCX file**
   - Click the file link to download
   - Opens in Microsoft Word or Google Docs

2. **Markdown summary in chat**
   ```
   RELIANCE INDUSTRIES - EQUITY RESEARCH REPORT
   
   VERDICT: BUY (Existing) / BUY ON DIPS (New Investors)
   Target: ₹3,100-₹3,200 (12M Base) | ₹3,500+ (Bull)
   
   Key Highlights:
   • Strong Q3 FY26 - Revenue ₹2.4L Cr (+8% YoY)
   • Jio ARPU expansion continuing (₹195 → ₹204)
   • Retail SSG 12% - omnichannel gaining traction
   • Petrochemicals margin compression (-150 bps)
   
   Investment Thesis:
   [3-4 paragraph summary]
   
   Top Risks:
   1. O2C margin volatility
   2. Retail competition intensity
   3. Jio 5G monetization timeline
   
   [Full report in attached DOCX]
   ```

### Step 4: Explore the Full Report

Open the DOCX file. You'll find:

```
TABLE OF CONTENTS
1. Executive Summary (p. 2)
2. The Macroeconomic Paradigm (p. 4)
3. Operational Architecture (p. 6)
4. Competitive Moat (p. 9)
5. Financials (p. 11)
   5A. Management Quality (p. 18)
   5B. DuPont Analysis (p. 20)
   5C. ROIC vs WACC (p. 21)
   5D. Forensic Accounting (p. 22)
6. Shareholding & Institutional Flows (p. 24)
7. Valuation (p. 26)
8. Technical Analysis (p. 30)
9. SWOT Analysis (p. 32)
10. Risk Matrix (p. 34)
11. Event Calendar (p. 36)
12. Investment Verdict (p. 38)
13. Disclaimer (p. 40)
```

---

## 📖 Understanding the Output

### Key Sections Explained

#### 1. Executive Summary
**What it is:** The "TL;DR" of the entire report
**What to look for:**
- Opening insight (the "hook" - why this stock matters NOW)
- Financial proof (key metrics that validate the story)
- Price action context (recent moves explained)
- Report roadmap

**Example:**
```
Jio's ARPU inflection is no longer a "when" question — it's a "how fast" 
story. At ₹204/month (Q3 FY26), Jio has crossed a critical psychological 
threshold (₹200+) that historically marks sustained pricing power. With 
440M subscribers, every ₹10 ARPU gain translates to ~₹5,280 Cr annual 
revenue uplift — and Jio's still 35% below Airtel's ₹314 ARPU, leaving 
runway for multi-year expansion...
```

#### 2. Price Snapshot Box
**What it is:** Real-time price verification
**Critical to check:**
- Date stamp (must be recent)
- Source citation (Google Finance / Tickertape)
- Not from Screener.in (stale cache warning)

**Example:**
```
📊 PRICE SNAPSHOT (as of 15 Mar 2026)
  CMP:         ₹2,850.00
  Prev. Close: ₹2,845.50
  52W High:    ₹3,024.00
  52W Low:     ₹2,440.00
  Market Cap:  ₹19.2L Cr
  Source:      Google Finance (NSE)
```

#### 3. TAM & Market Sizing
**What it is:** Growth runway quantification
**How to read:**
- Total market size (₹ Crore)
- Company's current market share (%)
- Achievable market share in 5Y
- Implied revenue potential

**Example:**
```
India Retail TAM: ₹65,00,000 Cr (FY25) growing at 11% CAGR
Reliance Retail revenue (FY25): ₹3,00,000 Cr
Current market share: 4.6%
At 7% long-term share → ₹4,55,000 Cr revenue potential (1.5x current)
```

**Interpretation:** Even reaching 7% share (vs current 4.6%) gives 50% revenue upside.

#### 4. Financial Tables
**What to look for:**

**Revenue Growth:**
- 3-year CAGR above industry
- Consistent QoQ growth
- No sudden spikes (one-time orders?)

**Margins:**
- OPM trend (expanding = pricing power)
- Net margin vs peers
- Any margin compression (input cost pressure?)

**Returns Ratios:**
- ROE > 15% (good)
- ROCE > 15% (capital efficient)
- ROE vs ROCE spread (high debt if ROE >> ROCE)

**Example Red Flag:**
```
| Quarter   | Sales (₹ Cr) | Net Profit | OPM % |
|-----------|--------------|------------|-------|
| Q1 FY25   | 45,200       | 3,620      | 18.2% |
| Q2 FY25   | 48,100       | 3,890      | 17.8% |  ⚠️ Margin dip
| Q3 FY25   | 52,300       | 3,950      | 16.9% |  🚨 Sustained decline
```

#### 5. Valuation Section
**The most important part for investment decision**

**Target Price Derivation:**
```
Method 1 - P/E Re-rating (50% weight)
  FY27E EPS: ₹126 [Source: Management guidance, Q3 concall]
  Target P/E: 25x (5-year median: 24.5x)
  Implied Price: ₹3,150

Method 2 - EV/EBITDA (30% weight)
  FY27E EBITDA: ₹1,45,000 Cr
  Target EV/EBITDA: 12x (peer median)
  Less: Net Debt ₹1,20,000 Cr
  Implied Price: ₹3,180

Method 3 - DCF (20% weight)
  WACC: 10.2%, Terminal growth: 5.5%
  Implied Price: ₹3,050

Blended Target: ₹3,100-₹3,200 (12M)
Upside from CMP (₹2,850): 9-12%
```

**Sensitivity Table:**
```
What if EPS or P/E is different?

         P/E: 22x  | P/E: 25x | P/E: 28x
EPS ₹120  ₹2,640  | ₹3,000   | ₹3,360
EPS ₹126  ₹2,772  | ₹3,150 ★ | ₹3,528
EPS ₹132  ₹2,904  | ₹3,300   | ₹3,696
```
★ = Base case

**How to use:** If you believe EPS will be ₹132 instead of ₹126, your target shifts to ₹3,300.

#### 6. Investment Verdict
**The actionable takeaway**

**For Existing Holders:**
```
HOLD / ADD ON DIPS
• Continue holding - fundamentals intact
• Accumulate on dips below ₹2,750 (200-DMA support)
• Stop-loss: ₹2,600 (material support breach)
• Key monitor: Q4 FY26 Jio ARPU trend (target ₹210+)
• Hold through AGM (Jun 2026) - potential bonus announcement
```

**For New Investors:**
```
BUY ON DIPS (NOT AT CMP)
• CMP ₹2,850 offers limited margin of safety (only 9% upside)
• Target accumulation: ₹2,700-₹2,800 (14-18% upside)
• Tranche strategy: 40% at ₹2,800 | 30% at ₹2,750 | 30% at ₹2,700
• Hard stop-loss: ₹2,600 (invalidates bull thesis)
• Minimum horizon: 12-18 months (re-rating is a process, not event)
```

---

## 🎯 Advanced Examples

### Example 1: Mid-Cap Stock with Limited Coverage

**Query:**
```
Research LatentView Analytics (LATENTVIEW)
```

**Skill handles:**
- Limited analyst coverage (fewer sources)
- Smaller market cap (different valuation norms)
- Detected Screener.in stale price issue (₹356 shown vs ₹383 actual)
- Auto-corrected by fetching via Google Finance
- Adjusted P/E benchmarks (mid-cap vs large-cap)

**Output highlight:**
```
⚠️ PRICE VERIFICATION ALERT
Screener.in displayed: ₹356.00 (13 Feb close - STALE)
Actual CMP (Google Finance): ₹383.50 (27 Feb close)
Discrepancy: 7.7% (₹27.50)

This report uses ₹383.50 as the verified CMP.
```

### Example 2: SME Stock (BSE-Listed)

**Query:**
```
Analyze Macfos Ltd (BSE: 543787) - the parent of Robu.in
```

**Skill handles:**
- BSE-only listing (no NSE ticker)
- Prefix handling (`BSE:MACFOS`)
- Illiquid stock (wider bid-ask)
- Limited institutional data
- Practitioner's edge: User mentioned procurement experience with Robu.in

**Output highlight:**
```
> PRACTITIONER'S EDGE — Channel Check Validation
As a direct procurement customer of Robu.in for drone components, 
the user reports AOV growth from ₹8K (FY23) to ₹14K (FY25) and 
48-hour delivery consistency. This field data corroborates the 
company's claim of B2B consolidation capturing share from 
fragmented suppliers.
```

### Example 3: Event-Driven Analysis

**Query:**
```
Analyze HDFC Bank post-merger with HDFC Ltd. 
Focus on NIM compression risk and deposit franchise quality.
```

**Skill handles:**
- Incorporates corporate action context
- Focuses analysis on user-specified risks
- Pro-forma financials (merged entity)
- Regulatory capital impact

**Output highlight:**
```
POST-MERGER IMPACT ANALYSIS

Pre-merger (HDFC Bank standalone):
  NIM: 4.2% | CASA: 41% | Advances/Deposits: 88%

Post-merger (Combined entity):
  NIM: 3.4% (-80 bps) ⚠️
  CASA: 46% (+500 bps) ✅
  Advances/Deposits: 102% (elevated)

The NIM compression is mechanical (HDFC Ltd's mortgage book 
carries lower yields). However, the CASA accretion MORE than 
offsets this via cheaper funding...
```

### Example 4: Sector Comparison

**Query:**
```
Compare the top 3 IT services stocks: INFY, TCS, WIPRO
Which offers the best risk-reward at current prices?
```

**Output:**
```
COMPARATIVE VALUATION TABLE

           CMP    P/E   ROE   ROCE  Rev CAGR  Target  Upside
TCS        ₹3,680  28.5x  44.2%  48.1%  12.4%   ₹3,850   4.6%
Infosys    ₹1,520  24.2x  31.8%  36.5%  14.2%   ₹1,750  15.1%  ★
Wipro      ₹445   18.5x  16.2%  22.1%   8.9%   ₹480    7.9%

VERDICT: Infosys offers the best risk-reward
• Trading at 15% discount to TCS on P/E despite superior growth
• ROE gap narrowing (was 1,200 bps, now 800 bps)
• Digital revenue mix 62% vs TCS 58%
• Re-rating catalyst: FY27 margin guidance (target 21-22%)
```

---

## 🔧 Customization Guide

### Customizing Report Style

**Edit:** `references/report-template.md`

**Example: Add Your Firm's Branding**

```markdown
## COVER BLOCK (Header)

```
[COMPANY NAME] ([TICKER])
EQUITY RESEARCH REPORT · [Month Year]

[YOUR FIRM NAME]
Research Division
[Your Name], CFA | [email] | [phone]

Prepared for: [Client Name] (if applicable)
```
```

**Example: Modify Investment Ratings**

Default scale:
```
BUY > 15% upside
ADD: 8-15%
HOLD: 0-8%
REDUCE: -5 to 0%
SELL < -5%
```

To change to 3-tier system, edit in `references/analysis-frameworks.md`:
```markdown
| Rating | Condition |
|---|---|
| **BUY** | Expected total return > 10% |
| **HOLD** | Expected return -10% to +10% |
| **SELL** | Expected return < -10% |
```

### Customizing Valuation Parameters

**Edit:** `references/analysis-frameworks.md` → Section A5

**Example: Change India ERP Assumption**

```markdown
# Default
- India ERP benchmark: 5.5–6.5% (use 6% as default)

# Your custom
- India ERP benchmark: 5.0–6.0% (use 5.5% as default)
```

**Example: Adjust Terminal Growth Rates**

```markdown
# Default
- Terminal growth: 5–6% (domestic consumption), 4–5% (cyclicals)

# Your custom
- Terminal growth: 4–5% (conservative), 6–7% (aggressive for high-growth)
```

### Adding Custom Analysis Sections

**Edit:** `references/report-template.md`

**Example: Add ESG Scoring Section**

Insert after Section 5C (ROIC vs WACC):

```markdown
---

## 5D. ESG SCORECARD

*Environmental, Social, Governance ratings from CRISIL/MSCI/Sustainalytics*

| Parameter | Score | Industry Avg | Rating |
|---|---|---|---|
| Environmental (E) | [X]/100 | [Y] | ✅ / ⚠️ / ❌ |
| Social (S) | [X]/100 | [Y] | |
| Governance (G) | [X]/100 | [Y] | |
| **Overall ESG** | **[X]/100** | **[Y]** | |

[2 paragraphs: ESG performance analysis, material issues, peer comparison]

Source: [CRISIL ESG / MSCI / Sustainalytics, Date]

---
```

Then update `SKILL.md` to instruct Claude to fetch ESG data:
```markdown
| ESG scores | `web_search: \"[COMPANY] ESG rating CRISIL MSCI 2025\"` | — |
```

---

## 🐛 Troubleshooting

### Issue 1: Skill Doesn't Trigger

**Symptom:** You ask "Analyze RELIANCE" but Claude responds conversationally without using the skill.

**Diagnosis:**
```
Skill not in Claude's context OR description too narrow
```

**Fix:**
1. Verify installation:
   ```
   List my custom skills
   ```
   If not listed → re-upload skill folder

2. Check skill description in `SKILL.md` frontmatter:
   ```yaml
   description: Generate a detailed Buy/Sell/Hold equity research 
   report for Indian stock market (NSE/BSE listed companies). Use 
   this skill whenever the user asks for a stock analysis...
   ```
   Make sure it includes trigger phrases you're using.

3. Be more explicit:
   ```
   Create a full equity research report for RELIANCE using the 
   india-equity-report skill
   ```

### Issue 2: "CMP Unavailable" Error

**Symptom:**
```
⚠️ Could not fetch current market price for [TICKER]
Using last available closing price: ₹[X] (dated [OLD DATE])
```

**Diagnosis:**
- Stock ticker misspelled
- Stock delisted or suspended
- Network/API issue

**Fix:**
1. Verify ticker on NSE website: https://www.nseindia.com
2. Try explicit exchange prefix:
   ```
   Analyze NSE:RELIANCE (not just RELIANCE)
   ```
3. For BSE-only stocks:
   ```
   Analyze BSE:MACFOS (BSE ticker: 543787)
   ```
4. If stock is illiquid, manually provide CMP:
   ```
   Analyze MACFOS. The current market price is ₹999 as of today.
   ```

### Issue 3: "Data Unavailable" for Recent Quarter

**Symptom:**
```
Q3 FY26 results: Data unavailable at time of report
```

**Diagnosis:**
- Results not announced yet
- Results announced but not updated on Screener.in
- Screener.in lag (can be 1-2 days)

**Fix:**
1. Check BSE directly:
   ```
   https://www.bseindia.com/stock-share-price/[company]/[ticker]/[code]/
   ```
2. Provide Claude with the BSE results URL:
   ```
   Analyze RELIANCE. Latest Q3 results are at: 
   [BSE results PDF URL]
   ```
3. Or paste key numbers:
   ```
   Analyze RELIANCE. Q3 FY26 results (just announced):
   Revenue ₹2.4L Cr, Net Profit ₹18,500 Cr
   ```

### Issue 4: Report Shows Formula Instead of Price

**Symptom:**
```
CMP: =GOOGLEFINANCE("NSE:RELIANCE","price")
```

**This should NEVER happen** (quality check should prevent it).

**If it does:**
1. **Immediate fix:** Tell Claude:
   ```
   The CMP shows a formula instead of a number. Fix it.
   ```

2. **Root cause:** Quality check step was skipped. Check if SKILL.md Section 5 is intact:
   ```markdown
   ### Step 5 — Quality Check (MANDATORY before publishing)
   - [ ] CMP is a real ₹ number (e.g., ₹183.50) — not a formula
   ```

3. **Verify fix:** Re-generated report should show:
   ```
   CMP: ₹2,850.00 [Source: Google Finance, 15 Mar 2026]
   ```

### Issue 5: Valuation Seems Unrealistic

**Symptom:**
```
Target Price: ₹15,000 (Current: ₹500)
→ 2,900% upside!
```

**Diagnosis:**
- Wrong EPS used (₹50 instead of ₹5.0)
- P/E multiple error (500x instead of 50x)
- Decimal place mistake

**Fix:**
1. Check the valuation section's underlying data:
   ```
   FY27E EPS: ₹[X] [Source: ...]
   Target P/E: [Y]x
   ```
2. Manually verify EPS on Screener.in
3. Tell Claude:
   ```
   The target price seems wrong. The TTM EPS is ₹5.20, not ₹52. 
   Recalculate the target using P/E of 25x.
   ```

### Issue 6: Report is Too Short/Long

**Default:** 1,500-3,000 words

**To shorten:**
```
Create a concise equity report for RELIANCE (max 1,500 words)
Focus on: Valuation, Risks, Investment Verdict
```

**To expand:**
```
Create a comprehensive deep-dive equity report for RELIANCE 
(4,000+ words). Include detailed segment analysis, 10-year 
financial history, and extensive management commentary.
```

---

## 💡 Pro Tips

### Tip 1: Batch Processing
```
Generate equity reports for my portfolio:
1. RELIANCE
2. HDFCBANK
3. INFY
4. ITC
5. TCS

Create all 5 reports in a single ZIP file.
```

Claude will sequentially generate all 5, then bundle them.

### Tip 2: Custom Focus Areas
```
Analyze TATAMOTORS focusing specifically on:
- JLR turnaround progress
- EV transition roadmap
- Debt reduction trajectory
- Tata.ev competitive position vs Mahindra
```

The skill adapts to emphasize these areas in the analysis.

### Tip 3: Comparative Shortcuts
```
Quick comparison:
HDFCBANK vs ICICIBANK vs KOTAKBANK

Just give me a 1-page summary table with:
P/E, P/B, ROE, ROCE, NIM, GNPA, Target, Verdict
```

Gets you a decision matrix without full reports.

### Tip 4: Update Existing Reports
```
I have an old equity report for RELIANCE from Dec 2025.
Update it with Q3 FY26 results and revised target price.
```

Claude will fetch new data and update only changed sections.

### Tip 5: Sector Rotation
```
Which sector should I rotate into?
Compare: IT (INFY, TCS) vs BFSI (HDFCBANK, ICICIBANK) 
vs Auto (TATAMOTORS, M&M)

Give me the sector with best forward 12M risk-reward.
```

Gets you strategic allocation guidance.

---

## 🎓 Learning Resources

### Understanding Financial Metrics

**ROE vs ROCE:**
- **ROE** = Return on Equity = PAT / Shareholder Equity
  - Measures return to shareholders
  - Can be inflated by high debt
  
- **ROCE** = Return on Capital Employed = EBIT / (Equity + Debt)
  - Measures return on all capital (debt + equity)
  - Better gauge of operating efficiency

**Rule:** If ROE >> ROCE, company is leveraged (check Debt/Equity ratio).

**Example:**
```
Company A: ROE 25%, ROCE 12% → High leverage (risky)
Company B: ROE 18%, ROCE 16% → Low leverage (safer)
```

**DuPont Formula:**
```
ROE = Net Margin × Asset Turnover × Equity Multiplier

Example:
ROE 20% = 5% margin × 2x turnover × 2x leverage

This tells you WHY ROE is high:
- High margin → pricing power (sustainable)
- High turnover → asset efficiency (good)
- High leverage → debt (risky)
```

**ROIC vs WACC:**
```
ROIC = Return on Invested Capital (what you earn)
WACC = Weighted Average Cost of Capital (what you pay)

If ROIC > WACC → Value creation ✅
If ROIC < WACC → Value destruction ❌

Example:
ROIC 15%, WACC 10% → 5% spread → Every ₹100 invested creates ₹5
```

### Interpreting Valuation Multiples

**P/E Ratio:**
```
P/E = Price per Share / Earnings per Share

Low P/E (< 15): Value stock or dying business?
High P/E (> 30): Growth stock or overvalued?

Compare to:
- Stock's own 5-year average
- Sector median
- Growth rate (PEG ratio)
```

**PEG Ratio:**
```
PEG = P/E / EPS Growth Rate

PEG < 1 → Undervalued relative to growth
PEG > 2 → Overvalued / growth priced in

Example:
Stock A: P/E 30, Growth 25% → PEG 1.2 (fair)
Stock B: P/E 30, Growth 10% → PEG 3.0 (expensive)
```

### Further Reading

1. **"The Intelligent Investor" - Benjamin Graham**
   - Chapter 14: Stock Selection for Defensive Investor
   - Chapter 20: Margin of Safety

2. **"One Up On Wall Street" - Peter Lynch**
   - PEG ratio methodology
   - Identifying multi-baggers

3. **SEBI Guidelines**
   - Research Analyst Regulations, 2014
   - Insider Trading Regulations

4. **Free Courses**
   - NSE Academy: Basics of Stock Market
   - BSE Institute: Equity Research Analyst

---

## 🚀 Next Steps

Now that you've completed the walkthrough:

1. **Generate 3-5 reports** for stocks you're familiar with
2. **Compare** your own analysis with the skill's output
3. **Customize** the template to your preferences
4. **Share** feedback via GitHub Issues
5. **Contribute** improvements back to the community

---

**Happy Investing! 📈**

*Remember: This skill is a tool, not a substitute for your judgment. Always do your own due diligence.*
