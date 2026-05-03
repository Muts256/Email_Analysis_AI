#### Phishing Email Case Studies

---

#### Case Study 001

*Email #:* 1
*Threat Type:* Credential Phishing

#### IOCs
- *Sender:** "Microsoft 365 Security" <security-noreply@microsoft365-verify.com> — display name impersonates Microsoft but domain is microsoft365-verify.com, not microsoft.com
- *Reply-To:* m365-support@securemail-verify.net — entirely different domain to the sender, a strong indicator of malicious intent
- *Source IP:* 194.165.16.83 (external relay), 45.133.203.17 (originating host)
- *Domains/URLs:* microsoft365-verify.com, securemail-verify.net, https://microsoft365-verify.com/reset?token=aHR0cHM6Ly9sb2dpbi5taWNyb3NvZnQuY29t&uid=james.miller&org=technovaLtd  The token value is Base64 encoded and decodes to https://login.microsoft.com, a common obfuscation technique
- *Attachments:* None
- *Authentication Results:* SPF: FAIL — IP 194.165.16.83 not authorised for microsoft365-verify.com | DKIM: NONE — no signature present | DMARC: FAIL — policy=none meaning no enforcement action taken

#### Social Engineering Indicators
- Urgency and fear — "Your password will expire in 24 hours."
- Consequence escalation — "your account will be temporarily locked" and "IT department will require an in-person visit"
- Impersonation of a trusted platform — Microsoft 365 branding and terminology
- Personalisation — target's full name, username, and organisation embedded in the URL and tracking pixel
- Tracking pixel present — confirms email delivery and open status back to attacker infrastructure

#### Technical Assessment
- *Initial Access:* Valid Accounts via harvested credentials (user clicks link and submits credentials to attacker-controlled page)
- *Impact:* Account takeover, unauthorised access to email, Teams, OneDrive, and any connected services. Potential for lateral movement or Business Email Compromise from the compromised account
- *Likelihood of Success:* Medium — authentication failures are detectable but DMARC policy=none means no automatic quarantine or rejection
- *MITRE ATT&CK:*
  - T1566.002 — Phishing: Spearphishing Link
  - T1078 — Valid Accounts
  - T1598 — Steal Web Session Cookie (likely post-credential harvest)

*Severity: HIGH*
Justification: Targets a named individual with personalised content, uses credential harvesting infrastructure, and DMARC policy=none means the email is unlikely to be automatically blocked.

#### Recommendation
- *User:* Do not click the link. Do not enter credentials on any page reached from this email. Report to the SOC immediately
- *SOC:* Block domains microsoft365-verify.com and securemail-verify.net at email gateway and web proxy. Check SIEM for any other emails from 194.165.16.83 or 45.133.203.17. Verify whether james.miller clicked the link or submitted credentials. If credentials were entered, initiate password reset and review account activity immediately
- *Preventive:* Update DMARC policy for technovaLtd.com to p=quarantine or p=reject. Deploy user awareness training on Microsoft impersonation phishing. Consider enforcing MFA across all Microsoft 365 accounts

---

#### Case Study 002

*Email #:* 2
*Threat Type:* Business Email Compromise (BEC)

#### IOCs
- *Sender:* "David Hargreaves - CEO" <d.hargreaves@pinnacle-group.com> — no display name spoofing detected, sender domain appears consistent
- *Reply-To:* Not present — email instructs recipient to reply directly, keeping communication within the attacker's controlled mailbox
- *Source IP:* 203.78.142.56
- *Domains/URLs:* pinnacle-group.com — no malicious URLs present. The attack is entirely social engineering-based
- *Attachments:* None
- *Authentication Results:* SPF: PASS | DKIM: PASS | DMARC: PASS (policy=reject) — all authentication checks pass, meaning this email would not be flagged by standard technical controls

#### Social Engineering Indicators
- Authority impersonation: sender presents as the CEO of an external organisation
- Extreme urgency: "before 3:00 PM EST" and "without exception."
- Isolation tactic: "do not discuss this with anyone else."
- Availability barrier:  "I am in back-to-back board meetings and cannot take phone calls" — pre-emptively removes the most effective verification method
- Confidentiality pressure: "until the deal is announced Monday."
- Specific financial detail: precise bank account, routing number, and amount to appear legitimate and reduce hesitation
- Reply-only instruction: "reply to this email only for confirmation." Designed to keep the victim inside the attacker's controlled channel.

#### Technical Assessment
- *Initial Access:* Not applicable — no malware or credential harvesting. The email itself is the attack
- *Impact:* Direct financial loss of $47,250.00. Potential for further requests if initial transfer succeeds. Reputational damage if the organisation is seen to have been defrauded
- *Likelihood of Success:* High — all authentication checks pass, the email contains no malicious links or attachments, and the social engineering is sophisticated and contextually convincing
- *MITRE ATT&CK:*
  - T1566.001 — Phishing: Spearphishing Attachment (adapted: no attachment but same spearphishing principle)
  - T1657 — Financial Theft
  - T1585 — Establish Accounts (attacker likely compromised or registered pinnacle-group.com to pass authentication)

**Severity: CRITICAL**
Justification: All technical authentication checks pass, making this invisible to standard email security controls. The attack targets a financial process with a specific and immediate monetary outcome. The sophistication of the social engineering significantly increases the likelihood of success.

#### Recommendation
- *User:* Do not process the transfer. Do not reply to the email. Attempt to verify the request by calling David Hargreaves directly using a phone number sourced independently, not from this email. Report to the SOC immediately
- *SOC:* Investigate pinnacle-group.com. Check the domain registration date, WHOIS records, and whether TechNova Ltd has any legitimate business relationship with Pinnacle Group. Search SIEM for any prior communication from this domain. Alert the finance team and any staff with wire transfer authority. If a transfer has already been made, contact the bank immediately
- *Preventive:* Implement a dual-authorisation policy for all wire transfers above a defined threshold. Establish a verbal verification requirement for any financial request received by email. Conduct targeted BEC awareness training for finance and executive assistant staff

---

#### Case Study 003

*Email #:* 3
*Threat Type:* Malware Delivery

#### IOCs
- *Sender:* "TechNova Ltd Human Resources" <hr-benefits@technovaLtd.com> — display name and domain both appear internal, but the email did not originate from TechNova infrastructure
- *Reply-To:* Not present
- *Source IP:* 77.91.124.38 — external and unknown, inconsistent with internal HR communications
- *Domains/URLs:* None — attack vector is the attachment
- *Attachments:* Employee_Benefits_Q2_2025.xlsm (487 KB) — .xlsm is a macro-enabled Excel file, a well-established malware delivery format
- *Authentication Results:* SPF: SOFTFAIL — IP 77.91.124.38 not explicitly authorised for technovaLtd.com | DKIM: FAIL — signature verification failed | DMARC: FAIL — policy=quarantine, meaning this email should have been quarantined automatically

#### Social Engineering Indicators
- Internal impersonation: pretends to originate from TechNova Ltd's own HR department
- Broad targeting: sent to all employees, maximising the chance of at least one user complying
- Legitimacy framing: uses a routine, expected business process (benefits review) to lower suspicion
- Explicit macro enablement instructions — steps 1 through 4 walk the user through disabling Microsoft Office security protections
- Deadline pressure: "submit your selections by Friday, 18 April 2025."
- Familiar contact detail: references HR extension 4500 to appear authentic

#### Technical Assessment
- *Initial Access:* Phishing attachment — macro-enabled Excel file likely delivers a malicious payload upon macro execution
- *Impact:* Malware infection of the opening user's device. Depending on payload: ransomware deployment, credential harvesting, remote access trojan (RAT) installation, or lateral movement across the TechNova network. Broad targeting means potential for widespread infection
- *Likelihood of Success:* Medium to High — internal impersonation is convincing and the benefits context is routine. DMARC policy=quarantine should catch it, but relies on the quarantine being reviewed rather than released
- *MITRE ATT&CK:*
  - T1566.001 — Phishing: Spearphishing Attachment
  - T1204.002 — User Execution: Malicious File
  - T1059 — Command and Scripting Interpreter (macro execution)
  - T1486 — Data Encrypted for Impact (if ransomware payload)

*Severity: CRITICAL*
Justification: Impersonates a trusted internal function, targets the entire organisation, and the macro-enabled attachment has the potential to deliver a range of high-impact payloads. A single user enabling macros could result in a network-wide compromise.

#### Recommendation
- *User:* Do not open the attachment. Do not enable macros under any circumstances. If the file has already been opened, disconnect from the network immediately and contact the SOC. Report the email without clicking anything
- *SOC:* Quarantine the email across all mailboxes immediately — do not allow any user to open it. Submit the attachment to a sandbox environment (e.g. Any.run or Cuckoo) for detonation and payload analysis. Search SIEM for any instances of the file being opened or macros being executed. Check endpoint detection and response (EDR) telemetry for any suspicious process activity originating from Excel. Block IP 77.91.124.38 at the perimeter firewall
- *Preventive:* Enforce DMARC quarantine policy to ensure automatic quarantine is actioned. Disable macros by default across all Microsoft Office installations via Group Policy. Implement application whitelisting to prevent unauthorised executables. Deploy targeted awareness training on macro-enabled file risks

---

#### Cross-Email Correlation

#### Timing Pattern
The three emails arrived on consecutive working days — Monday 07 April, Tuesday 08 April, and Wednesday 09 April 2025. This is not coincidental. A three-day sequence of escalating attacks against the same organisation strongly suggests a coordinated campaign rather than opportunistic phishing.

##### Targeting Pattern
The campaign demonstrates a deliberate escalation in targeting scope and sophistication:

| Email | Target | Scope | Authentication |
|---|---|---|---|
| Case Study 001 | james.miller (named individual) | Single user | All checks fail |
| Case Study 002 | lisa.thompson (finance/admin role implied) | Single user | All checks pass |
| Case Study 003 | all-employees | Entire organisation | Partial failure |

This suggests the threat actor conducted reconnaissance on TechNova Ltd before launching the campaign, identifying named staff, their roles, and the organisation's email infrastructure.

#### Infrastructure Observations
- No IP addresses are shared across the three emails, suggesting the attacker deliberately used separate infrastructure for each attack to avoid correlation and reduce the risk of a single block taking down the entire campaign
- All three emails successfully reached TechNova's internal mail store (mail-store01.technovaLtd.com), indicating the organisation's perimeter controls were insufficient to stop any of them at the gateway
- The Message-ID in Case Study 003 (mail-node41.biz) is entirely unrelated to technovaLtd.com, which is a clear indicator of external origin despite the internal impersonation

#### Campaign Assessment
Taken together, these three emails represent a multi-vector, multi-day campaign with three distinct objectives — credential harvesting, financial fraud, and malware delivery. The use of separate infrastructure, varied attack types, and a progression from individual targeting to organisation-wide targeting is consistent with a threat actor that is patient, organised, and familiar with TechNova Ltd's structure.

This is not opportunistic phishing. This is targeted attack activity.

---

#### Key Takeaways

These three case studies demonstrate a principle that sits at the heart of effective phishing triage: **technical analysis alone is not enough**.

Case Study 001 was technically detectable: SPF, DKIM, and DMARC all failed. A well-configured email gateway with an enforced DMARC policy would have quarantined or rejected it. Technical controls would have worked here.

Case Study 002 passed every technical check. SPF passed. DKIM passed. DMARC passed with a reject policy. No links. No attachments. By every technical measure, this was a legitimate email. Only behavioural and contextual assessment, the urgency, the isolation tactic, the unavailability of the sender, and the unusual financial request  reveal it as an attack. Without that layer of analysis, this email walks straight through.

Case Study 003 sits in the middle: Partial technical failures that should have triggered quarantine, combined with highly convincing internal impersonation that could easily deceive a user who receives a quarantine release notification without context.

The lesson across all three is consistent: effective email triage requires the analyst to ask both *what does the technical evidence say* and *does this behaviour make sense*. Headers tell you where an email came from. Context tells you whether it should have been sent at all. Neither question is sufficient on its own. Together, they give you the full picture.

AI accelerates both layers of this analysis, parsing headers quickly, identifying social engineering patterns in the body, and mapping findings to established frameworks. What it cannot replace is the analyst's judgement about whether something feels right. That remains the most important tool in the triage process.
