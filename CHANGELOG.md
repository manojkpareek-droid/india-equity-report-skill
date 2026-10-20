# Changelog

All notable changes to the india-equity-report skill are documented here.

---

## [1.1.0] — 2026-03-05

### Added
- **Peer comparison table** now mandatory in every report's Valuation section (minimum 3 peers: P/E, P/B, ROE, Revenue Growth). Fetched from Trendlyne peers tab or Tickertape comparison. Addresses the single biggest gap identified in v1.0 benchmark.
- **Analyst consensus target** fetch added to Step 2 data table (Trendlyne analyst section). Cited as reference context alongside independently derived target.
- **5Paisa** added as confirmed CMP fallback source (step 1.5 fallback chain) — shows verified NSE close with explicit date stamp.
- **Benchmark Quality Dimensions (D1–D5)** added to SKILL.md Section 5 — a self-assessment rubric for Claude to use before delivering any report.
- `BENCHMARK.md` added to repo root — full quantitative benchmark (3 test cases × 5 dimensions, WITH vs WITHOUT skill), confirming 10% → 100% quality improvement.
- `QUALITATIVE_ANALYSIS.md` added to repo root — root cause analysis of v1.0 gaps and v2.0/v3.0 roadmap.

### Changed
- **Step 1.5 (CMP fetch)**: Yahoo Finance explicitly added to blocked sources with empirical evidence (showed HDFCBANK at ₹1,001.60 vs actual NSE close ₹869.05 — 15% discrepancy, caused by US-session delayed quote).
- **`references/data-sources.md`**: Added 5Paisa as a confirmed CMP source; added Yahoo Finance blocked source entry with explanation; expanded fetch sequence to include steps 6 (peer comparison) and 7 (analyst consensus target).
- **Step 5 quality checklist**: Added two new checks — "CMP source is Tickertape/Google Finance/5Paisa (not Yahoo Finance)" and "Peer comparison table present in Valuation section."
- **Step 4 report writing instructions**: Added mandatory peer comparison table and analyst consensus reference to Valuation section instructions.
- **Tone & Style section**: Added explicit mandate for peer comparison table in Valuation section.

### Fixed
- Yahoo Finance CMP reliability issue (benchmark-confirmed 15% discrepancy vs NSE close for HDFCBANK on 5 Mar 2026).
- Reports with no peer context in valuation — now enforced via Step 2 fetch table and Step 5 checklist.

---

## [1.0.0] — 2026-03-03

### Initial Release
- Institutional-quality Buy/Sell/Hold research reports for NSE/BSE stocks
- Live CMP enforcement via Step 1.5 (Google Finance card + Tickertape fallback)
- Anti-Screener.in stale price guardrail
- Mandatory 7-layer hallucination prevention rules
- Full analysis framework: DuPont ROE, ROIC/WACC, forensic accounting, TAM sizing
- Bull/Base/Bear scenario analysis table in every report
- Split investment verdict (new investors vs existing holders) with specific ₹ price levels
- Mandatory Step 5 quality gate (5-section pre-publish checklist)
- .docx output via docx skill chaining
- Battle-tested on: Dixon Technologies, LatentView Analytics, Macfos Ltd, Reliance Industries, HDFC Bank
