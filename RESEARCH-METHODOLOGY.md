# Security Research Methodology - Step-by-Step

This document outlines how to **responsibly research** persistent HTML injection vulnerabilities in Google AI products.

## Phase 1: Reconnaissance (Week 1)

### Step 1.1: Identify Target Features
**Goal:** Find Google AI features that:
- Accept user input (text, files, content, etc.)
- Process and display that content to other users
- Use AI to summarize, translate, or format content

**Examples to investigate:**
- Google Docs with Gemini integration
- Gmail with AI features
- Google Chat with AI
- Google Workspace collaborative tools
- Shared Gemini conversations
- Google Drive with AI features

### Step 1.2: Review Product Documentation
- Read Google's official documentation for each feature
- Understand how content flows through the system
- Identify potential injection points
- Note which fields accept rich content

### Step 1.3: Create Test Accounts
**IMPORTANT:** Use only **YOUR OWN accounts**

```
Create at least 3 Gmail accounts:
- account1@gmail.com (attacker role - YOUR account)
- account2@gmail.com (victim role - YOUR account)
- account3@gmail.com (validation role - YOUR account)

DO NOT use other people's accounts
DO NOT create accounts pretending to be others
```

### Step 1.4: Setup Test Environment
- Set up isolated Google Workspace accounts
- Enable all AI features
- Document the testing environment setup
- Take baseline screenshots

---

## Phase 2: Passive Testing (Week 1-2)

### Step 2.1: Simple HTML Injection Tests

In **your own account only**, test simple HTML:

```
Test Input 1:
<h1>Test Header</h1>

Test Input 2:
<b>Bold Text</b><i>Italic Text</i>

Test Input 3:
<p>Paragraph</p>
```

**What to document:**
- Does HTML render or get escaped?
- Can you see your test tags in the output?
- Are tags processed by AI or displayed as text?

### Step 2.2: Script Tag Tests

```
Test Input:
<script>console.log('test')</script>
```

**What to document:**
- Does script execute?
- Does browser console show errors?
- Is tag removed or escaped?

### Step 2.3: Event Handler Tests

```
Test Input:
<img src=x onerror="console.log('xss')">

Test Input:
<body onload="console.log('xss')">

Test Input:
<div onclick="alert('xss')">Click me</div>
```

**What to document:**
- Do event handlers execute?
- Can you trigger console output?
- Are attributes stripped?

### Step 2.4: Persistence Testing

**For each test input:**

1. **Inject** the HTML in your account
2. **Share** the content with your other test account
3. **Log out** completely from browser
4. **Clear browser cache** (important!)
5. **Log back in** from a different device/browser
6. **Check** if the injection persists

**What to document:**
- Does content persist across sessions?
- Does it affect other accounts?
- How long does it persist?
- Can other users see it?

---

## Phase 3: Targeted Testing (Week 2-3)

### Step 3.1: Phishing Content Testing

**ONLY use legitimate-looking content that doesn't actually steal data:**

Create HTML that *looks like* a phishing form but:
- ✅ Doesn't submit anywhere
- ✅ Doesn't capture real data
- ✅ Is clearly fake for testing purposes

```html
<!-- SAFE FOR TESTING: Form doesn't actually submit -->
<form onsubmit="event.preventDefault(); return false;">
  <h2>TEST FORM - This is not real</h2>
  <input type="email" placeholder="Email">
  <input type="password" placeholder="Password">
  <button type="submit">TEST BUTTON</button>
</form>
```

### Step 3.2: Document What You See

For each test:

| Aspect | Document |
|--------|----------|
| **Feature Tested** | Which Google product/feature |
| **Input Provided** | Exact HTML/content injected |
| **Result** | What actually happened |
| **Rendered?** | Did HTML render as code? |
| **Executable?** | Did scripts/events execute? |
| **Persistent?** | Did it stay across sessions? |
| **Cross-user?** | Could other accounts see it? |
| **Screenshot** | Visual proof of the issue |

### Step 3.3: Test AI Processing

**Question:** Does the AI legitimize injected content?

1. Inject HTML containing a "fake alert"
2. Ask the AI to "summarize this content"
3. Document how the AI processes it

**Example:**
```
Injected content:
<div style="background: red; color: white;">URGENT: Your account has been compromised!</div>

AI Response:
Does the AI highlight this as important?
Does it reformat it?
Does it amplify the urgency?
```

---

## Phase 4: Validation (Week 3)

### Step 4.1: Verify the Vulnerability

Before you claim you found a vulnerability, confirm:

- [ ] Input I provided actually persists
- [ ] It appears in other user accounts (my own test accounts)
- [ ] It appears in the AI-generated output
- [ ] I can reproduce it consistently
- [ ] It's not intended behavior
- [ ] It violates Google's security model
- [ ] It could actually harm real users

### Step 4.2: Verify You Can Reproduce It

**Reproduction test:**
1. Clear all cache and cookies
2. Use a fresh browser/device
3. Repeat the exact same steps
4. Confirm you get the same result

**Document:**
- Step-by-step instructions
- Time it takes to reproduce
- What browser/OS you used
- Screenshots at each step

### Step 4.3: Assess the Impact

Ask yourself:

**Scope of Impact:**
- How many users could be affected?
- Could an attacker inject once and reach 1000s of users?
- Is it easy to automate?

**Type of Impact:**
- Could this enable data theft?
- Could this enable account takeover?
- Could this spread malware?
- Could this enable phishing at scale?

**Severity Rating:**
- CRITICAL: Account takeover, widespread data theft
- HIGH: Phishing capability, significant data exposure
- MEDIUM: Limited impact, requires specific conditions
- LOW: Proof-of-concept only, limited real-world impact

---

## Phase 5: Documentation (Week 4)

### Step 5.1: Create Your Research Report

Use the template in `reports/REPORT-TEMPLATE.md`

**Include:**
- Clear vulnerability description
- Exact reproduction steps
- Screenshots/video
- Impact assessment
- CVSS score
- Suggested mitigation

### Step 5.2: Organize Evidence

Create a folder: `research/findings/`

```
research/findings/
├── screenshots/
│   ├── step-1-injection.png
│   ├── step-2-persistence.png
│   ├── step-3-cross-user.png
│   └── step-4-in-ai-output.png
├── logs/
│   ├── browser-console.txt
│   ├── network-traffic.txt
│   └── timestamps.txt
├── reproduction-steps.md
└── impact-assessment.md
```

### Step 5.3: Prepare Submission

Before submitting to Google:

- [ ] Reviewed all documentation
- [ ] Removed any sensitive information
- [ ] Tested reproduction steps one more time
- [ ] Screenshots are clear and labeled
- [ ] CVSS score is accurate
- [ ] Report is professional and clear

---

## Phase 6: Responsible Disclosure (Week 5+)

### Step 6.1: Submit to Google

Go to: https://bughunters.google.com/

**Steps:**
1. Create an account
2. Click "Submit a vulnerability"
3. Choose "Google AI Products" or relevant category
4. Fill out the vulnerability report form
5. Attach evidence
6. Submit

### Step 6.2: Communication Timeline

- **Day 1:** Submit report
- **Days 1-7:** Google may ask for clarification
- **Days 7-90:** Google investigates and fixes
- **Day 90:** Public disclosure permitted (if agreed)
- **Day 90+:** You may receive reward ($100 - $30,000+)

### Step 6.3: Follow Up

- Respond to Google's questions promptly
- Provide additional evidence if requested
- Don't share findings publicly before 90 days
- Be patient - Google is thorough

---

## ⚠️ Things NOT To Do

### ❌ DO NOT

- Create actual phishing sites
- Capture real credentials
- Target other people's accounts
- Deploy to production systems
- Share exploits publicly
- Automate attacks at scale
- Use this for criminal purposes
- Bypass authentication
- Access other people's data

### ❌ DO NOT Assume

- That the feature "looks broken" means it's vulnerable
- That HTML rendering is always a bug
- That AI processing is always a vulnerability
- That persistence is always unintended

### ✅ DO Instead

- Use only your own test accounts
- Document everything thoroughly
- Report responsibly to Google
- Follow the 90-day disclosure timeline
- Be professional and clear
- Ask questions if unsure

---

## Success Criteria

You've completed legitimate research when:

✅ You've tested the vulnerability thoroughly  
✅ You have clear reproduction steps  
✅ You have visual evidence (screenshots)  
✅ You understand the real-world impact  
✅ You've written a professional report  
✅ You're ready to submit to Google  
✅ You haven't harmed any real users  
✅ You haven't captured any real credentials  

---

## Troubleshooting

**Q: I tested but couldn't reproduce the issue**
A: It may not be a real vulnerability. Try different Google products or features. Not everything that looks suspicious is exploitable.

**Q: The AI processed my injection but didn't execute it**
A: The AI might be safely handling it. Document this anyway - it shows Google's security is working.

**Q: I'm not sure if what I found is actually a vulnerability**
A: Submit it anyway with a note that you're unsure. Google's team can assess it. Better to report something questionable than miss a real issue.

**Q: How long until I get paid?**
A: After submission: 90+ days for investigation and fix. Once fixed, you'll receive an email about the reward. Google processes rewards quarterly.

---

**Remember:** The goal is to help Google make their products more secure, not to exploit them.
