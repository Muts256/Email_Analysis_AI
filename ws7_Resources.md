#### Resources & References

#### Threat Frameworks
#### MITRE ATT&CK
The industry standard framework for mapping adversary behaviour to known tactics, techniques, and procedures (TTPs). All case studies in this project reference relevant ATT&CK techniques.

https://attack.mitre.org

##### MITRE ATT&CK: Phishing (T1566)
The specific technique entry covering spearphishing links, attachments, and service-based phishing.

https://attack.mitre.org/techniques/T1566/

##### MITRE ATT&CK: Business Email Compromise (T1657)
The technique entry covering financially motivated fraud via email.

https://attack.mitre.org/techniques/T1657/

##### MITRE ATLAS
MITRE ATLAS (Adversarial Threat Landscape for Artificial-Intelligence Systems)
It is the AI-specific companion to MITRE ATT&CK: Covering tactics and techniques used against machine learning systems. A natural fit alongside the OWASP LLM reference.

https://atlas.mitre.org

---

#### Email Authentication Standards
##### SPF (Sender Policy Framework) — RFC 7208
The standard defining how receiving mail servers verify that incoming email from a domain is sent from a host authorised by that domain's
administrators.

https://datatracker.ietf.org/doc/html/rfc7208

##### DKIM (DomainKeys Identified Mail) — RFC 6376
The standard defining how email messages are digitally signed to allow receivers to verify the message was sent from an authorised server and was not altered in transit.

https://datatracker.ietf.org/doc/html/rfc6376

##### DMARC (Domain-based Message Authentication) — RFC 7489
The standard that builds on SPF and DKIM to give domain owners the ability to specify how unauthenticated mail should be handled and to receive reporting on authentication results.

https://datatracker.ietf.org/doc/html/rfc7489

---

#### Further Reading:
##### Verizon Data Breach Investigations Report (DBIR)
Published annually, the DBIR provides data-driven analysis of breach patterns across industries. Phishing consistently features as one of the top initial access vectors — a useful reference for contextualising the threat landscape.

https://www.verizon.com/business/resources/reports/dbir/

##### Anti-Phishing Working Group (APWG)
An industry consortium that tracks phishing trends globally. Their quarterly Phishing Activity Trends Reports provide current data on phishing volumes, targeted sectors, and evolving attacker techniques.

https://apwg.org

##### Google Project Zero — Understanding BEC
Technical research and analysis on Business Email Compromise campaigns, covering infrastructure patterns and detection approaches.

https://googleprojectzero.blogspot.com


