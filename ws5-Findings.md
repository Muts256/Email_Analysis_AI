# Findings & Verdict

## Did AI Make the Analyst Faster?

The short answer is yes — significantly.

A SOC analyst working through three emails manually, producing structured triage reports, extracting IOCs, mapping to MITRE ATT&CK, identifying cross-email patterns, and writing up a campaign assessment would typically spend the best part of two to three hours on this volume of work. That estimate assumes an experienced analyst working without interruption, in a real SOC environment, and that time would likely be longer.

With AI assistance, the same analysis was produced in a fraction of that time. The structured output was consistent across all three case studies, the IOC extraction was thorough, and the cross-email correlation,  which would have required the analyst to mentally hold all three emails in context simultaneously, was produced clearly and without prompting.

For a SOC team processing dozens of flagged emails every day, that difference is not marginal. It is operationally significant.

---

## Did AI Make the Analyst Better?

This is the more interesting question, and the answer is more nuanced.

Across the three case studies, AI demonstrated genuine analytical depth in areas that matter:

**Header analysis** was fast and accurate. Parsing SPF, DKIM, and DMARC results, identifying relay path inconsistencies, and flagging the Message-ID anomaly in Case Study 003, where the ID domain was entirely unrelated to the supposed internal sender, are exactly the kinds of details that get missed under pressure.

**Social engineering identification** was strong. AI consistently named the specific tactics being used — urgency, isolation, authority impersonation, consequence escalation, and grounded each observation in the actual language of the email rather than offering generic observations.

**MITRE ATT&CK mapping** added a layer of structured context that would take a junior analyst considerably longer to produce manually, and might not be produced at all under time pressure.

**Cross-email correlation** was perhaps the most impressive output. Identifying the three-day consecutive pattern, the deliberate use of separate infrastructure, and the escalation in targeting scope required holding all three analyses in context simultaneously — something AI handles without difficulty and without fatigue.

---

## The Finding That Matters Most

Case Study 002 is the one that proves the value of AI assistance most clearly and most honestly.

That email passed every technical check. SPF passed. DKIM passed. DMARC passed with a reject policy. There were no malicious links, no suspicious attachments, no authentication failures to flag. By every technical measure available to a standard email security gateway, it was a clean email.

It was also a sophisticated Business Email Compromise attempt targeting a $47,250.00 wire transfer.

A human analyst under pressure, having already reviewed Case Study 001 with its clear technical failures, could very reasonably see three green checkmarks on Case Study 002 and move on. That is not a failure of skill. That is what cognitive load and time pressure do to even experienced analysts.

AI does not get reassured by green checkmarks. It does not carry the mental weight of the previous alert into the next one. It applied the same depth of behavioural and contextual analysis to Case Study 002 as it did to the emails that were technically obvious — and it was that second layer of analysis, not the technical layer, that exposed the attack.

This is the difficulty human analysts face every day. Authentication checks are necessary but not sufficient. The threat has evolved beyond what technical controls alone can reliably catch — and AI assistance ensures that the behavioural and contextual layer of analysis is applied consistently, regardless of what the technical layer says.

---

## Where AI Falls Short

An honest verdict requires acknowledging the limitations.

**AI cannot verify in real time.** It cannot check live domain reputation, query threat intelligence feeds, or confirm whether an IP address has been seen in prior campaigns. Every IOC still needs to be validated against tools like VirusTotal, URLScan.io, and MXToolbox. AI identifies what to look at — it cannot tell you what those lookups will find.

**AI does not know your organisation.** It had no way of knowing whether TechNova Ltd has a genuine business relationship with Pinnacle Group, whether David Hargreaves is a known contact, or whether a wire transfer request of this nature would be unusual. That organisational context lives with the analyst — not with the AI.

**AI can be confidently wrong.** On occasion, AI may misinterpret a malformed header, assign an incorrect MITRE technique, or produce a severity rating that does not account for context the analyst holds but has not shared. Its output should always be reviewed, not accepted without question.

**The prompt shapes the output.** AI is only as good as the question it is asked. A vague or poorly structured prompt produces a vague or incomplete analysis. The master triage prompt used in this project was deliberately designed to be comprehensive — but it took iteration to get there.

---

## Is It Worth Adding to Your Workflow?

Yes — with clear eyes about what it is and what it is not.

AI is not a replacement for an analyst. It does not replace the judgement, the organisational knowledge, the threat intelligence relationships, or the experience that a skilled SOC analyst brings to the table. Anyone who tells you otherwise is overselling it.

What it is, is a genuinely useful analytical partner — one that is fast, consistent, tireless, and thorough in ways that are difficult to maintain manually at volume. Used well, it raises the floor of every analysis. It ensures that the behavioural and contextual layer is never skipped, even when time pressure makes skipping it tempting.

For junior analysts, it provides structure and depth that accelerates development. For senior analysts, it handles the mechanical parts of triage quickly, freeing up time and cognitive capacity for the judgement calls that actually require experience.

---

## A Personal Reflection

Working through these three case studies, the moment that stayed with me was Case Study 002.

Seeing SPF pass, DKIM pass, and DMARC pass with a reject policy, and then watching AI continue past those green checkmarks and systematically analyse the email on behavioural grounds alone, made something clear that I had understood intellectually but not quite felt before.

The authentication checks passing did not mean the email was safe. It meant the attacker had done their homework. And in that gap — between what the technical controls confirm and what the full picture actually shows, is exactly where analysts get caught out and where AI assistance 
makes a genuine difference.

The checks being comprehensive is not just about speed. It is about consistency. It is about ensuring that every email, regardless of how clean it looks on the surface, gets the same depth of scrutiny. That is what this project set out to test. And on that measure, the answer is clear.

AI does not make the analyst redundant. It makes the analyst better equipped for the threat that actually exists — not the one that fails all its authentication checks and announces itself clearly, but the one that looks legitimate right up until the moment it isn't.
