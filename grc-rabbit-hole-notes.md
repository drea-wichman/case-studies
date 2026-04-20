# GRC Rabbit Hole Notes

Ongoing notes on governance, risk, and compliance topics I chase down for fun. Entries are driven by whatever I'm curious about, reading, or watching in the news, not a set curriculum. Coming from zero and forming opinions as I go.

Each entry is dated. Content reflects my understanding at the time of writing and may go out of date as laws, cases, or policies evolve.

---

## Mutual Legal Assistance Treaties (MLATs)
*Added: March 5 2026*

**Real-world example:**
US law enforcement used the MLAT with Switzerland to make Swiss-based Proton Mail hand over account metadata (credit card number) for a criminal investigation. Proton complied because they are legally required to follow Swiss court orders. Important distinction people are missing: Proton's end-to-end encryption meant they could not hand over email content or file contents (which they should not have access to anyway), only metadata which to my knowledge can't be encrypted, only hidden like in onion routing. Despite backlash, the Proton critique is moot because their job is to encrypt CONTENT. Account creation and payment info are not content. The user's OPSEC failure was using a personal credit card and public IP without a VPN which made them traceable.

**What is an MLAT:**
An agreement between two or more countries that allows them to request and share evidence and information for criminal investigations.

**What can be requested:**
- Witness testimony and statements
- Documents, records, and evidence
- Search and seizure execution
- Locating or identifying people

**Key points:**
- Only available to government officials, usually prosecuters - not private citizens or civil cases
- Requests must go through formal legal processes and be approved by a court in receiving country
- The US has MLATs with 65+ countries including Switzerland, the UK, and all EU member states for starters

**Why it matters for GRC:**
Organizations operating internationally need to understand that legal obligations cross borders. Privacy tools protect content, but metadata and account information can still be captured legally. Compliance teams should consider how MLATs affect who can legally access data and where.

**Sources:**
- [404 Media - Proton Mail Helped FBI Unmask Anonymous 'Stop Cop City' Protester](https://www.404media.co/proton-mail-helped-fbi-unmask-anonymous-stop-cop-city-protestor/)
- [TechCrunch - ProtonMail logged IP address of French activist after order by Swiss authorities](https://techcrunch.com/2021/09/06/protonmail-logged-ip-address-of-french-activist-after-order-by-swiss-authorities/)
- [Proton - Important clarifications regarding arrest of climate activist](https://proton.me/blog/climate-activist-arrest)
- [Proton - Transparency Report](https://proton.me/legal/transparency)

---

## Encryption vs. Metadata
*Added: March 5 2026*

**Real-world (rabbit hole) examples:**
- 2021: Proton handed over IP address and browser fingerprint of a climate activist to Swiss police when requested through Europol. User didn't use a VPN though.
- 2024: Proton handed over a recovery email which was an iCloud email address (metadata and not required by Proton) of a person to Spanish police. Apple then provided full name, home addresses, and linked Gmail.

**So what IS encrypted? Content:**
- Email text and attachments
- Files stored in encrypted drives
- Calendars, notes, etc.
- End to end meaning even the provider can't read it

**What's NOT encrypted? Metadata:**
- IP addresses used to log in
- Account creation date
- Recovery email addresses
- Payment method used
- Email timestamps and recipient addresses(!)
- Device/browser fingerprint (isn't unique 1/1 but can narrow down a search)

**Why it matters for GRC:**
It seems people assume that "encrypted" means invisible. Encryption protects content which really is resting data and data in transit, not the fact that you exist as a user who accessed a service. Metadata alone can be enough to identify somebody. Metadata protection is our responsibility as a user through VPN, anonmyous payment, no recovery acct, etc. If you have shit OPSEC it doesn't matter what company you use, your privacy will never be protected.

**Sources:**
- [TechCrunch - ProtonMail logged IP address of French activist after order by Swiss authorities](https://techcrunch.com/2021/09/06/protonmail-logged-ip-address-of-french-activist-after-order-by-swiss-authorities/)
- [The Register - ProtonMail deletes 'we don't log your IP' boast from website](https://www.theregister.com/2021/09/07/protonmail_hands_user_ip_address_police/)
- [CyberInsider - Proton Mail payment data helped FBI identify 'Stop Cop City' account holder](https://cyberinsider.com/proton-mail-payment-data-helped-fbi-identify-stop-cop-city-account-holder/)
- [Proton - Transparency Report](https://proton.me/legal/transparency)

---

## Swiss Surveillance Law (VÜPF)
*Added: March 5 2026*

**Real-world example**
Switzerland built its reputation as a kind of privacy refuge. Swiss law historically categorized VPN providers differently from telecom providers so VPNs had no logging obligations which is why companies like Proton based themselves there.

**What's changing:**
Switzerland is proposing a revision to the VÜPF that would begin in late 2026:
- Require VPN and email providers to log IP addresses for 6 months
- Mandate user ID verification (official ID or phone number)
- Wants to create backdoor to decrypt data

**Why it matters:**
- Seems this would make Swiss surveillance stricter than the US or EU because it doesn't affect US-based Gmail or WhatsApp for example

**Proton's response:**
- Started moving physical infrastructure to Germany and Norway (EU courts have ruled blanket data retention illegal)
- Proton has already moved new-ish Lumo AI chatbot which is hosted Germany
- Headquarters remain in Geneva, not complete relocation
- CEO Andy Yen said "If necessary, we can shut down the systems in Switzerland within a short period of time"

**Why it matters for GRC:**
A country's privacy laws today don't guarantee its privacy laws tomorrow. Organizations must monitor these changes constantly and have contingency plans.

**Sources:**
- [TechRadar - Is Proton leaving Switzerland?](https://www.techradar.com/vpn/vpn-privacy-security/is-proton-leaving-switzerland-legal-uncertainty-of-proposed-surveillance-laws-is-pushing-them-to-make-several-changes)
- [Heise - Surveillance: Proton relocates parts of its infrastructure from Switzerland](https://www.heise.de/en/news/Surveillance-Proton-relocates-parts-of-its-infrastructure-from-Switzerland-10538664.html)
- [Tuta - Switzerland plans surveillance worse than US](https://tuta.com/blog/switzerland-surveillance-plan)
- [DoVPN - Switzerland's new VPN surveillance plan](https://dovpn.com/swiss-vpn-surveillance-protonvpn-privadovpn/)

---

## Section 702 FISA
*Added: April 19, 2026*

**Real-world example:**
Section 702 was supposed to expire April 20, 2026 unless Congress reauthorizes it. As of tonight, the fight is live. The Trump administration pushed for a clean 18-month reauthorization with no changes. House blocked amendments that would have required warrants for searching Americans' data. On April 17, two back-to-back votes failed. Those were 1: a five-year package with modest reforms which collapsed when roughly a dozen Republicans rejected it and 2: the procedural vote for the clean 18 month extension failed 197-228, with 20 Republicans defying Trump and 4 Dems also voting no. Around 2am the House passed a 10 day stopgap, pushing the deadline to April 30. DNI Tulsi Gabbard, who previously opposed 702 as a congresswoman and co-sponsored legislation to repeal it, reversed position again saying warrants should be required for US person queries which goes against Trump. The reform coalition cuts across both parties (Freedom Caucus Republicans plus progressive Democrats). The coalition protecting 702 also spans across both parties. Outcome unclear.

**What is Section 702:**
A surveillance authority passed in 2008 as part of the FISA Amendments Act. It allows the US government to collect emails, phone calls, and text messages of non-US persons located outside of the US without a warrant. Targets are selected by intelligence analysts, not courts. The Attorney General and DNI issue annual "certifications" (very broad/bulk request like "We want to spy on foreign cyber threats") that the FISA court reviews and generally approves. The FISA court does not approve individual targets. Any American who communicates with a foreign target can have their communications swept into the 702 database as "incidental collection."

**The loophole:**
Once Americans' communications are in the 702 database, the FBI can search them for US person information without a warrant. These are called "US person queries" or backdoor searches. The FISA Court found in 2022 that "compliance problems with the FBI's querying of Section 702 information have proven to be persistent and widespread." From 2020 to 2021 alone, the FBI conducted 278,000 noncompliant searches that the DOJ determined violated FBI standards. Documented abuses include searches targeting Black Lives Matter protesters, January 6 participants, a congressional campaign's 19,000 donors, a US Senator, a state senator, and a state judge. A 2024 federal court ruling held that these backdoor searches are unconstitutional and ordinarily require a warrant. Congress has reauthorized 702 multiple times despite the abuses.

**Why it matters for GRC:**
Section 702 is why US cloud services struggle with EU data protection compliance. The EU's Schrems II ruling in 2020 found that US surveillance law, specifically 702, gives US intelligence agencies too much access to European data which violates GDPR. Any organization handling EU citizen data through US based infrastructure is exposed to this. GRC teams at multinational companies spend significant time managing this tension. For US companies specifically, 702 shapes what, if any privacy assurances can legally be made to customers, because no contractual clause overrides surveillance authority like 702. The live reauthorization fight also illustrates how surveillance law actually changes in practice: not through clean reform but through coalition fights, sunset clauses, and last minute procedural maneuvers.

**Sources:**
- [The Hill - GOP rebels block FISA Section 702 spy powers deal](https://thehill.com/homenews/house/5835879-fisa-702-spy-powers-vote/)
- [NPR - Congress extends controversial surveillance powers for 10 days](https://www.npr.org/2026/04/17/nx-s1-5788573/house-extends-surveillance-powers-for-10-days)
- [Brennan Center - Section 702 of the Foreign Intelligence Surveillance Act](https://www.brennancenter.org/our-work/research-reports/section-702-foreign-intelligence-surveillance-act)
- [Wikipedia - FBI Section 702 query violations](https://en.wikipedia.org/wiki/FBI_Section_702_query_violations)
- [EFF - Federal Court Rules Backdoor Searches of 702 Data Unconstitutional](https://www.eff.org/deeplinks/2025/01/victory-federal-court-finally-rules-backdoor-searches-702-data-unconstitutional)
- [ABC News - Tulsi Gabbard shifts stance on key surveillance tool](https://abcnews.go.com/Politics/tulsi-gabbard-shifts-stance-key-surveillance-tool-previously/story?id=117587144)

---

## The Wyden Letter
*Added: April 19, 2026*

**Real-world example:**
On March 26, 2026 six Democratic lawmakers: Senators Ron Wyden, Alex Padilla, Ed Markey, and Elizabeth Warren, plus Rep. Sara Jacobs and Rep. Pramila Jayapal sent a formal letter to Director of National Intelligence Tulsi Gabbard. The letter asks her to publicly clarify whether Americans who use commercial VPN services are being treated as foreigners for surveillance purposes and so losing their protections under the Fourth Amendment. As of now, Gabbard has not responded. The timing was intentional as the letter was sent while Congress is actively debating Section 702 reauthorization which forces the VPN question into the fight.

**The core question:**
VPNs route internet traffic through servers in other locations to hide a user's real location. That is the point. But under Section 702 the government can obtain foreign communications without a warrant. If an American's traffic exits through a VPN server in Amsterdam, does the intelligence community treat that traffic as Dutch/foreign/okay to collect without a warrant? The lawmakers are asking Gabbard to say publicly whether this is happening or not. If yes, it means a privacy tool is actually stripping Americans of their Fourth Amendment rights. If no, Gabbard should say so on the record. Her refusal to answer is an answer in itself.

**Why it matters for GRC:**
The letter exposes the gap between what privacy tools are marketed/aim to do and how they are manipulated and misused under the law. GRC teams advising on data handling need to understand that where infrastructure is physically located matters for compliance, not just for marketing. A VPN being "privacy-focused" does not automatically mean stronger legal protection for users and in some cases may mean the opposite. For organizations with employees or clients using commercial VPNs, the categorization question affects what laws actually apply to their communications. The letter is also a good example of how Congress actually forces answers from the executive branch: put the question in writing, make it public, time it to a vote.

**Sources:**
- [Nextgov - Lawmakers question VPN impact on Americans' FISA surveillance protections](https://www.nextgov.com/cybersecurity/2026/03/lawmakers-question-vpn-impact-americans-fisa-surveillance-protections/412437/)
- [Android Authority - Do US-based VPN users risk being treated as foreign surveillance targets?](https://www.androidauthority.com/using-vpn-could-allow-us-government-surveillance-3652311/)
- [The Meridiem - VPN Privacy Inflection as Overseas Routing May Trigger NSA Surveillance](https://themeridiem.com/tech-policy-regulation/2026/03/26/vpn-privacy-inflection-as-overseas-routing-may-trigger-nsa-surveillance)

---

## Executive Order 12333
*Added: April 19, 2026*

**Real-world example:**
In 2013, documents leaked by Edward Snowden revealed the MUSCULAR program. The NSA and its UK counterpart GCHQ tapped into the private underwater(!) fiber-optic links that connected Google's and Yahoo's data centers around the world. Before your email left Google's network to travel the public internet, it was encrypted. After it left, it was encrypted. But between Google's own data centers, on Google's own private cables, it was not encrypted because Google assumed that network was theirs. The NSA tapped those cables and collected hundreds of millions of records a day. Because the collection was happening outside of the US targeting non-US infrastructure, it required zero warrants, no FISA court approval, and no Section 702 certification. It was done legally under the authority of Executive Order 12333. An actual NSA slide describing the location of the tap had a smiley face drawn on it.

**What Executive Order 12333 is:**
This is an executive order (issued directly by the President without Congress voting on it) by President Reagan on December 4, 1981. It is the foundational authority governing how US intelligence conducts surveillance outside the US against non-US persons. It covers the CIA, NSA, DIA, and the intelligence arms of other agencies when they operate abroad. It came decades before FISA Section 702 (2008) and the Patriot Act (2001) but is still in effect today.

**Why "executive order" matters:**
Section 702, as flawed as it is, does at least have some oversight. Congressional committees, sunset clauses, FISA court review, public debate, etc. EO 12333 has almost none of that. It cannot be modified by Congress because it is an executive order. It has no sunset clause so it never expires and never provides a reauthorization conversation. It is not subject to FISA court review because the FISA court only covers FISA. The intelligence community interprets EO 12333 internally, with the rules for what to do when Americans' data gets swept up set by the agencies themselves. Most of what is done under it is classified. The public has almost no visibility into the largest category of US surveillance.

**Legislation from a different time:**
1981 was before the commercial internet, even before cellphones, before cloud computing, before undersea fiber-optic cables carried the majority of global communications, before Google existed, before email was common, before anyone imagined that a person in Illinois would have their private emails routed through servers in Ireland and back through London. EO 12333 was written for a world of embassies, foreign agents, and cold war intelligence yet is being applied to a world where the physical infrastructure of citizen communications happens to pass through foreign jurisdictions by default. The law has not caught up wiht the world that exists today. The permissions have not been adjusted...the surveillance has just expanded to fill the technology as it was built.

**Why it matters for GRC:**
Most corporate data flows through foreign infrastructure at some point. Overseas offices, international customers, cloud providers with centers/servers abroad, and routine traffic that crosses borders invisibly. All of this is potentially exposed to EO 12333 collection and that exposure cannot be contracted around by any "privacy focused" company or service. For GRC teams negotiating with EU customers, EO 12333 is part of why Schrems II was decided the way it was: US surveillance law including the parts that the US government would prefer not to discuss gives intelligence agencies access that violates GDPR standards. Understanding EO 12333 matters for honest risk assessments. You cannot tell a customer their data is protected from US government access if it passes through infrastructure the US government can legally tap at any time for any amount of time without a warrant.

**Sources:**
- [Washington Post - How we know the NSA had access to internal Google and Yahoo cloud data](https://www.washingtonpost.com/world/national-security/how-we-know-the-nsa-had-access-to-internal-google-and-yahoo-cloud-data/2013/11/04/b4e4b2f2-456d-11e3-b6f8-3782ff6cb769_story.html)
- [EFF - EO 12333: End Mass Surveillance Under Executive Order 12333](https://www.eff.org/deeplinks/2014/01/eo-12333-end-mass-surveillance-under-executive-order-12333)
- [ACLU - Executive Order 12333: Unchecked Surveillance of Americans](https://www.aclu.org/report/executive-order-12333-unchecked-surveillance-americans)
- [ODNI - Executive Order 12333 (official text)](https://www.dni.gov/index.php/ic-legal-reference-book/executive-order-12333)
- [Brennan Center - What the Government Does with Americans' Data](https://www.brennancenter.org/our-work/research-reports/what-government-does-americans-data)
