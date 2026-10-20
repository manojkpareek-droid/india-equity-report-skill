# Frequently Asked Questions (FAQ)

## General Questions

### What is this skill?
A Claude Code skill that generates institutional-quality equity research reports for Indian stocks (NSE/BSE). It automates the complete workflow from data gathering to valuation modeling to report generation.

### Is it free to use?
Yes, the skill itself is free (MIT License). You just need a Claude.ai account. The free tier works, but Claude Pro is recommended for faster processing.

### How accurate are the reports?
The skill fetches data from authoritative sources (Screener.in, BSE, NSE, Google Finance) and includes source citations for every figure. However, you should always:
- Verify critical data independently
- Cross-check valuations with your own analysis
- Understand this is NOT investment advice

### Can I use this for professional/commercial purposes?
Yes, under MIT License. However:
- ⚠️ **Not SEBI-registered research** - cannot be marketed as such
- ✅ Can be used for personal portfolio management
- ✅ Can be used by RIAs for internal analysis (with proper disclaimers)
- ❌ Cannot be distributed as "official research reports" without SEBI registration

---

## Technical Questions

### Q: Which stocks are supported?

**A:** Any stock listed on NSE or BSE, including:
- Large-cap (Nifty 50, Sensex)
- Mid-cap (Nifty Midcap 150)
- Small-cap (Nifty Smallcap 250)
- SME (BSE SME platform)

**Not supported:**
- Unlisted companies
- Delisted stocks
- Stocks without Screener.in coverage
- International stocks (use for Indian listings only)

### Q: How long does it take to generate a report?

**A:** Typically 3-5 minutes, depending on:
- Stock complexity (multi-segment companies take longer)
- Data availability (recent IPOs have limited history)
- Network speed (data fetching from 6-12 sources)

**Breakdown:**
- Data fetching: 2-3 minutes (60%)
- Analysis: 30-60 seconds (20%)
- Report generation: 1-2 minutes (20%)

### Q: Can I analyze multiple stocks at once?

**A:** Yes, use batch queries:
```
Generate equity reports for: RELIANCE, HDFCBANK, INFY, TCS
```

Claude will process them sequentially. For 4 stocks = ~15-20 minutes total.

### Q: What if data is missing for my stock?

**A:** The skill handles this gracefully:
- **Recent IPOs**: Generates shorter report, flags limited historical data
- **Illiquid stocks**: Uses last available prices, flags wide bid-ask
- **Missing quarterly results**: States "Data unavailable at time of report"
- **No analyst coverage**: Omits consensus targets, focuses on intrinsic valuation

---

## Data & Pricing Questions

### Q: Why does the report show a different price than Screener.in?

**A:** This is intentional and correct behavior.

**Problem:** Screener.in often displays a **stale cached price** with an old date (e.g., "13 Feb close" shown on 27 Feb).

**Solution:** The skill:
1. Ignores Screener.in's CMP field entirely
2. Fetches live price via `web_search: "[TICKER] NSE share price"`
3. Uses Google Finance data (same as GOOGLEFINANCE() in Sheets)
4. Validates the date stamp

**Example:**
```
Screener.in shows: ₹356 (13 Feb - STALE)
Skill reports:      ₹383.50 (27 Feb - CURRENT)
Source:             Google Finance
```

This is a **feature, not a bug**. Always trust the skill's CMP over Screener.in's display.

### Q: How recent is the financial data?

**A:** Depends on the source:
- **Live prices**: Real-time to 15-min delayed
- **Quarterly results**: Updated within 1-2 days of BSE filing
- **Annual reports**: Updated when company publishes
- **Shareholding**: Updated quarterly (45 days post-quarter-end)

**Note:** Screener.in has a 1-2 day lag for quarterly updates. If results were announced today, they might not appear until tomorrow.

### Q: Can I specify a custom price?

**A:** Yes, if needed:
```
Analyze MACFOS. The current market price is ₹999 as of today.
Use this for all valuation calculations.
```

Useful for very illiquid stocks where last traded price is days old.

---

## Valuation Questions

### Q: How are target prices calculated?

**A:** Minimum 2 methods, typically 3:

**1. P/E Re-rating (most common)**
```
Target = Forward EPS × Target P/E multiple
Where:
  Forward EPS = Management guidance / Analyst consensus / Skill estimate
  Target P/E = 5-year median OR peer median (whichever justified)
```

**2. EV/EBITDA**
```
Target = (Target EV - Net Debt) / Shares Outstanding
Where:
  Target EV = Forward EBITDA × Industry multiple
```

**3. DCF (for stable businesses)**
```
3-stage model:
  Years 1-3: Explicit forecasts
  Years 4-7: Fade period
  Year 8+:   Terminal growth (5-6%)
```

**Blended Target:**
Weighted average (e.g., 50% P/E + 30% EV/EBITDA + 20% DCF)

### Q: Why is the target price different from analyst consensus?

**Possible reasons:**
1. **Different assumptions** - We may use different growth/margin forecasts
2. **Different multiples** - We benchmark to 5Y median, they use forward estimates
3. **More conservative** - We apply margin of safety, they may be optimistic
4. **Data timing** - Consensus may not reflect latest quarter

**Which to trust?**
- If variance < 10%: Both reasonable
- If variance > 20%: Dig into assumptions - one of us is missing something

### Q: Can I customize valuation assumptions?

**A:** Yes, edit `references/analysis-frameworks.md`:

**Change Equity Risk Premium:**
```markdown
# Default: 6.0%
- India ERP benchmark: 5.0–6.0% (use 5.5% as default)
```

**Change Terminal Growth:**
```markdown
# Default: 5-6% for consumption, 4-5% for cyclicals
- Terminal growth: 4% (conservative), 7% (aggressive)
```

After editing, regenerate reports to apply new assumptions.

---

## Report Format Questions

### Q: Can I get the report in Excel instead of Word?

**A:** Not currently, but on roadmap for v1.1.

**Workaround:** 
1. Open the DOCX in Word
2. Copy tables → Paste into Excel
3. Or use: File → Save As → Excel (.xlsx)

### Q: Why is the report so long (3,000+ words)?

**A:** Institutional research reports are comprehensive by design. They cover:
- Business analysis
- Financial deep dive
- Valuation models
- Risk assessment
- Technical analysis
- Management quality
- Catalyst tracking

**Want shorter reports?**
```
Generate a concise 1-page summary for RELIANCE
Focus only on: Valuation, Key Risks, Investment Verdict
```

Or use the `india-stock-onepager` skill (separate, shorter format).

### Q: Can I customize the report template?

**A:** Yes! Edit `references/report-template.md`:
- Reorder sections
- Add/remove sections
- Change table formats
- Modify branding

Then regenerate reports - they'll follow your custom template.

### Q: How do I add my company logo?

**A:** Edit the COVER BLOCK in `report-template.md`:
```markdown
## COVER BLOCK (Header)

```
[COMPANY NAME] ([TICKER])
EQUITY RESEARCH REPORT

[YOUR FIRM NAME]
[Your Logo Image - add after DOCX generation]
```
```

The DOCX skill supports image insertion - add logo to the generated file manually (for now).

---

## Comparison Questions

### Q: How does this compare to paid research services?

| Feature | This Skill | Paid Research (₹5K-25K) |
|---------|------------|-------------------------|
| Data sources | 6-12 | 10-15 |
| Valuation models | 2-3 | 3-5 |
| Turnaround time | 3-5 min | 24-48 hours |
| Cost | Free | ₹5,000-25,000 per report |
| Customization | Full access to template | None |
| Update frequency | On-demand | Quarterly |

**Advantage: Skill**
- Instant gratification
- Unlimited reports
- Fully customizable

**Advantage: Paid**
- Proprietary channel checks
- Management access
- Regulatory compliance (SEBI-registered)

### Q: Should I still subscribe to research services?

**A:** Depends on your needs:

**Use this skill if:**
- Individual investor doing own research
- Portfolio < ₹50L
- Can interpret financial data yourself
- Want quick analysis on-demand

**Use paid services if:**
- Managing OPM (Other People's Money)
- Need SEBI-compliant research for audit trail
- Want exclusive management access/concalls
- Require proprietary sector insights

**Best approach:** Use both!
- Skill for quick screening and idea generation
- Paid for final validation on large positions

---

## Troubleshooting

### Q: Skill doesn't trigger when I ask about a stock

**Diagnosis:** Trigger matching issue

**Solutions:**
1. Be more explicit:
   ```
   ❌ "What do you think about Reliance?"
   ✅ "Analyze RELIANCE stock"
   ✅ "Create an equity research report for RELIANCE"
   ```

2. Specify exchange:
   ```
   ✅ "Analyze NSE:RELIANCE"
   ```

3. Force skill usage:
   ```
   ✅ "Use the india-equity-report skill to analyze RELIANCE"
   ```

### Q: Report shows "Data unavailable" for recent quarter

**Common causes:**
1. **Results not announced yet** - Check BSE/NSE announcements
2. **Screener.in lag** - Wait 1-2 days after announcement
3. **Very new IPO** - Limited historical data

**Fix:**
Provide the data manually:
```
Analyze RELIANCE. Q3 FY26 results (just announced on BSE):
Revenue: ₹2.4L Cr
Net Profit: ₹18,500 Cr
EBITDA: ₹42,000 Cr

Use these figures in the report.
```

### Q: Valuation seems unrealistic (too high/low)

**Check:**
1. Is the EPS correct? (TTM vs FY vs Forward)
2. Is the P/E multiple reasonable? (compare to 5Y avg)
3. Any one-time charges/gains skewing results?

**Example issue:**
```
Wrong: Target ₹15,000 (EPS ₹50, P/E 300x)
Fix:   Target ₹1,500  (EPS ₹5,  P/E 300x) - decimal error
```

**Tell Claude:**
```
The valuation looks wrong. The TTM EPS is ₹5.20, not ₹52.
Recalculate the target using correct EPS.
```

### Q: DOCX file won't open

**Causes:**
1. Incomplete generation (interrupted)
2. File corruption
3. Incompatible Word version

**Fix:**
1. Regenerate report:
   ```
   Regenerate the RELIANCE equity report
   ```

2. Try alternative formats:
   ```
   Export the report as HTML instead of DOCX
   ```

3. Use Google Docs:
   Upload DOCX → Google Docs auto-converts

---

## Usage Scenarios

### Q: I'm a beginner investor. Will I understand the reports?

**A:** Reports are technical but accessible:

**You'll understand:**
- Investment verdict (BUY/SELL/HOLD)
- Target price and upside
- Key risks (plainly stated)
- Price levels (entry zones, stop-loss)

**May need help with:**
- DuPont decomposition
- ROIC-WACC spread
- DCF valuation mechanics
- Forensic accounting flags

**Recommendation:**
1. Start with "Investment Verdict" section (end of report)
2. Read "Executive Summary" (beginning)
3. Gradually work through other sections
4. Refer to WALKTHROUGH.md for metric explanations

### Q: Can I use this for swing trading / short-term?

**A:** Partially.

**Reports optimized for:** 12-18 month investment horizon (fundamental analysis)

**For swing trading:**
- **Use:** Technical Analysis section (Section 10)
  - Support/Resistance levels
  - RSI, MACD signals
  - 20/50 DMA trends
  
- **Ignore:** Long-term DCF models, TAM sizing

**Better approach:**
Combine this with dedicated technical analysis tools for intraday/swing.

### Q: I'm an RIA. Can I share these reports with clients?

**A:** Yes, WITH DISCLAIMERS:

**You MUST:**
- ✅ Keep the SEBI disclaimer intact
- ✅ Add your own RIA disclaimer
- ✅ State "For informational purposes, not SEBI-registered research"
- ✅ Include your SEBI RIA registration number
- ✅ Disclose any conflicts of interest

**You CANNOT:**
- ❌ Remove the skill's disclaimers
- ❌ Market as "official research report"
- ❌ Claim SEBI registration for the report
- ❌ Charge separately for the reports (but can include in overall AUM fee)

**Legal structure:**
```
This report was generated using automated research tools 
and reviewed by [Your Name], SEBI RIA [REG NUMBER].

[Standard RIA Disclaimers]
[Conflict of Interest Disclosures]
```

---

## Advanced Usage

### Q: Can I build a screening system using this?

**A:** Yes! Example workflow:

**Step 1: Screen on Screener.in**
```
Filter:
- Market Cap > 500 Cr
- ROE > 15%
- Debt/Equity < 1
- Sales growth > 15% CAGR
```
**Result:** 50 stocks

**Step 2: Batch analyze top 10**
```
Generate reports for: [10 tickers from Step 1]
```

**Step 3: Review verdicts**
Filter for "BUY" ratings → Shortlist 3-5 stocks

**Step 4: Manual deep dive**
Read full reports for those 3-5, make final decision

### Q: Can I automate quarterly updates?

**A:** Not yet, but workaround:

**Create a reminder:**
```
Every quarter (Jan 15, Apr 15, Jul 15, Oct 15):
  Regenerate reports for: [Your portfolio tickers]
  Compare to previous quarter
  Note any rating changes
```

**Future:** v1.1 will have auto-update feature

### Q: Can I integrate this with Google Sheets?

**A:** Indirectly:

**Export workflow:**
1. Generate report in Claude
2. Copy financial tables from DOCX
3. Paste into Google Sheets
4. Use `=GOOGLEFINANCE()` for live price tracking

**Future:** Direct Sheets integration planned for v1.2

---

## Philosophy & Approach

### Q: Why institutional-grade instead of simpler reports?

**A:** Institutional standards exist for a reason:
- **Completeness** - All material factors considered
- **Traceability** - Every number sourced
- **Rigor** - Multiple valuation methods cross-validate
- **Risk disclosure** - Nothing swept under the rug

Simpler reports often miss critical risks or rely on single valuation method. We err on the side of thoroughness.

### Q: Why so many anti-hallucination measures?

**A:** Financial decisions involve real money. Hallucinated data can lead to:
- Wrong buy/sell decisions
- Misjudged valuations
- Missed risks

**The 7-layer approach ensures:**
- Every figure is traceable
- No invented analyst consensus
- No formula leaks into reports
- Stale data is flagged

**Example of what we prevent:**
```
❌ Hallucinated: "Consensus target: ₹450" (no actual consensus)
✅ Correct:      "Target: ₹450 (derived from 25x P/E on ₹18 EPS)"
                 [Source: Management guidance, Q3 concall]
```

---

## Future Development

### Q: What's on the roadmap?

See [CHANGELOG.md](CHANGELOG.md) for detailed roadmap.

**v1.1 (Q2 2026):**
- FII/DII flow auto-tracking
- Options data (PCR, max pain)
- Excel output format
- Quarterly auto-updates

**v1.2 (Q3 2026):**
- Portfolio-level dashboards
- Google Sheets integration
- Automated peer discovery
- Multi-language support (Hindi)

**v2.0 (Q4 2026):**
- Machine learning price predictions (experimental)
- Sentiment analysis from news
- Earnings surprise tracking
- Alert system for catalysts

### Q: Can I request a feature?

**A:** Absolutely!

**Submit via:**
[GitHub Issues → Feature Request](https://github.com/[username]/india-equity-report-skill/issues/new?template=feature_request.md)

**Include:**
- Problem it solves
- Use case example
- Why existing features don't address it

**Popular requests move up the roadmap.**

---

## Legal & Compliance

### Q: Is this SEBI-compliant?

**A:** The skill itself is a tool, not a SEBI-registered entity.

**Compliance requirements:**
- Tool: ✅ No SEBI registration needed
- Using reports personally: ✅ Fully compliant
- Sharing with friends: ✅ Fine (not solicitation)
- RIA using for clients: ✅ Allowed (with RIA disclaimers)
- Selling research reports: ❌ Requires SEBI RA license

**Key distinction:**
The skill generates "informational analysis" (allowed), not "investment advice/recommendations" (requires license).

### Q: What about copyright on the reports?

**A:** Reports YOU generate are YOUR property.

**You can:**
- Share freely
- Modify as needed
- Use commercially (with disclaimers)
- Publish (with attribution to tool)

**You cannot:**
- Claim the underlying skill code as yours (it's MIT licensed)
- Remove MIT License from skill code
- Remove SEBI disclaimers from reports

**Recommendation:**
Add a footer to your reports:
```
Generated using India Equity Report Skill (MIT License)
Reviewed and distributed by [Your Name/Firm]
```

---

## Still Have Questions?

**Check these resources:**
1. [README.md](README.md) - Feature overview
2. [WALKTHROUGH.md](WALKTHROUGH.md) - Beginner guide
3. [INSTALL.md](INSTALL.md) - Setup help
4. [Examples](examples/) - Sample reports

**Ask the community:**
- [GitHub Discussions](https://github.com/[username]/india-equity-report-skill/discussions)

**Report bugs:**
- [GitHub Issues](https://github.com/[username]/india-equity-report-skill/issues)

**Contact maintainer:**
- Email: [your-email]
- LinkedIn: [your-profile]

---

**Can't find your answer? Ask in Discussions - we're here to help!**
