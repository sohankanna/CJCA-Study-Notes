# 15 - Physical Security Testing

## 1. The Goal of a Physical Pentest

The primary objective is to identify and exploit weaknesses in the physical security layers that protect an organization's most critical assets—its people, data, and infrastructure. It answers the question: "Can an unauthorized person get into our building and access sensitive areas?"

---

## 2. Key Components of a Physical Security Assessment

A physical pentest evaluates multiple layers of defense.

### a) Perimeter Security
*   **What it is:** The outermost layer of defense.
*   **Targets:** Fences, gates, walls, lighting, and landscaping.
*   **Assessment:** Looking for weaknesses like gaps in fences, poorly lit areas that provide cover, or climbable structures.

### b) Access Control Systems
*   **What it is:** The mechanisms that control entry into the building and restricted areas.
*   **Targets:** Key card systems, biometric readers, PIN pads, and traditional locks.
*   **Assessment:** Attempting to bypass these controls through techniques like **badge cloning** (copying an RFID card), lock picking, or simply checking for propped-open or unsecured doors.

### c) Surveillance and Monitoring
*   **What it is:** The systems used to detect and observe activity.
*   **Targets:** Security cameras, motion sensors, and intrusion detection alarms.
*   **Assessment:** Identifying camera blind spots, testing the response to triggered alarms, and determining if surveillance is actively monitored.

### d) Human Element
*   **What it is:** The people responsible for enforcing security policies. This is often the weakest link.
*   **Targets:** Security guards, receptionists, and general employees.
*   **Assessment:** Using **social engineering** to test security awareness and adherence to procedures.

---

## 3. The Physical Pentest Methodology

### 1. Information Gathering (OSINT)
The test begins with **passive reconnaissance**.
*   **Activities:** Studying satellite imagery (Google Maps) to map the facility layout, reviewing social media for employee information and photos of badges, and analyzing public documents to understand the organization's structure.

### 2. On-Site Observation
Testers conduct surveillance of the target facility.
*   **Activities:** Observing employee entry/exit patterns, identifying main entrances and less-trafficked side doors, noting security guard patrol routes and shift changes, and looking for common "smoker's doors" that are often left unsecured.

### 3. Exploitation (The Breach Attempt)
With proper authorization, testers attempt to bypass security controls.
*   **Common Techniques:**
    *   **Tailgating / Piggybacking:** The most common and effective technique. The tester, often carrying boxes or looking busy, simply follows an authorized employee through a secure door before it closes.
    *   **Social Engineering:** Posing as a delivery driver, IT support, or a new employee to trick staff into granting access.
    *   **Technical Bypasses:** Using specialized tools to pick locks or clone RFID access cards.

---

## 4. Legal and Ethical Considerations

Physical penetration testing carries significant legal and personal risk. **It is illegal and dangerous without explicit, written authorization.**

*   **The "Get Out of Jail Free" Letter:** This is a **mandatory** document that every tester must carry on their person during a physical engagement. It is a formal letter from the client organization that:
    *   Explicitly authorizes the testing activities.
    *   Defines the scope and approved timeframes.
    *   Provides emergency contact information for both the client and the testing firm.
*   **Do No Harm:** The primary principle. The tester's actions must not cause any real damage to property or pose a risk to people.
*   **Privacy:** The tester must respect the privacy of individuals and handle any sensitive information discovered with the utmost confidentiality.
