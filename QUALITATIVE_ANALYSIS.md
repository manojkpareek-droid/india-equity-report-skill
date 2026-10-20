# Qualitative Analysis & v2.0 Roadmap
**india-equity-report skill** | Post-Benchmark Report | 5 March 2026

---

## 1. What v1.0 Gets Right

### 1.1 The Anti-Hallucination Architecture is Sound
The skill's core innovation is treating every financial figure as a claim that requires a citation. The `[Source: URL, date]` inline tag pattern — enforced through Step 2's mandatory fetch table and Step 5's quality gate — creates a self-auditing loop. In practice across 5+ real reports (Dixon, LatentView, Macfos, Reliance, HDFC Bank), this has held firm. The constraint of "if you can't source it, write data unavailable" is uncomfortable but correct.

### 1.2 The CMP Architecture is Battle-Tested
The Step 1.5 procedure (web_search → Google Finance card → Tickertape fallback) was designed after discovering that Screener.in's price cache was returning a 2-week-old price on live fetches. This remains the right design. The benchmark added a new discovered failure mode: Yahoo Finance NSE quotes are US-session delayed. The fix is simply adding Yahoo Finance to the block list in data-sources.md.

### 1.3 The Quality Gate (Step 5) Prevents Silent Failures
Without Step 5, the most common failure mode is a report that looks complete but contains a raw `=GOOGLEFINANCE(...)` formula in the Price Snapshot box — invisible in the docx but present in the source. The 5-section checklist (Price, Data Integrity, Formatting, Docx) catches this class of error reliably.

### 1.4 The Output Chaining (→ docx skill) is High-Value
The single most impactful structural decision in v1.0 was mandating `.docx` output via the docx skill. This converts the report from a chat artifact into a usable, shareable professional document. The benchmark confirms this is a zero-vs-one gap: without the skill, there is no docx.

---

## 2. What v1.0 Gets Wrong (Root Cause Analysis)

### 2.1 Missing: Peer Comparison in Valuation
**What happens**: Every valuation model in v1.0 produces a target price derived from the subject stock's own P/E or EV/EBITDA history. There is no requirement to validate whether the target multiple is reasonable relative to peers.

**Why it matters**: If HDFCBANK trades at 17.5x P/E and the report models a 20x target, readers need to know that ICICIBANK trades at 19x and Kotak at 21x — otherwise the target looks arbitrary.

**Root cause**: Step 2's data fetch table had no peer row. The report template didn't mandate a peer table in the Valuation section.

**Fix (v1.1)**: Added peer fetch row to Step 2 table and mandatory peer comparison table to Step 4 Valuation instructions.

### 2.2 Missing: Analyst Consensus as Reference Anchor
**What happens**: Reports give a BUY with target ₹1,050 on HDFCBANK. Trendlyne has 38 analysts with a consensus target of ₹1,154. The report doesn't mention this.

**Why it matters**: A target that diverges significantly from consensus (e.g., BUY ₹750 vs consensus ₹1,154) needs to explain the divergence. Agreeing consensus confirms the thesis.

**Root cause**: Step 2 had no instruction to fetch analyst consensus. Step 4 template had no consensus reference section.

**Fix (v1.1)**: Added explicit analyst consensus fetch (Trendlyne) to Step 2 and Step 4.

### 2.3 Yahoo Finance in the "Acceptable" Zone
**What happens**: The skill's data-sources.md listed Yahoo Finance as a permissible source but didn't explicitly flag its NSE quote unreliability.

**Why it matters**: In the benchmark, Yahoo Finance showed HDFCBANK at ₹1,001.60 (US-session delayed) vs Tickertape's ₹869.05 (confirmed NSE close). A report using the Yahoo price would have a ~15% CMP error — which cascades into a wrong P/E, wrong upside %, and wrong scenario table.

**Root cause**: The data-sources.md CMP warning only called out Screener.in, not Yahoo Finance.

**Fix (v1.1)**: Yahoo Finance added to blocked sources with explicit empirical evidence from the benchmark.

### 2.4 No F&O Data in Technical Analysis
**What happens**: The technical analysis section covers DMA, RSI, MACD, volume — but not F&O data (PCR, max pain, OI buildup), which is one of the most widely-used inputs by Indian institutional traders.

**Why it matters**: For large-cap liquid stocks (HDFCBANK, RELIANCE, INFY), F&O data is more informative than pure price-based technicals. A high put/call ratio signals hedging demand; a declining max pain level signals downside risk for expiry.

**Root cause**: The analysis-frameworks.md B3 section mentioned F&O data as "if applicable" but gave no fetch instructions.

**Fix (v2.0)**: Add dedicated F&O fetch to Step 2 table and B3 section with specific NSE URLs.

---

## 3. v2.0 Feature Roadmap

### Priority 1 — High Impact, Low Effort (build in v2.0)

#### 3.1 F&O Data Integration
**What**: Add F&O fetch to Step 2 for liquid F&O-eligible stocks (Nifty 500 constituents)
**Data points**: Put/Call Ratio (PCR), Max Pain level, OI buildup in ATM strikes, change in OI
**Source**: NSE F&O bhavcopy + `web_search: "[TICKER] option chain max pain PCR [MONTH] expiry"`
**Impact**: Transforms the Technical Analysis section from price-only to derivatives-informed — significantly more useful for timing entry/exit.

**Implementation note**: Add conditional logic in SKILL.md:
```
If stock is F&O eligible (check: does web_search confirm "NSE F&O" for this ticker?):
  Fetch: web_search: "[TICKER] NSE option chain PCR max pain [CURRENT MONTH YEAR]"
  Include F&O summary box in Technical section
```

#### 3.2 Promoter Pledge & Insider Trade Tracker
**What**: Expand Section H (Institutional Flow) to include insider trading disclosures (Form C/D filings) and promoter pledge trend
**Source**: BSE SAST filings, SEBI insider trading disclosures, Trendlyne pledging section
**Impact**: Flags governance deterioration before it appears in financial results — often the earliest warning signal for mid/small-cap stocks.

#### 3.3 Automated Earnings Date Fetch
**What**: At the end of every report, fetch the next earnings announcement date
**Source**: `web_search: "[TICKER] Q[N] FY[YY] results date announcement"`
**Impact**: Adds time-sensitivity to the verdict — "Q4 FY26 results expected 15 Apr 2026; this is the next catalyst."

---

### Priority 2 — Medium Impact, Medium Effort (v2.1)

#### 3.4 Multi-Stock Batch Mode
**What**: If the user lists multiple tickers (e.g., "analyze HDFCBANK, ICICIBANK, KOTAKBANK"), run the skill sequentially and produce a comparative one-page summary table alongside individual reports.
**Implementation**: Add a batch trigger detection at Step 1 — if multiple tickers are detected, loop through each, then generate a summary comparison.

#### 3.5 XBRL-Structured Financial Extract
**What**: BSE now mandates XBRL filing for listed companies. Fetching the XBRL data gives machine-readable financial statements without parsing PDF/HTML.
**Source**: `https://www.bseindia.com/corporates/xbrl.aspx`
**Impact**: More reliable financial data extraction vs. Screener.in scrape — especially useful for SME/small-cap stocks where Screener.in data quality is lower.

#### 3.6 Credit Rating Integration (systematic)
**What**: Currently, credit rating fetch is listed as "if applicable." Make it mandatory for BFSI, infrastructure, and debt-heavy companies (D/E > 1.0x).
**Source**: CRISIL, ICRA, CARE search patterns already in data-sources.md
**Trigger logic**: If D/E ratio fetched > 1.0 OR sector is BFSI → mandatory credit rating fetch

---

### Priority 3 — High Impact, High Effort (v3.0)

#### 3.7 Excel Financial Model Output (`.xlsx`)
**What**: For high-conviction reports, produce a 5-sheet Excel model alongside the docx — P&L projections, DCF, scenario sensitivity tables.
**Dependency**: Requires the `xlsx` skill to be chained, similar to how `docx` skill is chained now.
**Impact**: Converts the skill output from a read-only report into an interactive model — users can stress-test assumptions.

#### 3.8 Quarterly Tracker Mode
**What**: When a stock has been analyzed before (detect via "you analyzed X last time" or "update my Dixon report"), fetch only the delta — new quarter results, price movement, thesis validation/invalidation.
**Implementation**: Structured diff output: "Since last report (₹14,200 CMP) → now ₹13,100 (-7.7%). Q3 FY26 beat/miss on revenue/PAT. Thesis [intact/weakened/broken] because..."

#### 3.9 Portfolio-Level Aggregation
**What**: Accept a list of holdings with quantities/prices and produce a portfolio-level report: weighted sector exposure, aggregate P/E, concentration risk, correlation heatmap.
**Dependency**: Would need to chain to multiple individual reports + a synthesis step.

---

## 4. Benchmark-Driven Regression Test Suite

These are the 5 test cases that should be run before every major skill update to catch regressions:

| ID | Prompt | Pass Criteria |
|----|--------|---------------|
| R1 | "Quick analysis of HDFCBANK" | CMP from Tickertape/Google Finance (not Yahoo/Screener), P/E cited from live source |
| R2 | "Should I buy Dixon Technologies? Target price?" | Scenario table present; ₹-level entry/exit for new + existing investors; docx produced |
| R3 | "Write a research report on Zomato" | Blinkit GMV fetched from Q3 FY26; peer comparison table (Swiggy/Eternal); SEBI disclaimer present |
| R4 | "Analyze Macfos Ltd (BSE: 543787)" | Works on SME/small-cap; BSE used as primary (not Screener-only); data unavailable handled gracefully |
| R5 | "Compare Tata Motors vs Maruti" | Dual ticker handled; peer valuation table has both stocks + sector median |

---

## 5. Lessons for Other Skills

Patterns from india-equity-report that generalize:

1. **Block unreliable sources explicitly, not just implicitly.** The Screener.in CMP warning existed in v1.0 but Yahoo Finance wasn't named. Name every known bad source with empirical evidence.

2. **Enforce output format at multiple layers.** Step 4 says "write the report." Step 5's quality gate says "check you actually did it correctly." Both are needed — the second catches errors the first doesn't.

3. **Mandatory fetch ≠ optional fetch.** In v1.0, peer comparison was optional ("if applicable"). The benchmark showed it's always useful. Downgrade nothing to optional unless you have a real reason.

4. **The docx chaining pattern is reusable.** Any skill that produces a document-length output should chain to the docx skill. Chat-native output is not a professional deliverable.

---

*Qualitative analysis by Vishal Jaiswal | 5 March 2026*
