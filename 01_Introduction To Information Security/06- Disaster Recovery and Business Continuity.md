# 06- Disaster Recovery and Business Continuity


Disaster Recovery (DR) and Business Continuity (BC) are related but distinct concepts that ensure an organization's resilience against major disruptions like natural disasters, power outages, or severe cyberattacks.

### The Concert Analogy
Imagine you are hosting a large outdoor concert.

*   **Disaster Recovery (DR) is your technical, on-the-spot fix.**
    *   **The Problem:** The power suddenly goes out.
    *   **The DR Plan:** You immediately switch on the backup generator to get the lights and sound back on.
    *   **Focus:** Restoring critical *technical systems* as quickly as possible.

*   **Business Continuity (BC) is your overall strategic plan.**
    *   **The Problem:** The weather forecast predicts a severe thunderstorm for the entire day of the concert.
    *   **The BC Plan:** You activate your contingency plan to move the entire concert to a pre-arranged indoor venue.
    *   **Focus:** Keeping the entire *business operation* running, even in a degraded state.

**Key Takeaway:** DR is a *component* of BC. You need a DR plan (get the generator running) to achieve your BC goal (the show must go on).

---

## Core Concepts and Terminology

| Concept | Description |
| :--- | :--- |
| **Business Continuity (BC)** | The holistic strategy and plan that ensures essential business functions can continue during and after a disaster. It answers the question: "How do we keep the business running?" |
| **Disaster Recovery (DR)** | The specific, technical subset of BC that focuses on restoring IT infrastructure, systems, and data after an incident. It answers the question: "How do we get our technology back online?" |
| **Recovery Time Objective (RTO)** | The **maximum acceptable downtime** for a system after a disaster. How long can we afford for this system to be offline? (e.g., "The payment processing system must be back online within 1 hour"). |
| **Recovery Point Objective (RPO)** | The **maximum acceptable amount of data loss**, measured in time. How much data can we afford to lose? (e.g., "We can lose up to 15 minutes of transaction data, so we need backups every 15 minutes"). |

---

## Responsibility and Testing

### Who is Responsible?
*   **Strategy & Management:**
    *   A **Business Continuity Manager** or a dedicated team is typically responsible for creating, managing, and updating the DR/BC plans.
    *   This team works closely with **executive leadership** (to align with business goals) and **IT** (for technical implementation).

### How are Plans Tested?
DR/BC plans are useless unless they are regularly tested and refined.

*   **Tabletop Exercises:** Team members gather in a conference room and talk through a simulated disaster scenario, step-by-step, to identify gaps in the plan.
*   **Full-Scale Simulations:** A more intensive test where the organization actually performs a failover to its backup systems or recovery site. This provides a real-world test of the plan's effectiveness.
*   **Role of Penetration Testers:** Pen testers can be brought in to test the security of backup systems or recovery sites, ensuring that the disaster recovery environment itself isn't vulnerable to attack.

**Key Takeaway:** Regular testing (often annually) is crucial to ensure that plans are up-to-date and that employees know their roles during a real crisis.
