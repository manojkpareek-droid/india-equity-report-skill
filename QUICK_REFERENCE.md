# Quick Reference Card

**India Equity Research Report Skill - Cheat Sheet**

---

## 🚀 Quick Start

```bash
# 1. Clone repository
git clone https://github.com/[username]/india-equity-report-skill.git

# 2. Upload to Claude.ai
# Drag and drop the 'india-equity-report' folder into Claude chat

# 3. Test
"Analyze RELIANCE"
```

---

## 💡 Common Queries

| What You Want | What To Type |
|---------------|--------------|
| Full equity report | `Analyze RELIANCE` |
| Quick analysis | `Give me a 1-page summary for HDFCBANK` |
| Compare stocks | `Compare INFY vs TCS - which is better value?` |
| Portfolio review | `Review my holdings: RELIANCE, HDFCBANK, INFY` |
| Event analysis | `Analyze HDFC Bank post-merger impact` |
| Sector view | `Which IT stock should I buy: INFY, TCS, or WIPRO?` |

---

## 📊 Report Structure (20 sections)

1. **Executive Summary** - The "why now" story
2. **Macro Context** - Sector tailwinds/headwinds
3. **Business Model** - How the company makes money
4. **Competitive Moat** - Why competitors can't replicate
5. **Financials** - 5Y P&L, quarterly trends, balance sheet
6. **Shareholding** - Promoter/FII/DII holdings
7. **Valuation** - P/E, EV/EBITDA, DCF models
8. **Technical Analysis** - Charts, indicators, levels
9. **SWOT** - Strengths/Weaknesses/Opportunities/Threats
10. **Risk Matrix** - Ranked by severity
11. **Catalysts** - Upcoming events timeline
12. **Investment Verdict** - Actionable BUY/SELL/HOLD

---

## 🎯 Key Metrics Explained

| Metric | Formula | Good if... |
|--------|---------|------------|
| **ROE** | PAT / Equity | > 15% |
| **ROCE** | EBIT / Capital Employed | > 15% |
| **ROIC** | NOPAT / Invested Capital | > WACC |
| **P/E** | Price / EPS | < 5Y median |
| **EV/EBITDA** | Enterprise Value / EBITDA | < peer median |
| **Debt/Equity** | Total Debt / Equity | < 1.0x |
| **CFO/PAT** | Operating Cash Flow / PAT | > 0.8 |

---

## ⚠️ Critical Warnings

### Never Trust Screener.in CMP
```
❌ Screener shows: ₹356 (13 Feb - STALE)
✅ Skill fetches:  ₹383.50 (27 Feb - LIVE via Google Finance)
```

### Always Check Date Stamps
Every price must have:
- ✅ Concrete ₹ number (e.g., ₹2,850.00)
- ✅ Date stamp (as of 15 Mar 2026)
- ✅ Source (Google Finance / Tickertape)

### Red Flags to Watch
- ⚠️ CFO/PAT < 0.8 (earnings quality issue)
- ⚠️ Receivables growing faster than revenue
- ⚠️ Promoter pledging increasing
- ⚠️ Audit qualifications
- ⚠️ ROIC < WACC (value destruction)

---

## 🔧 Customization Quick Edits

### Change Valuation Assumptions
**File:** `references/analysis-frameworks.md`
```markdown
# Line 285: India ERP
- India ERP benchmark: 5.5% (instead of 6.0%)

# Line 312: Terminal Growth
- Terminal growth: 4-5% (instead of 5-6%)
```

### Modify Report Template
**File:** `references/report-template.md`
```markdown
# Add your branding:
[YOUR FIRM NAME]
Research Division
[Your Name], CFA | [email]
```

### Add New Data Source
**File:** `references/data-sources.md`
```markdown
| New Source Name | URL | Data Type | Priority |
|---|---|---|---|
| [Source] | [URL] | [What it provides] | Primary/Fallback |
```

---

## 📱 Mobile Usage

**Via Claude Mobile App:**
1. Open app → New conversation
2. Type: `Analyze [TICKER]`
3. Download DOCX from chat
4. Open in Word/Google Docs app

---

## 🐛 Troubleshooting

| Problem | Quick Fix |
|---------|-----------|
| Skill doesn't trigger | Be explicit: `Use india-equity-report skill to analyze RELIANCE` |
| "Data unavailable" | Wait 1-2 days if results just announced |
| Valuation seems off | Check if EPS is TTM vs Forward |
| Report won't download | Regenerate: `Recreate the RELIANCE report` |
| Price looks wrong | Report is correct - Screener.in likely stale |

---

## 📚 Learning Path

### Beginner (Week 1)
1. Read [WALKTHROUGH.md](WALKTHROUGH.md)
2. Generate 3 reports (large-cap stocks you know)
3. Focus on "Investment Verdict" section

### Intermediate (Week 2-3)
4. Understand valuation models (P/E, EV/EBITDA)
5. Learn to read DuPont analysis
6. Interpret technical indicators

### Advanced (Month 2)
7. Customize report template
8. Build screening workflow
9. Compare your analysis vs skill's output

---

## 💰 Investment Workflow

```
Step 1: Screen on Screener.in
  ↓ (Filter: ROE>15%, Sales growth>15%, Debt/Equity<1)
  
Step 2: Generate reports for top 10
  ↓ (Batch: "Analyze STOCK1, STOCK2, ... STOCK10")
  
Step 3: Filter for BUY ratings
  ↓ (Read Investment Verdict sections)
  
Step 4: Deep dive on 3-5 finalists
  ↓ (Read full reports, check risks)
  
Step 5: Make decision
  ↓ (Buy in tranches as per recommended zones)
  
Step 6: Monitor catalysts
  ↓ (Event Calendar → Set reminders)
```

---

## 🎓 Free Resources

**Learn Fundamentals:**
- NSE Academy: "Basics of Stock Market"
- Varsity by Zerodha (free modules)
- SEBI Investor Education portal

**Practice Valuation:**
- Read annual reports on BSE website
- Follow earnings calls (Screener.in transcripts)
- Compare valuations across 3-4 stocks

**Technical Analysis:**
- TradingView free charts
- Chartink screeners
- YouTube: "Candlestick patterns"

---

## 📞 Get Help

**Documentation:**
- [README](README.md) - Overview
- [WALKTHROUGH](WALKTHROUGH.md) - Step-by-step
- [FAQ](FAQ.md) - Common questions
- [Examples](examples/) - Sample reports

**Community:**
- [GitHub Discussions](https://github.com/[username]/india-equity-report-skill/discussions)
- [Issues](https://github.com/[username]/india-equity-report-skill/issues)

---

## ⭐ Pro Tips

1. **Always verify CMP** before trading (don't rely on report's fetched price)
2. **Read risks first** before investment verdict
3. **Check date stamps** on all financial data
4. **Use scenario analysis** (Bull/Base/Bear) for position sizing
5. **Set stop-losses** as recommended in technical section
6. **Monitor catalysts** from Event Calendar
7. **Update quarterly** - Regenerate reports after results

---

## 🚨 Disclaimers

```
⚠️ NOT INVESTMENT ADVICE - For informational use only
⚠️ NOT SEBI-REGISTERED - Not official research
⚠️ VERIFY DATA - Cross-check before trading
⚠️ MARKET RISKS - Past performance ≠ future results
```

---

**Print this card** | **Bookmark this page** | **Share with friends**

*Happy Investing! 📈*
