####  Phishing Email Analysis Methodology

#### Overview

This template is the foundation of most analyses. It  provides a repeatable, structured approach to phishing triage, designed to be followed consistently, whether you are analysing the first suspicious email or the fiftieth.

AI is used as an analytical aid throughout this process. Each section notes where AI was applied, what it was asked to do, and whether it genuinely added value.

---

#### Step 1: Initial Observation

Before diving into headers or links, take a moment to record your first impressions. What made this email suspicious? Trust your instincts.

*What to note:*
- What triggered the suspicion (reported by user, caught by filter, random check)
- The apparent sender and subject line.
- The overall tone and purpose of the email.

*Why this matters:*

First impressions are data. Documenting them before analysis begins helps you spot patterns across case studies and trains your instincts over time.

---

#### Step 2: Sender Analysis

Attackers invest heavily in making emails look legitimate. This step looks beyond the display name to examine what is actually being sent and from where.

*What to examine:*
- Display name vs actual email address. Do they match?
- The sending domain: Is it a lookalike or typosquat of a legitimate domain?
- Domain age: Newly registered domains are a strong indicator of malicious intent.
- Whether the domain has any legitimate web presence.

*Why this matters:*

Display name spoofing is one of the simplest and most effective phishing techniques. Many users never look past the name they recognise.

---

#### Step 3: Header Analysis

Email headers tell the full story of how a message travelled from sender to inbox. They are difficult to fake entirely and often reveal the clearest evidence of spoofing or malicious infrastructure.

*What to examine:*
- *SPF:* Did the email come from an authorised server for that domain?
- *DKIM:* Is the email's digital signature valid?
- *DMARC:* Did the email pass or fail the domain's authentication policy?
- *Reply-To* Does it differ from the sender address?
- *X-Originating-IP:* Where did the email actually originate from?

*Why this matters:*

A legitimate email from a well-configured domain will typically pass SPF, DKIM and DMARC. Failures across all three are a strong indication that something is wrong.

---

#### Step 4: Content Analysis

This step examines the body of the email — the language, tone, and psychological tactics being used. This is where AI tends to add the 
most value.

*What to examine:*
- Urgency or fear-based language ("Your account will be suspended")
- Requests for credentials, personal information, or payment
- Grammar, spelling, and formatting inconsistencies
- Impersonation of trusted brands or individuals
- Mismatched or generic greetings ("Dear Customer")

*Why this matters:*

Social engineering is the core of most phishing attacks. Understanding the tactic being used helps assess how convincing the email is and who it is likely targeting.

---

#### Step 5: URL and Link Analysis

Links are the most common delivery mechanism for phishing attacks. This step examines every link in the email before anything is clicked.

**What to examine:**
- Hover text vs the actual destination URL, do they match?
- Lookalike domains (e.g., paypa1.com instead of paypal.com)
- URL shorteners masking the true destination
- HTTPS: Its presence does not guarantee legitimacy
- Domain reputation using tools such as VirusTotal or URLScan.io

*Why this matters:*

A convincing email with a malicious link is still a phishing email. Never assume the link matches what the text says.

---

#### Step 6: Attachment Analysis

Not all phishing emails contain attachments, but when they do, this step should never be skipped.

*What to examine:*
- File type executables, Office files with macros, and PDFs are common vehicles
- File name urgency in the name ("Invoice_OVERDUE.pdf") is a common tactic
- Whether an attachment is expected or unsolicited
- Scanning with tools such as VirusTotal, where safe to do so

**Why this matters:**

Malicious attachments can deliver malware, ransomware, or credential harvesters. Even a convincing attachment from a known sender warrants scrutiny if the context is unusual.

---

#### Step 7 AI Contribution

This step is unique to this project. After completing the analysis, this section documents how AI was used and whether it added value.

**What to record:**
- Which step/s was AI applied to
- What prompts were used, and what they returned
- Whether AI spotted anything the manual analysis missed
- Whether AI slowed the process down or sped it up
- Any instances where AI was wrong or unhelpful

*Why this matters:*

This is the core question of the project. Without honestly documenting AI's contribution at each stage, the findings section has no foundation.

---

#### Step 8: Verdict

Every analysis ends with a clear, documented verdict.

**Verdict options:**
- *Legitimate:* No indicators of malicious intent found
-  *Suspicious:* Some indicators present but inconclusive
- *Phishing:* Clear indicators of malicious intent

*What to include:*
- The verdict with a confidence level (low/medium/high)
- The two or three strongest indicators that led to the verdict
- Recommended action (release, quarantine, block sender, escalate)

*Why this matters:*

A structured verdict ensures every analysis ends with a clear, actionable outcome, not just a list of observations.
