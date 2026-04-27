# Google AI Vulnerability Research Lab

This repository documents legitimate security research methodology for identifying vulnerabilities in Google AI products, with a focus on responsible disclosure through Google's AI Vulnerability Reward Program (VRP).

**⚠️ IMPORTANT DISCLAIMER**
- This research is conducted ethically and responsibly
- All testing is performed in isolated environments with proper authorization
- No actual user data or credentials are targeted or captured
- Findings are reported to Google through official channels only
- This repository is for educational and research purposes

## Overview

This lab provides resources for security researchers to:
1. Understand vulnerability types in AI systems
2. Learn responsible disclosure practices
3. Document findings for Google's AI VRP
4. Develop proof-of-concept demonstrations safely

## Target Vulnerability: Persistent HTML Injection in AI Systems

### What We're Researching
- How AI applications handle and sanitize user-provided content
- Whether injected HTML persists across sessions
- If phishing content could be delivered through AI features
- Whether AI systems legitimize or amplify injected malicious content

### What We're NOT Doing
- Creating functional phishing sites
- Stealing real user credentials
- Targeting actual Google users
- Deploying malicious code to production systems

## Directory Structure

```
.
├── README.md                          # This file
├── VULNERABILITY-GUIDE.md             # Detailed vulnerability explanation
├── RESEARCH-METHODOLOGY.md            # Step-by-step research process
├── RESPONSIBLE-DISCLOSURE.md          # How to report findings
├── examples/
│   ├── vulnerable-pattern-1.md       # Code patterns to investigate
│   ├── vulnerable-pattern-2.md       # More patterns
│   └── sanitization-examples.md      # Good vs bad code
├── reports/
│   └── REPORT-TEMPLATE.md            # Google VRP submission template
└── tools/
    └── testing-checklist.md          # Verification checklist
```

## Quick Start

1. **Read the Vulnerability Guide** → `VULNERABILITY-GUIDE.md`
2. **Learn the Research Methodology** → `RESEARCH-METHODOLOGY.md`
3. **Understand Responsible Disclosure** → `RESPONSIBLE-DISCLOSURE.md`
4. **Study Examples** → `examples/` directory
5. **Use Report Template** → `reports/REPORT-TEMPLATE.md`

## Google AI VRP Scope

**Covered Products:**
- Google Search
- Gemini (Web, Android, iOS)
- Google Workspace (Gmail, Drive, Meet, Calendar, etc.)
- AI Studio, Jules, and AI-integrated features

**In-Scope Vulnerabilities:**
- Rogue actions via prompt injection
- Sensitive data exfiltration
- **Phishing enablement via persistent HTML injection** ← Our focus
- Model theft
- Access control bypass

**Reward Tiers:**
- Critical: Up to $20,000 + $10,000 bonus = $30,000
- High: Up to $15,000
- Medium: Up to $5,000
- Low: $100+

## Research Ethics Checklist

Before starting any research, confirm:
- [ ] Testing is in YOUR OWN isolated environment
- [ ] You have authorization to test (own accounts/systems)
- [ ] No real user data will be captured
- [ ] No malicious code is deployed to Google systems
- [ ] Testing follows Google's responsible disclosure policy
- [ ] You plan to report findings through official channels

## Reporting to Google

When you find a vulnerability:

1. **Document thoroughly** using our report template
2. **Submit through** https://bughunters.google.com/
3. **Include:**
   - Clear vulnerability description
   - Step-by-step reproduction instructions
   - Proof-of-concept (conceptual, not malicious)
   - Potential impact assessment
   - Screenshots/logs demonstrating the issue

## Resources

- [Google Bug Hunters Program](https://bughunters.google.com/)
- [Google AI VRP Rules](https://bughunters.google.com/about/rules/google-friends/ai-vulnerability-reward-program-rules)
- [Responsible Disclosure Best Practices](https://cheatsheetseries.owasp.org/cheatsheets/Vulnerability_Disclosure_Cheat_Sheet.html)
- [OWASP XSS Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)

## Questions?

Refer to the detailed guides in this repository or consult Google's official VRP documentation.

---

**Last Updated:** 2026-04-27
**Status:** Active Research Lab
