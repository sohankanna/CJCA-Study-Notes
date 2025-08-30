# 12 - Ransomware



**Ransomware** is a type of malicious software (malware) that encrypts a victim's files, making them completely inaccessible. The attackers then demand a ransom payment, usually in cryptocurrency, in exchange for the decryption key.

**Core Idea:** It is the digital equivalent of kidnapping your data and holding it hostage.

### The Art Gallery Analogy
Imagine you own an art gallery.

*   **The Art:** Your valuable and critical data (documents, photos, databases).
*   **The Ransomware Attack:** One night, an intruder breaks in and locks every piece of art inside an impenetrable glass case.
*   **The Ransom Note:** A note is left on the door demanding a large sum of money for the keys to unlock the cases.
*   **The Impact:** Your gallery is completely shut down. You can't show or sell any art until you either pay the ransom or find another way to break the cases.

---

## How a Ransomware Attack Works

A typical ransomware attack follows a clear, multi-stage process.


1.  **Initial Access (Infiltration):** The ransomware needs a way to get onto the victim's network. The most common method is through **phishing emails** containing malicious attachments or links. Other methods include exploiting unpatched software vulnerabilities or weak remote access credentials (like RDP).

2.  **Execution & Encryption:** Once on a system, the ransomware activates. It begins to scan for valuable files (documents, images, databases, backups) and encrypts them using strong cryptographic algorithms, making them unreadable.

3.  **Ransom Demand:** After the encryption is complete, the malware displays a ransom note on the victim's screen. The note explains what has happened and provides instructions on how to pay the ransom, including the amount, the cryptocurrency to use, and often a deadline before the price increases or the data is permanently deleted.

**Important Note:** Paying the ransom is risky. There is **no guarantee** that the attackers will provide a working decryption key. Paying also marks the victim as a willing target for future attacks.

---

## Real-World Impact: WannaCry (2017)

*   **What it Was:** A massive, global ransomware attack that spread rapidly by exploiting a vulnerability in Microsoft Windows known as **EternalBlue**.
*   **How it Spread:** It acted like a "worm," automatically spreading from one unpatched computer to another on the same network without any human interaction.
*   **The Impact:** Infected over 200,000 computers in 150 countries. It famously crippled parts of the UK's National Health Service (NHS), forcing hospitals to cancel surgeries and divert ambulances because they were locked out of patient records.

## The Consequences of a Ransomware Attack

The damage from a ransomware attack extends far beyond the ransom payment itself.

| Impact Area | Description |
| :--- | :--- |
| **Operational Shutdown**| This is often the most immediate and costly impact. Business operations grind to a halt, leading to massive financial losses for every hour of downtime. |
| **Financial Loss**| Includes the ransom payment (if made), the cost of recovery and rebuilding systems, regulatory fines, and lost revenue. |
| **Data Loss**| If backups are also encrypted or unavailable, the data loss can be permanent and catastrophic. |
| **Reputational Damage**| A successful attack erodes customer trust and can permanently damage a company's brand. |
| **Life-Threatening Risks**| In critical sectors like healthcare, ransomware can prevent access to patient records and medical equipment, directly endangering lives. |
