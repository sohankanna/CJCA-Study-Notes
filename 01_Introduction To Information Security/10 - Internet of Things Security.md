# 10 - Internet of Things Security

The Internet of Things (IoT) refers to the global network of physical devices—from smart home gadgets and wearable fitness trackers to industrial sensors and connected cars—that are embedded with sensors, software, and other technologies to connect and exchange data over the internet.

### The Smart Home Analogy
Imagine your home is full of smart devices (thermostat, lights, refrigerator, door lock).

*   **The Convenience:** You can control your entire home from your smartphone, making life easier.
*   **The Risk:** Each smart device is a potential *digital doorway* into your home network.
*   **IoT Security:** The practice of adding strong locks, alarms, and safeguards to these digital doorways to prevent digital intruders from gaining access to your network and personal data.

---

## Unique Challenges of IoT Security

Securing IoT devices is uniquely difficult compared to traditional computers for several reasons.

| Challenge | Description |
| :--- | :--- |
| **Limited Resources** | Many IoT devices have minimal processing power, memory, and battery life, making it difficult to run complex security software like antivirus or encryption without impacting performance. |
| **Lack of Updates / Patching** | Devices are often "set and forget." Manufacturers may not provide security updates, or users may not know how to apply them, leaving known vulnerabilities unpatched for years. |
| **Weak & Default Passwords** | A massive number of IoT devices ship with simple, default credentials (like `admin`/`admin`) that users never change, making them incredibly easy for attackers to compromise. |
| **Large Attack Surface** | A single home or business can have dozens or hundreds of IoT devices, dramatically increasing the number of potential entry points for an attacker. |
| **Physical Accessibility** | Many IoT devices (like security cameras or sensors) are physically located in insecure, public areas, making them vulnerable to physical tampering. |


---

## Real-World Impact: The Mirai Botnet

One of the most famous examples of IoT insecurity is the **Mirai Botnet**.
*   **How it Worked:** The malware continuously scanned the internet for IoT devices (like cameras and routers) that were still using their factory-default usernames and passwords.
*   **What it Did:** It infected hundreds of thousands of these insecure devices, turning them into a massive "zombie army" or botnet.
*   **The Impact:** The attackers used this botnet to launch some of the largest **Distributed Denial of Service (DDoS)** attacks ever seen, taking down major websites and services.

---

## Responsibility for IoT Security

IoT security is a shared responsibility that spans the entire lifecycle of a device.

| Player | Responsibility | Analogy |
| :--- | :--- | :--- |
| **Device Manufacturers** | The **most critical** role. They are responsible for building security into the device from the start (**Security by Design**), such as forcing a password change on first use and providing a mechanism for security updates. | The architect and builder of a house. |
| **Network Administrators** | Responsible for securing the network that the IoT devices connect to. This includes practices like **network segmentation**, which isolates IoT devices onto their own separate network so that if one is compromised, it can't access more sensitive systems (like corporate servers). | The guards patrolling the castle walls. |
| **Application Developers** | Responsible for securing the mobile and web applications used to control the IoT devices, ensuring strong authentication and encrypted communication. | The scribes and scholars who write the laws. |
| **End Users (Consumers/Employees)** | Responsible for practicing good security hygiene: changing default passwords, enabling security features, and installing updates when available. | The homeowner who must remember to lock the doors. |
