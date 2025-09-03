# Authentication Protocols

## 1. Foundational & Network-Level Authentication

These protocols are fundamental to securing network access and communications.

| Protocol | Description | Security Level |
| :--- | :--- | :--- |
| **Kerberos** | The core authentication protocol in **Microsoft Active Directory** environments. It uses a trusted third party, the **Key Distribution Center (KDC)**, to issue encrypted "tickets" that grant users access to network services without repeatedly sending their passwords. | Very Secure |
| **SSH** | **Secure Shell**. A protocol for secure remote command-line access. It uses strong encryption and can authenticate users via passwords or, more securely, with public/private key pairs. | Very Secure |
| **SSL / TLS** | **Secure Sockets Layer / Transport Layer Security**. Cryptographic protocols that provide security for communications over a network. **TLS** is the modern successor to the deprecated SSL. It's the "S" in **HTTPS**. | Very Secure |
| **PAP** | **Password Authentication Protocol**. An extremely simple protocol that sends the username and password in **cleartext**. | **Highly Insecure** |
| **CHAP** | **Challenge-Handshake Authentication Protocol**. A more secure alternative to PAP. It uses a three-way handshake and a shared secret to verify identity without sending the actual password over the network. | Moderately Secure |

## 2. Web & Federated Authentication

These protocols and standards are used to manage identity and access across multiple web applications and services.

| Acronym | Full Name | Description |
| :--- | :--- | :--- |
| **SSO** | **Single Sign-On** | A concept and method that allows a user to log in once with a single set of credentials and gain access to multiple, independent applications without needing to re-authenticate. |
| **SAML** | **Security Assertion Markup Language**| An open standard that enables SSO. It allows an **Identity Provider (IdP)** to securely pass authentication and authorization credentials ("assertions") to a **Service Provider (SP)**. |
| **OAuth** | Open Authorization | An open standard for **authorization**, not authentication. It allows a user to grant a third-party application limited access to their resources on another service *without* sharing their password (e.g., letting a new app "access your Google contacts"). |
| **OpenID**| OpenID Connect (OIDC)| An open standard for **authentication** built on top of OAuth 2.0. It allows a user to use a single identity (like their Google or Facebook account) to log in to multiple third-party websites. |

## 3. Wireless & Access Control Frameworks

These are specifically designed for authenticating users and devices onto networks, particularly wireless ones.

| Acronym | Full Name | Description |
| :--- | :--- | :--- |
| **EAP** | **Extensible Authentication Protocol**| A flexible **framework**, not a single protocol. It provides a standardized way to transport different authentication methods (called EAP methods) over a network. It's the foundation for modern network access control. |
| **LEAP** | **Lightweight EAP**| A Cisco-proprietary, early EAP method. It is now considered **insecure** due to vulnerabilities and has been largely replaced. |
| **PEAP** | **Protected EAP**| A more secure EAP method. It creates an encrypted TLS tunnel between the client and the authentication server first, and then sends the user's credentials (like a password) through this secure tunnel. |

## 4. Multi-Factor Authentication (MFA)

MFA enhances security by requiring a user to provide two or more different types of evidence to prove their identity.

| Acronym | Full Name | Description |
| :--- | :--- | :--- |
| **2FA** | **Two-Factor Authentication**| The most common form of MFA, requiring two distinct factors. |
| **MFA** | **Multi-Factor Authentication**| The broader term, requiring two or more factors. The factors are categorized as: <br> 1. **Something you know** (a password, a PIN). <br> 2. **Something you have** (a phone for an OTP, a hardware token). <br> 3. **Something you are** (biometrics like a fingerprint or face scan). |
| **FIDO** | **Fast IDentity Online**| An open standard for passwordless authentication. It aims to replace passwords with more secure and user-friendly methods, such as using biometrics on a device or a physical security key (like a YubiKey). |

## 5. Public Key Infrastructure (PKI)

| Acronym | Full Name | Description |
| :--- | :--- | :--- |
| **PKI** | **Public Key Infrastructure**| A system of hardware, software, policies, and procedures used to create, manage, distribute, and revoke **digital certificates**. PKI is the foundation of trust for technologies like HTTPS (SSL/TLS), where a server's digital certificate proves its identity to your browser. |
