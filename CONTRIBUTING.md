# Contributing to India Equity Report Skill

Thank you for your interest in improving this skill! This guide will help you contribute effectively.

---

## 🎯 Ways to Contribute

### 1. **Bug Reports**
Found an issue? Help us fix it.

**Before submitting:**
- Search [existing issues](https://github.com/[username]/india-equity-report-skill/issues)
- Verify the bug on latest version
- Collect reproduction steps

**Submit via:** [New Bug Report](https://github.com/[username]/india-equity-report-skill/issues/new?template=bug_report.md)

**Include:**
- Stock ticker and query used
- Expected vs actual output
- Error messages (if any)
- Screenshots of report issues

### 2. **Feature Requests**
Have an idea? We want to hear it.

**Good feature requests:**
- Solve a real problem you've encountered
- Include use case examples
- Consider implementation complexity

**Submit via:** [New Feature Request](https://github.com/[username]/india-equity-report-skill/issues/new?template=feature_request.md)

### 3. **Documentation Improvements**
Found unclear instructions or errors?

**Documentation includes:**
- README.md (main overview)
- WALKTHROUGH.md (beginner guide)
- INSTALL.md (setup instructions)
- examples/ (sample reports)
- Inline comments in SKILL.md

### 4. **Code Contributions**
Ready to write code? Follow the workflow below.

---

## 🚀 Contribution Workflow

### Step 1: Fork & Clone

```bash
# Fork the repo on GitHub, then:
git clone https://github.com/YOUR-USERNAME/india-equity-report-skill.git
cd india-equity-report-skill

# Add upstream remote
git remote add upstream https://github.com/ORIGINAL-OWNER/india-equity-report-skill.git
```

### Step 2: Create Feature Branch

```bash
git checkout -b feature/your-feature-name

# Examples:
# feature/add-fii-flow-tracking
# fix/screener-timeout-handling
# docs/improve-installation-guide
```

### Step 3: Make Changes

**File structure:**
```
india-equity-report-skill/
├── india-equity-report/          # Main skill files
│   ├── SKILL.md                  # Core logic & workflow
│   └── references/
│       ├── analysis-frameworks.md  # Edit for new metrics
│       ├── data-sources.md        # Edit for new sources
│       └── report-template.md     # Edit for formatting
├── examples/                     # Add sample outputs
├── tests/                        # Add test cases
└── docs/                         # Add documentation
```

**Editing guidelines:**

**For SKILL.md:**
- Preserve YAML frontmatter structure
- Document all new data fetching steps
- Add error handling for edge cases
- Include inline comments for complex logic

**For analysis-frameworks.md:**
- Add formulas with source citations
- Include interpretation guidance
- Provide worked examples
- Flag any assumptions

**For report-template.md:**
- Maintain section hierarchy
- Preserve source citation format
- Keep SEBI disclaimer intact
- Test with actual stock data

### Step 4: Test Thoroughly

**Minimum test coverage:**
Test on these stock categories:
1. ✅ Large-cap (e.g., RELIANCE, HDFCBANK)
2. ✅ Mid-cap (e.g., DIXON, LATENTVIEW)
3. ✅ Small-cap/SME (e.g., MACFOS)
4. ✅ Different sectors (IT, BFSI, Manufacturing, Retail)

**Test checklist:**
- [ ] Skill triggers correctly
- [ ] Data fetching succeeds (all sources)
- [ ] Valuation calculations accurate
- [ ] Report formatting clean (no broken tables)
- [ ] DOCX generation works
- [ ] No hallucinated data
- [ ] Source citations present

**Generate test reports:**
```bash
# In Claude, test your changes:
Analyze RELIANCE using the updated india-equity-report skill
Analyze DIXON using the updated skill
Analyze MACFOS using the updated skill
```

Save outputs to `tests/` directory for comparison.

### Step 5: Commit Changes

**Commit message format:**
```
type(scope): description

[optional body]
[optional footer]
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation only
- `style`: Formatting, no logic change
- `refactor`: Code restructuring
- `test`: Adding tests
- `chore`: Build/tooling changes

**Examples:**
```bash
git commit -m "feat(valuation): add PEG ratio calculation"
git commit -m "fix(data-fetch): handle Screener.in timeout gracefully"
git commit -m "docs(walkthrough): add mid-cap stock example"
```

### Step 6: Push & Create PR

```bash
git push origin feature/your-feature-name
```

**On GitHub:**
1. Go to your fork
2. Click "Compare & pull request"
3. Fill out PR template:

```markdown
## Description
[What does this PR do?]

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Performance improvement

## Testing
Tested on:
- [ ] RELIANCE (large-cap)
- [ ] DIXON (mid-cap)
- [ ] MACFOS (small-cap)

## Screenshots
[Attach before/after report comparisons]

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-reviewed changes
- [ ] Commented complex sections
- [ ] Updated documentation
- [ ] No breaking changes
- [ ] Tested on 3+ stocks
```

4. Submit PR

---

## 📋 Contribution Guidelines

### Code Style

**SKILL.md structure:**
```markdown
---
name: skill-name
description: Trigger description...
---

# Skill Title

## 0. Pre-flight
[Read reference files]

## 1. Workflow
### Step 1 — [Action]
[Instructions]

### Step 2 — [Action]
[Instructions]

## 2. [Major Section]
[Content with subsections]
```

**Markdown formatting:**
- Use `###` for subsections
- Use `>` for callout boxes
- Use `|---|---|` for tables
- Use ` ``` ` for code blocks

**Data fetching:**
```markdown
| Data needed | Primary source | Fallback |
|---|---|---|
| [Metric] | [URL/method] | [URL/method] |
```

### Naming Conventions

**Files:**
- Lowercase with hyphens: `analysis-frameworks.md`
- Not: `Analysis_Frameworks.md` or `analysisFrameworks.md`

**Sections:**
- Sentence case: `## Investment Verdict`
- Not: `## INVESTMENT VERDICT` or `## investment verdict`

**Variables (in examples):**
- Square brackets: `[TICKER]`, `[Company]`
- Not: `<TICKER>` or `{Company}`

### Quality Standards

**Before submitting, ensure:**

✅ **No Hallucinations**
- Every financial figure sourced
- No invented analyst consensus
- No estimated numbers without flagging

✅ **Error Handling**
- Graceful fallbacks for missing data
- User-friendly error messages
- No silent failures

✅ **Documentation**
- Every new feature documented
- Complex logic commented
- Examples provided

✅ **Backward Compatibility**
- Existing reports still generate
- No breaking changes to YAML schema
- Deprecated features have migration path

---

## 🎨 Priority Contribution Areas

### High Priority

1. **FII/DII Flow Integration**
   - Auto-fetch from moneycontrol.com
   - Historical trend charts
   - Flow signal interpretation

2. **Options Data Module**
   - Put/Call Ratio
   - Max Pain calculation
   - OI buildup analysis

3. **Peer Auto-Discovery**
   - Smart peer selection algorithm
   - Same sector + similar market cap
   - Business model similarity scoring

4. **Multi-Language Support**
   - Hindi report template
   - Regional language support
   - Bilingual output option

### Medium Priority

5. **Excel Output Format**
   - Multi-sheet workbook
   - Interactive dashboards
   - Embedded charts

6. **Quarterly Tracker**
   - Auto-update existing reports
   - Quarter-over-quarter comparison
   - Delta highlights

7. **Portfolio Aggregation**
   - Multi-stock dashboard
   - Correlation matrix
   - Sector exposure analysis

### Feature Requests Welcome

- Credit rating integration
- Insider trading tracker
- Analyst target compilation
- Earnings surprise history
- Short interest data

---

## 🧪 Testing Requirements

### Unit Tests (Future)
For major logic changes:
```python
# tests/test_valuation.py
def test_pe_rerating_calc():
    eps = 45.20
    target_pe = 25
    expected_target = 1130
    assert calculate_target_pe(eps, target_pe) == expected_target
```

### Integration Tests
Test full workflow:
```
Input: "Analyze RELIANCE"
Expected:
1. ✅ CMP fetched (₹ number, not formula)
2. ✅ 5-year P&L retrieved
3. ✅ Q3 FY26 results included
4. ✅ Valuation models run
5. ✅ DOCX generated
```

### Regression Tests
Verify no breakage:
```bash
# Run on known stocks
python tests/regression_suite.py

# Should pass for:
RELIANCE, HDFCBANK, INFY, TCS, DIXON, LATENTVIEW, MACFOS
```

---

## 📞 Getting Help

**Questions about contributing?**
- [GitHub Discussions](https://github.com/[username]/india-equity-report-skill/discussions)
- Tag: `question` or `help-wanted`

**Need code review feedback?**
- Request review in PR
- Tag maintainers: `@[maintainer-username]`

**Want to become a maintainer?**
- Contribute 3+ meaningful PRs
- Show consistent engagement
- Express interest via Discussion

---

## 🏆 Recognition

**Contributors will be:**
- Listed in README.md
- Mentioned in release notes
- Credited in report footer (optional)

**Top contributors get:**
- Maintainer status
- Direct push access
- Co-ownership of roadmap

---

## 📜 Code of Conduct

### Our Pledge
We pledge to make participation in this project a harassment-free experience for everyone.

### Our Standards
**Positive behavior:**
- Using welcoming and inclusive language
- Being respectful of differing viewpoints
- Accepting constructive criticism gracefully
- Focusing on what's best for the community

**Unacceptable behavior:**
- Trolling, insulting, or derogatory comments
- Public or private harassment
- Publishing others' private information
- Spamming issues/PRs
- Other unprofessional conduct

### Enforcement
Violations reported to [maintainer-email] will be reviewed and may result in:
1. Warning
2. Temporary ban
3. Permanent ban

---

## 🔒 Security Issues

**Found a security vulnerability?**

**DO NOT** open a public issue.

**Instead:**
1. Email: [security-email]
2. Subject: `[SECURITY] India Equity Report Skill`
3. Include:
   - Vulnerability description
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)

**We will:**
- Acknowledge within 48 hours
- Investigate and confirm
- Release patch ASAP
- Credit you in security advisory (unless you prefer anonymity)

---

## 📄 License

By contributing, you agree that your contributions will be licensed under the MIT License.

See [LICENSE](LICENSE) file for full terms.

---

**Thank you for contributing! 🙏**

Every bug fix, feature addition, and documentation improvement makes this tool better for the entire community of Indian equity investors.

*Happy contributing!*
