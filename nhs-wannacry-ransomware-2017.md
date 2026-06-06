# NHS WannaCry Attack (2017)

> [!NOTE]
> **Updated April 23, 2026:** Revised to sharpen accountability analysis, refine framing around attack targeting, clarify the kill switch mechanism, and add post 2017 context on NHS cyber incidents.

**Type:** GRC Case Study | ISO 27001 Analysis  
**Date:** March 27, 2026 | **Revised:** April 23, 2026

---

> *This is an independent educational case study based on publicly available post-incident reports and investigations. It is not an official audit or compliance assessment.*

## Executive Summary
The 2017 WannaCry ransomware attack on the NHS was not a sophisticated operation. It exploited a known vulnerability with a publicly available patch, on systems that had been flagged as outdated for years, inside an organization that had been warned about exactly this risk twelve months prior. The result was 81 affected trusts, 19,000 cancelled appointments, and £92 million in damages. This case study applies an ISO 27001 gap analysis to identify the specific control failures that made the attack possible and outlines a remediation roadmap to prevent recurrence.

---

## Overview

The National Health Service is the United Kingdom's publicly funded healthcare system, established in 1948 and serving over 65 million people. The NHS is one of the largest employers in the world and runs on a large network of interconnected systems including patient records, diagnostic equipment, and communications infrastructure across hundreds of hospital trusts and GP surgeries nationwide.

On May 12, 2017, a ransomware worm called WannaCry tore through 150 countries infecting over 200,000 computers in hours. WannaCry exploited a Windows vulnerability called EternalBlue, originally developed by the NSA, stolen and leaked publicly by a hacker group called Shadow Brokers on April 14, 2017. Although Microsoft had patched the vulnerability on March 14, nearly two months before the attack, most of the NHS had not applied it.

The NHS was not the intended target, it was the most exposed large institution in the worm's path. WannaCry was indiscriminate.  It spread automatically to any reachable Windows system running the vulnerable service, attacking targets across continents without discrimination. It became the largest cyber incident to affect the NHS.

---

## Timeline

- **March 14, 2017** — Microsoft releases a patch for the EternalBlue vulnerability across all supported Windows versions.
- **April 14, 2017** — Shadow Brokers leak EternalBlue publicly. The exploit is now available to anyone.
- **March–April 2017** — NHS Digital issues critical alerts warning NHS organizations to patch their systems. Nobody checked if anyone actually did it.
- **May 12, 2017, 07:44 UTC** — WannaCry launches globally. Within hours it spreads across 150 countries. NHS systems begin going down. 45 NHS organizations including 37 trusts are infected by end of day.
- **May 12, 2017, 15:03 UTC** — Security researcher Marcus Hutchins analyzes a WannaCry sample and notices the malware was programmed to check for a specific unregistered domain before executing. The check was likely a feature intended to prevent the malware from running inside security research and analysis sandboxes. If the domain responded the malware would assume it was being studied and shut down. Hutchins registers the domain for $10.69, activating this domain check globally and halting the attack within hours.
- **May 13–14, 2017** — NHS staff work through the weekend to contain damage and prevent a second wave on Monday. Five hospitals diverting patients. Staff resort to pen and paper.
- **October 2017** — National Audit Office publishes its investigation confirming the attack was preventable and that the Department of Health had been warned about NHS cyber risk a full year prior.
- **December 2017** — US and UK governments formally attribute WannaCry to North Korea's Lazarus Group.

---

## Threat Actor

**Group:** Lazarus Group  
**Type:** State-sponsored  
**Origin:** North Korea  
**Method:** Ransomware worm. EternalBlue exploit used to automatically spread WannaCry across unpatched Windows systems, encrypting files and demanding Bitcoin ransom  
**Attribution:** Formally attributed to North Korea by the US and UK governments in December 2017. North Korea has denied involvement.  
**Notable:** Most ransomware groups are criminal organizations motivated purely by money. Lazarus Group works for the North Korean government. The following traits of WannaCry suggest it was either unfinished or potentially released prematurely: the ransom demand was somewhat low at $300–$600 per machine, the payment infrastructure used only three hardcoded Bitcoin wallets with no way to keep track of who made payments, and the total ransom collected was approximately $140,000 against estimated total damages of $4 billion. These traits raise questions about whether financial gain was the primary motivation or if the malware escaped before it was ready.

---

## Operational Impact

At least 81 of 236 NHS trusts in England were affected, 34 directly infected and the rest disrupted through preventative shutdowns or shared systems with infected organizations. Eight percent of GP surgeries were also impacted.

Hospitals were locked out of their computers, patient records, and diagnostic equipment at the same time. MRI scanners, blood storage refrigerators, and theatre equipment were among the devices affected. Staff reverted to pen and paper and used personal mobile phones after internal communications went down. Thousands of critical and elective procedures were cancelled, totaling 19,000 appointments in one week. Total cost to the NHS was £92 million, £19 million in lost output during the attack and £73 million in IT recovery costs afterward. No patient deaths were directly attributed to WannaCry in the initial investigation but post-event analysis has raised questions about that claim. The NHS did not pay the ransom.

---

## Control Failures & Risk Gaps

**Failure to apply a known patch:** Microsoft released a patch for EternalBlue on March 14, 2017, nearly two months before the attack. NHS Digital followed with critical alerts in March and April telling organizations to apply it and most of the NHS did not.

**Outdated operating systems:** Microsoft had ended XP support in 2014 and the Department of Health stated in 2014 that migrating away from XP was essential by April 2015, yet 5% of NHS computers were still running it on the day of the attack. Unsupported systems do not receive security patches, which means every unpatched vulnerability is permanent.

**No compliance verification:** NHS Digital sent alerts but had no way to confirm anyone acted on them. Warnings went out to hundreds of trusts with no follow-up and no audit. Sending a warning is not the same as managing a risk.

**Poor network segmentation:** WannaCry spread across NHS systems because devices and departments were not isolated from each other, paving the way for it to spread across entire trusts.

**No incident response plan:** When the attack hit nobody knew who was in charge. The NHS had never rehearsed for a national cyberattack so there was no playbook. Communications collapsed because email systems were either infected or shut down to stop the spread.

**Ignored warnings:** The Department of Health had been warned about NHS cyber risk a full year before WannaCry but did not formally respond until July 2017, two months after the attack.

---

## Regulatory & Compliance Implications

**Data Protection Act 1998:** At the time of the attack the NHS was governed by the UK's Data Protection Act 1998. The attack exposed patient and organizational data, triggering obligations to report to the Information Commissioner's Office. The NHS's failure to implement basic security measures raised serious questions about whether it had met its legal duty to protect personal data.

**GDPR:** WannaCry occurred one year before GDPR came into force in May 2018. Had the attack happened after GDPR, the NHS would have faced a 72 hour mandatory breach notification requirement and potential fines of up to 4% of annual turnover for failure to implement appropriate technical and organizational security measures. The unpatched systems and ignored warnings would have been difficult to defend under GDPR's accountability principle.

**NIS Regulations 2018:** The UK's Network and Information Systems Regulations did not come into force until after WannaCry. Under NIS the NHS would have been required to have appropriate security measures in place and report incidents to regulators. WannaCry would have triggered both obligations.

**Ransom Payment:** The NHS did not pay the ransom which avoided any sanctions risk, but the absence of a legal requirement to report ransom payments in 2017 meant there was no obligation to disclose even if they had paid.

**Regulatory Timing:** WannaCry exposed a significant gap. GDPR and NIS are the frameworks that would have required the NHS to take cybersecurity seriously but they did not yet exist. The attack became one of the key arguments for why they were needed.

---

## ISO 27001 Controls Mapping

*Note: Control references below reflect ISO 27001:2013 Annex A, the version in effect at the time of the attack.*

ISO 27001 is an international standard for information security management. The following gap analysis maps NHS control failures against the relevant Annex A controls.

| Control | Requirement | Observed State | Gap | Risk Impact |
|---|---|---|---|---|
| A.12.6.1 Technical Vulnerability Management | Identify and patch vulnerabilities in a timely manner | Patch MS17-010 was available March 14, 2017. NHS Digital sent alerts. Most NHS systems were still unpatched when the attack hit. | No patch management process. No one verified the alerts were acted on. | EternalBlue spread freely across a network that had a fix sitting unused for two months. |
| A.8.1 Asset Management | Maintain an inventory of assets and ensure they are protected | No centralized asset inventory. No visibility into how many devices ran unsupported software. | Couldn't identify vulnerable systems, let alone fix them. | Windows XP machines were already end of life and became a permanent open door. |
| A.13.1.3 Network Segregation | Segment networks to limit the spread of incidents | No effective segmentation across departments, facilities, or device types. | One flat network. No boundaries. | A single entry point took down trusts across England within hours. |
| A.16.1 Incident Management | Maintain a documented incident response capability | No national response plan. No designated lead. No rehearsed procedures. | Nobody knew who was in charge when it mattered. | Response was reactive and communications collapsed immediately. |
| A.18.1 Compliance with Legal Requirements | Meet applicable legal and regulatory obligations | Patient data exposed. Systems containing personal data ran unpatched, unsupported software. | No technical measures in place to meet Data Protection Act 1998 obligations. | Regulatory exposure. GDPR liability would have been significant had the attack happened a year later. |

---

## Recommendations

**A.12.6.1 — Patch Management**
Deploy a centralized patch management tool (WSUS, SCCM, or equivalent). Critical patches applied within 48 hours, high severity within 7 days. Compliance verified automatically, not by hoping someone read an email.

**A.8.1 — Asset Inventory**
Build and maintain a centralized asset inventory covering every device including medical equipment. Unsupported operating systems get isolated or replaced on a fixed timeline. No exceptions without documented sign-off.

**A.13.1.3 — Network Segmentation**
Separate clinical networks from corporate IT. High-risk devices get their own VLANs with strict access controls. One infected machine should not be able to reach everything else.

**A.16.1 — Incident Response**
Write the plan before the attack, not during it. Assign named roles, rehearse annually, and make sure everyone knows who picks up the phone when systems go down.

**A.18.1 — Regulatory Compliance**
Map legal obligations to technical controls and assign owners to each one. GDPR's 72-hour clock starts the moment you know about a breach. That is not enough time to figure out the rules from scratch.

---

## Remediation Roadmap

A step-by-step plan to fix the gaps identified and prevent future attacks.

| Phase | Timeline | Key Actions | Goal |
| :--- | :--- | :--- | :--- |
| **Phase 1: Immediate Fixes** | Days 0–30 | • Apply all missing security patches immediately.<br>• Identify and isolate any computers running old/legacy software.<br>• Separate critical hospital systems from general office networks. | Make sure no known vulnerabilities are left open. |
| **Phase 2: Process Setup** | Months 1–3 | • Set up an automatic system to install updates so humans don't forget.<br>• Create a clear list of every computer and device in the hospital.<br>• Write a simple "Emergency Plan" so staff know who to call if systems go down. | Move from "hoping" things are safe to "knowing" they are safe. |
| **Phase 3: Long-Term Safety** | Months 3–12 | • Practice the Emergency Plan regularly with staff.<br>• Regularly check for new security risks and fix them quickly.<br>• Train all staff on how to spot phishing and suspicious emails. | Make safety a daily habit and workplace culture, not just a one-time fix. |

---

## Lessons Learned

**A patch is only useful if it's applied.**
EternalBlue had a fix which sat unused across hundreds of NHS systems for nearly two months. Vulnerability management is not simply knowing a patch exists, it's about making sure it gets installed.

**Warnings mean nothing without accountability.**
The NHS received alerts from NHS Digital and a warning from the Department of Health a full year before the attack. None of it translated into action. An organization that issues guidance without verifying compliance has not actually managed a risk.

**Legacy systems are a liability, not an inconvenience.**
Windows XP was end of life in 2014 and was a known vulnerability in 2017. The decision to keep running unsupported software is a risk decision that the NHS made repeatedly.

**Underfunding and underplanning is a security risk.**
The NHS's refusal to modernize its IT infrastructure was consistently linked to budget constraints. An incident response plan that has never been tested is not a plan. Cybersecurity investment is inherent to patient safety and should be treated as any other emergency. WannaCry has made that impossible to ignore.

**Cybersecurity is a duty of care, not a discretionary expense.**
Organizations holding personal data or providing critical services have a legal and ethical obligation to the people depending on them. The UK's Data Protection Act, GDPR, and NIS Regulations all rest on this principle that security is not a nice-to-have, it is the standard of care expected of any organization entrusted with sensitive information. WannaCry exposed a failure of that duty and future incidents should be measured against the same standard.

---

## Aftermath: Post-2017 Pattern Analysis

In the months following WannaCry the UK government announced additional funding, rolled out the Data Security and Protection Toolkit, and made public commitments to modernize NHS cybersecurity. The political narrative was "lessons learned."

However, the record since then tells a different story.

- **2018** — National Audit Office follow-up found NHS trusts still failing basic cyber hygiene assessments. Many had not implemented the recommendations from the original post-WannaCry review.
- **August 2022** — Software supplier Advanced was hit by LockBit 3.0 ransomware taking down NHS 111, out-of-hours GP systems, and patient management platforms for weeks. The ICO's investigation found the access came through a third party customer account that did not have multi-factor authentication enabled. The ICO fined Advanced £3.07 million in 2025.
- **June 2023** — Barts Health NHS Trust, the largest trust in the NHS, was breached by the ALPHV/BlackCat ransomware group. The attackers claimed to have exfiltrated seven terabytes of data including staff personal information, passports, and driver's licences.
- **June 2024** — The Synnovis attack disrupted pathology services across multiple south east London NHS trusts including King's College Hospital and Guy's and St Thomas'. The Qilin ransomware group demanded a reported $50 million ransom. Over 11,000 outpatient and elective procedure appointments were delayed. A patient death was later formally linked to delays in blood test results caused by the attack. Data belonging to approximately 900,000 individuals was exfiltrated and subsequently published.

Seven years after WannaCry the pattern still holds: inadequate third-party security, insufficient segmentation, underinvestment in defense, and the patients paying the price. The lessons have been named, not internalized.

---

## Sources

- National Audit Office — Investigation: WannaCry Cyber Attack and the NHS, October 2017
- Department of Health and Social Care — Cyber Attack Cost Report
- Wikipedia — WannaCry Ransomware Attack
- Cloudflare — What was the WannaCry Ransomware Attack?
- National Health Executive — WannaCry Cyber Attack Cost the NHS £92m
- npj Digital Medicine — A Retrospective Impact Analysis of the WannaCry Cyberattack on the NHS
- Acronis — The NHS Cyber Attack: How and Why it Happened
- CybCube — Five years of WannaCry: what has changed in ransomware since 2017?, 2022
- Computer Weekly — Advanced faces fine over LockBit attack that crippled NHS 111, August 2024
- HIPAA Journal — Patient Death Linked to Ransomware Attack on Pathology Services Provider, June 2025
- UK Parliament written statement on Synnovis, November 2025
- Bloomberg — BlackCat Hacking Gang Says It Stole Data from UK's Barts Health NHS Trust, June 2023

---
*Analysis based on publicly available post-incident reports including the National Audit Office investigation (October 2017) and the Department of Health and Social Care cost report. This is an independent educational assessment, not an official audit or legal determination.*
