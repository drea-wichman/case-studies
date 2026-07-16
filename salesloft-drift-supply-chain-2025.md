# Salesloft-Drift Supply Chain Breach (2025)
**Case:** CS-003  
**Type:** GRC Case Study | NCSC Supply Chain Principles Analysis  
**Date:** July 16, 2026

---

> *This is an independent educational case study based on publicly available incident reports and investigations. It is not an official audit or compliance assessment.*

## Executive Summary

The August 2025 Salesloft-Drift breach compromised more than 700 organizations without directly breaching a single one of them. Attackers stole the OAuth tokens, the digital keys that let Drift's chatbot connect to its customers' systems, and walked in with valid credentials. Every victim had approved the access that was used against it. This case study applies the NCSC's principles of supply chain security to ask whether the UK government's checklist for vetting a supplier would have caught this risk before the connection was approved, and what the answer reveals about the limits of vendor assessment.

---

## Overview

Three companies feature in this incident and two of them have confusingly similar names:

- **Salesforce** - software where companies store customer records and support history.
- **Drift** - a website chatbot that connects to Salesforce to log visitor conversations.
- **Salesloft** - the company that owns Drift. Its systems were compromised.

Salesloft owns Drift. Salesforce, despite the name, is unrelated to both.

Drift is the chat window that appears on a company's website. When a visitor types into it, Drift files the conversation into the company's Salesforce as a new sales lead. To do this automatically, each customer grants Drift standing access to its Salesforce through an OAuth token. The token works like a key: Salesforce accepts it without asking further questions, because the customer authorized it.

By 2025 thousands of companies used Drift, most of them mid-size to large businesses selling to other businesses. Its confirmed customers included some of the best-known security companies in the world. Each of them held the same quiet arrangement: an outside vendor's product, holding a valid key to the system where their customer data lived.

In August 2025, attackers who had compromised Salesloft's infrastructure stole those tokens and used them. The result was one of the largest supply chain breaches on record: more than 700 organizations were potentially impacted through a connection they themselves had approved, without their own systems ever being broken into directly.

---

## Timeline

- **March-June 2025** - Attackers gain access to Salesloft's private repositories on GitHub, the platform where most software companies store and develop their code. They download code, add a guest user account, and quietly explore both the Salesloft and Drift environments. This goes undetected for months. How the attackers first got in has never been publicly disclosed.
- **June-August 2025** - The attackers pivot from GitHub into Drift's AWS environment, where they obtain the OAuth tokens for Drift customers' integrations. Mandiant's concluded investigation dates the full intrusion from March 22 to September 5, 2025.
- **August 8-18, 2025** - Using OAuth tokens stolen from Drift's infrastructure, the attackers log into victims' Salesforce systems and bulk-export data, primarily support case records, deleting the export jobs afterward to hide their tracks.
- **August 9, 2025** - A stolen token is also used to access a small number of Google Workspace email accounts connected through Drift's email product.
- **August 20, 2025** - Salesloft, working with Salesforce, revokes all active Drift tokens. The Drift app is removed from the Salesforce marketplace.
- **August 28, 2025** - Google's threat intelligence team discloses that the compromise extended beyond Salesforce to Drift's other integrations and advises companies to treat all Drift-connected credentials as compromised.
- **Early September 2025** - Salesloft takes Drift offline entirely.
- **September 7, 2025** - Salesforce restores its integration with Salesloft's main platform. Drift remains offline.

---

## Threat Actor

**Group:** UNC6395  
**Type:** Uncategorized threat cluster  
**Origin:** Unknown  
**Method:** Supply chain compromise. Broke into the vendor's development infrastructure, stole customer OAuth tokens, used them for mass data theft, then mined the stolen data for further credentials.  
**Attribution:** "UNC6395" is the tracking label assigned by Google's investigators; UNC means uncategorized, a cluster of activity not yet tied to a known group. A separate criminal group publicly claimed the attack; Google's investigators found no evidence supporting that claim. No country or established group has been credibly identified.  
**Notable:** The operation was patient and quiet: months of undetected access, no ransomware, no immediate extortion. The attackers deleted their export jobs to hide their tracks and prioritized harvesting credentials pasted inside stolen support tickets, keys that could unlock victims' other systems. This was theft designed to enable more theft.  

---

## Operational Impact

More than 700 organizations were potentially impacted by the Drift compromise, according to Google's investigators. Confirmed victims include some of the largest security companies in the world, all of which disclosed actual data theft: Cloudflare, Zscaler, and Palo Alto Networks all publicly acknowledged exposure, and a small number of Google Workspace accounts connected through Drift were accessed.

The data taken varied by company but centered on Salesforce records: customer and contact information and, above all, support case text, the running record of help requests where customers routinely paste credentials, configuration details, and error logs.

The operational burden landed after the theft. Google's advisories urged every affected organization to search its Salesforce data for exposed credentials and revoke them, which for victims meant combing through years of accumulated support tickets. Cloudflare's public account of its own response, identifying and rotating 104 exposed Cloudflare API tokens and notifying affected customers, illustrates the scale of that work.

For Salesloft, the incident meant taking its product entirely offline and a public investigation by Google's Mandiant. For its customers, the lasting cost is harder to count.

---

## The Trust Relationship

The victims' own controls did not fail; the failure sat in an approved connection to another company. An integration token is a standing grant of access: not challenged by MFA, not expiring at the end of a shift, working every time because working every time is its purpose. Once issued, the customer's security depends on the vendor's, on how Salesloft guarded its repositories and credentials, none of it visible from outside.

Seven hundred organizations did not make the same technical mistake. They made the same governance decision: accept a standing connection to a vendor whose internal security they could not observe. Each inherited that vendor's compromise the instant it happened.

Whether that decision could have been made better is the question the rest of this study tests, against the NCSC's principles of supply chain security.

---

## The 12 Principles Analysis

*Note: The principles referenced below are from "The principles of supply chain security" published by the National Cyber Security Centre (NCSC), version 1.0, reviewed October 2025. The NCSC organizes these into four stages: Understand the risks (1-3), Establish control (4-9), Check your arrangements (10), and Continuous improvement (11-12).*

### Stage I: Understand the Risks

**1. Understand what needs to be protected and why**

Drift's integration token granted continuous access to the customer's Salesforce, including customer records, support histories, and credentials pasted into support tickets. Whether affected organizations had mapped the full scope of what that token could reach is not publicly known. What is known is that when the token was stolen, it provided access to data sensitive enough to fuel further attacks.

**Verdict: the scope of access the Drift token provided, and the sensitivity of the data it could reach, became apparent only after the breach.**

---

**2. Know who your suppliers are and build an understanding of what their security looks like**

Drift's customers knew Drift. Most would not have known that Drift's parent company, Salesloft, stored its code on GitHub, or how Salesloft managed access to those repositories. The attackers entered through Salesloft's GitHub, not through Drift itself. This principle asks buyers to look beyond the product they use and understand the vendor's own infrastructure. The breach began in a system one layer removed from what a typical customer might have evaluated.

**Verdict: the attack path ran through infrastructure that was almost certainly outside the scope of any customer's vendor assessment.**

---

**3. Understand the security risk posed by your supply chain**

This principle asks organizations to assess the risk that a supplier's systems could be compromised and used as a path into their own. The risk that materialized here was not that Drift's chatbot would malfunction, but that its credentials could be stolen and used to reach Salesforce. That scenario is precisely the category of supply chain risk this principle exists to surface.

**Verdict: the scenario that occurred is the one this principle directly addresses.**

---

### Stage II: Establish Control

**4. Communicate your view of security needs to your suppliers**

Salesloft maintained SOC 2 Type 2, ISO 27001, and ISO 27701 certifications and published a Trust Portal, providing a basis for security evaluation. Salesloft published detailed security controls including a zero-trust model, privileged access management with MFA, 24/7 SIEM monitoring, automated code scanning, and annual penetration testing. However, Salesloft operates under a standardized Master Subscription Agreement (current published version, February 2026). No publicly available materials indicate that individual buyers could negotiate security obligations beyond the standard terms. The communication was one-directional: Salesloft published, buyers evaluated, but the two-way security conversation this principle envisions does not appear to have existed.

**Verdict: Salesloft's security posture was transparent and well-credentialed. But the principle asks buyers to communicate their security needs to the supplier. Under Salesloft's standardized model, that channel did not exist. Evaluate or leave were the options.**

---

**5. Set and communicate minimum security requirements for your suppliers**

Salesloft's published controls met or exceeded common security baselines. A buyer evaluating Salesloft against this principle would have found strong credentials and independent audits. But buyers could verify, not dictate. The controls that ultimately failed were ones the vendor claimed to have in place.

**Verdict: a buyer applying this principle would likely have approved Salesloft. The breach occurred despite a program that, on paper, addressed the risks that materialized.**

---

**6. Build security considerations into your contracting processes and require that your suppliers do the same**

Salesloft's MSA included a Security Addendum and Data Processing Addendum. This principle focuses on ensuring suppliers pass security requirements to their own subcontractors. No subcontractor was involved in the breach. The attack ran through Salesloft's own infrastructure and its own product.

**Verdict: not applicable. The principle addresses supply chain depth. This breach did not involve subcontractor failure.**

---

**7. Meet your own security responsibilities as a supplier and consumer**

This principle places responsibility on the supplier to uphold its own security, report issues proactively, and welcome scrutiny. Salesloft published a strong security program and held multiple certifications. Its GitHub was compromised for approximately three months without detection. Attackers then operated inside its Drift infrastructure for a further period before spending ten days exporting data from customer Salesforce environments. Salesloft has not publicly disclosed how the initial access to its GitHub was obtained.

**Verdict: this is the principle that failed. Salesloft's documented security program did not prevent or detect the compromise of its own systems for months. The responsibility the principle places on the supplier to maintain its own security was not met.**

---

**8. Raise awareness of security within your supply chain**

This principle asks organizations to ensure key staff understand security risks and to promote threat information sharing across the supply chain. Salesloft required all personnel to complete security and privacy awareness training during onboarding and annually thereafter, and published security alerts through internal communications. Despite this, the GitHub compromise went undetected for approximately three months.

**Verdict: a security awareness program existed. The breach suggests it was insufficient to prevent the specific failures that occurred, though the relationship between training and this compromise cannot be directly established.**

---

**9. Provide support for security incidents**

This principle asks suppliers to have clear incident reporting requirements, defined timescales, and to share lessons learned. Salesloft notified affected customers beginning August 20, two days after the exfiltration ended. Formal breach notifications followed in the days after. Mandiant was retained in late August. Salesloft published updates through its Trust Center throughout September, including the disclosure that the compromise originated in its GitHub account months earlier. Individual victims such as Cloudflare, PagerDuty, and Dynatrace published their own incident reports detailing their response and findings.

**Verdict: once the breach was identified, Salesloft's notification and disclosure were relatively prompt. The principle also asks suppliers to share lessons learned. Salesloft disclosed the attack path and engaged Mandiant publicly, but has never disclosed how the initial GitHub access was obtained, leaving an open question for any customer attempting to learn from the incident.**

---

### Stage III: Check Your Arrangements

**10. Build assurance activities into your supply chain management**

This principle asks buyers to build audit rights into contracts, require upward reporting of security performance, and establish assurance mechanisms such as penetration testing or formal certifications. Salesloft held SOC 2 Type 2 and ISO 27001 certifications, both independently audited annually and published on its Trust Portal. These provided assurance that a security program existed and was tested. However, Salesloft's standardized MSA (current published version) does not include a customer right to audit. Buyers could review published audit reports but could not independently examine Salesloft's systems, test its controls, or verify specific practices such as how tokens were stored or how GitHub access was managed.

**Verdict: third-party assurance existed and was accessible. Salesloft's standardized MSA does not include a customer right to audit. The NCSC specifically recommends building audit rights into contracts. Under Salesloft's terms, that option was not available.**

---

### Stage IV: Continuous Improvement

**11. Encourage the continuous improvement of security within your supply chain**

This principle asks buyers to actively encourage suppliers to improve, support them in doing so, and monitor progress. Under a standardized SaaS agreement with no mechanism for individual buyer input, this principle has no operational pathway. Drift's customers could not encourage, require, or monitor security improvements at Salesloft. They could observe what Salesloft chose to publish on its Trust Portal.

**Verdict: not applicable under Salesloft's standardized model. The principle requires a collaborative relationship that did not exist.**

---

**12. Build trust with suppliers**

The NCSC envisions strategic partnerships where buyer and supplier share concerns, exchange information, and treat supply chain security as a joint responsibility. Drift's customer relationship was transactional: sign the MSA, connect the integration, use the product. No evidence exists of a structured security dialogue between Salesloft and its Drift customers before the breach. After the breach, Salesloft published updates and engaged Mandiant publicly, which is closer to the spirit of this principle, but reactive rather than ongoing.

**Verdict: the trust relationship this principle describes is not reflected in Salesloft's standardized contract or public-facing security model. What the contract established was access, not partnership.**

---

## Regulatory Outlook

The Cyber Security and Resilience Bill, which cleared the House of Commons in June 2026 and is now before the House of Lords, with Royal Assent expected late in the year, begins to address the structural gap this case study exposes. The bill expands the Network and Information Systems Regulations 2018 to bring key suppliers into scope, introduces mandatory incident reporting with initial notification within 24 hours and a full report within 72, creates a "designated critical supplier" regime, and sets tiered fines reaching £17 million or 4% of turnover at the top level. Where the NCSC's principles rely on buyers to demand protections that vendors may not offer, the bill places obligations directly on the suppliers themselves. It does not solve the problem: its scope is limited to critical sectors, and it is not yet law. But it represents the UK government's acknowledgment that voluntary guidance and market incentives have not been sufficient.

---

## Lessons Learned

**Guidance without legislation is not governance.** The NCSC published 12 principles for supply chain security. Of those, at least five (Principles 4, 5, 10, 11, and 12) assume a buyer-supplier relationship that does not exist under standardized SaaS agreements. The principles tell buyers to negotiate, audit, encourage, and build trust with vendors who offer none of those channels and have zero obligation to. When guidance assumes leverage the market does not provide, it is aspiration without mechanism. Seven hundred organizations were breached while the principles sat on a government website. The UK's Cyber Security and Resilience Bill exists because guidance proved unenforceable and, in this case, structurally inapplicable.

**The affected organizations settled for standardized terms.** The affected organizations were not small companies unfamiliar with vendor risk. They include Cloudflare, Palo Alto Networks, and Zscaler, companies whose entire product is security. Each connected Drift to its most sensitive customer data under a standardized contract that offered no audit rights, no negotiation, and no mechanism to verify the vendor's internal practices. The NCSC's guidance was publicly available. The decision to connect without the protections it recommends was made by organizations with the resources and expertise to apply them.

**Salesloft's documented security program did not prevent or detect a three-month compromise.** Salesloft held SOC 2 Type 2, ISO 27001, and ISO 27701 certifications. It published detailed controls including a zero-trust model, privileged access management, and 24/7 monitoring. Its GitHub was compromised for three months without detection. The attackers operated inside its infrastructure, stole customer tokens, and spent ten days exporting data before anyone noticed. Its published security program looked strong on paper. What it looked like in practice was a three-month undetected compromise and hundreds of organizations' data walking out the door. The entire burden of catching this failure fell on Salesloft's customers, who were expected to build a relationship that Salesloft's own contract rejected.

**The system is backwards.** The NCSC's principles place the burden of supply chain security on the buyer, who is unable to audit the vendor, negotiate terms, verify internal controls, or compel improvements. The vendor, which holds the keys, the code, and the data, faces no binding obligations beyond what it voluntarily adopts. Salesloft operated within the only rules that existed: vague data protection requirements and its own self-selected certifications. Those rules were not enough. When the incentive to secure a product is voluntary and the incentive to ship it is not, the outcome is predictable. In this incident, voluntary guidance protected no one. The pending bill's premise is that companies must be legally required to secure the data they hold and the access they are granted. This case is the evidence for that premise. Anything less is a utopian checklist built for a market that does not exist.

---

## Sources

- [Salesloft Trust Center — Update on Mandiant Drift and Salesloft Application Investigations](https://trust.salesloft.com/?uid=Update+on+Mandiant+Drift+and+Salesloft+Application+Investigations), investigation concluded September 30, 2025
- [Google Threat Intelligence Group — Widespread Data Theft Targets Salesforce Instances via Salesloft Drift](https://cloud.google.com/blog/topics/threat-intelligence/data-theft-salesforce-instances-via-salesloft-drift), August 26, 2025, updated August 28, 2025
- [Cloudflare — Our response to the Salesloft Drift incident](https://blog.cloudflare.com/response-to-salesloft-drift-incident/), September 2, 2025
- [PagerDuty — Salesloft's Drift Integration Security Incident Impacting Some PagerDuty Salesforce Data](https://www.pagerduty.com/blog/uncategorized/saleslofts-drift-integration-security-incident-impacting-some-pagerduty-salesforce-data/), September 2025
- [Dynatrace — Salesloft Drift Incident: Dynatrace's Response](https://www.dynatrace.com/news/blog/salesloft-drift-incident-dynatraces-response/), September 8, 2025
- [The Hacker News — Salesloft OAuth Breach via Drift AI Chat Agent Exposes Salesforce Customer Data](https://thehackernews.com/2025/08/salesloft-oauth-breach-via-drift-ai.html), August 28, 2025
- [Permiso — Anatomy of the Salesloft Breach](https://permiso.io/blog/anatomy-of-the-salesloft-breach), September 2025
- [Salesloft — Security and Compliance](https://www.salesloft.com/security-compliance)
- [Salesloft — Master Subscription Agreement](https://www.salesloft.com/legal/msa-2026-02-10), version dated February 10, 2026
- [NCSC — The principles of supply chain security](https://www.ncsc.gov.uk/collection/supply-chain-security/principles-supply-chain-security), version 1.0, reviewed October 22, 2025
- [UK Parliament — Cyber Security and Resilience (Network and Information Systems) Bill](https://bills.parliament.uk/bills/4035)
- [House of Lords Library — Cyber Security and Resilience Bill briefing](https://lordslibrary.parliament.uk/research-briefings/lln-2026-0032/), July 2026