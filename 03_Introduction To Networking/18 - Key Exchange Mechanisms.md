# Key Exchange Mechanisms

## The Core Problem: Securely Sharing a Secret
Imagine two people who have never met need to start a private conversation over a public channel (like the internet) where anyone could be listening. How can they create a secret key to encrypt their messages without an eavesdropper also learning the key? Key exchange algorithms solve this problem.

---

## 1. Classical Key Exchange Algorithms

### Diffie-Hellman (DH)
*   **What it is:** The original and one of the most common key exchange algorithms.
*   **How it Works (Analogy):** It's like a **paint mixing scheme**.
    1.  Alice and Bob publicly agree on a common paint color (a public base number).
    2.  Alice secretly chooses her own private color and mixes it with the common color.
    3.  Bob secretly chooses his own private color and mixes it with the common color.
    4.  They exchange their mixed paints publicly.
    5.  Alice takes Bob's mix and adds her own secret color.
    6.  Bob takes Alice's mix and adds his own secret color.
    7.  Both now have the **exact same final color**, but an eavesdropper who only saw the public colors and the mixed colors cannot easily figure out the final secret color.
*   **Limitation:** Vulnerable to a **Man-in-the-Middle (MITM)** attack if not used with an authentication mechanism (like digital signatures).

### Rivest–Shamir–Adleman (RSA)
*   **What it is:** An **asymmetric** cryptographic algorithm widely used for both key exchange and digital signatures.
*   **How it Works for Key Exchange:**
    1.  The server has a **public key** (which it shares with everyone) and a **private key** (which it keeps secret).
    2.  The client generates a temporary, random secret key.
    3.  The client encrypts this secret key using the server's **public key**.
    4.  The client sends the encrypted secret to the server.
    5.  Only the server, with its corresponding **private key**, can decrypt the message and retrieve the secret key.
    6.  Both parties now share the same secret key.
*   **Strength:** Very secure but more computationally intensive (slower) than DH.

---

## 2. Modern Elliptic Curve Cryptography (ECC)

Elliptic Curve Cryptography is a more modern approach that provides the same level of security as classical algorithms but with much **smaller key sizes**, making it faster and more efficient.

### Elliptic Curve Diffie-Hellman (ECDH)
*   **What it is:** A variant of the Diffie-Hellman algorithm that uses the mathematics of elliptic curves.
*   **Advantage:** Provides the same security as DH but is much more computationally efficient, making it ideal for mobile and low-power devices. It is a core component of modern **TLS** for providing **forward secrecy**.

### Elliptic Curve Digital Signature Algorithm (ECDSA)
*   **What it is:** An algorithm used to create **digital signatures** using elliptic curve cryptography.
*   **Purpose:** Provides **authentication** and **integrity**. It is used to prove that a message came from a specific sender and has not been altered. It can be used alongside a key exchange like ECDH to prevent MITM attacks.

---

## 3. Internet Key Exchange (IKE)

**IKE** is a protocol, not a single algorithm. It is a framework used to set up a secure, authenticated communication channel, primarily for **IPsec VPNs**.

*   **Core Function:** IKE automates the negotiation of security parameters and the secure exchange of keys between two VPN endpoints. It combines other cryptographic techniques (like DH and RSA) to achieve this.
*   **Operating Port:** UDP Port 500.

### IKE Modes of Operation

| Mode | Description | Security Trade-off |
| :--- | :--- | :--- |
| **Main Mode** | The default and **more secure** mode. It uses a three-phase, six-message exchange to negotiate parameters. It protects the identities of the communicating parties. | Slower due to more message exchanges. |
| **Aggressive Mode**| A faster, alternative mode. It uses a two-phase, three-message exchange. All parameters are exchanged in the first phase. | **Less secure** because it exposes the identities of the parties in cleartext during the negotiation, making it more vulnerable to sniffing. |

### Pre-Shared Keys (PSK) in IKE
*   **What it is:** A "password" or secret string that is shared between the two VPN endpoints *before* the IKE process begins (out-of-band).
*   **Purpose:** Used as an initial authentication method to prove the identity of the two parties. If the PSKs match, the IKE negotiation can proceed.
*   **Limitation:** If the PSK is weak or compromised, the entire security of the VPN session is at risk.
