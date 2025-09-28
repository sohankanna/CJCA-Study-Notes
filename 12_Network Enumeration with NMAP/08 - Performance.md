# 08 - Performance


## 1. The Speed vs. Accuracy Trade-Off

The core concept of Nmap performance tuning is balancing speed with accuracy and stealth.

*   **Faster Scans:** Can finish large network scans more quickly.
*   **The Risk:** Sending packets too fast or not waiting long enough for a reply can cause Nmap to **miss live hosts or open ports**. This happens because either the target host or an intermediary device (like a firewall) may drop packets under a heavy load, or a slow network connection may delay the reply beyond Nmap's timeout window.

---

## 2. Manual Performance Tuning

Nmap provides granular control over its scanning engine, allowing you to manually tune its performance.

| Option | Description | Impact |
| :--- | :--- | :--- |
| **`--max-retries <number>`** | Sets the maximum number of times Nmap will retransmit a probe to a port that has not responded. The default is 10. | Setting this to a low number (e.g., `0` or `1`) will significantly speed up a scan against a network with many filtered ports but dramatically increases the risk of missing open ports that are on a slow or lossy network. |
| **`--initial-rtt-timeout <time>`** <br> **`--max-rtt-timeout <time>`** | Sets the initial and maximum **Round-Trip-Time (RTT)** timeout. This is how long Nmap will wait for a response to a probe. | Setting these values too low on a slow or high-latency network is a primary cause of inaccurate scans, as Nmap will give up waiting for a reply before it has a chance to arrive. |
| **`--min-rate <number>`** | Tells Nmap to send packets at a rate of at least `<number>` packets per second. | Very effective for speeding up scans on fast, reliable networks where you have been whitelisted. Can easily overwhelm slower networks or trigger an IDS/IPS. |

**Key Takeaway:** Manual tuning is powerful but requires a good understanding of the target network's condition. For most scenarios, using Nmap's built-in timing templates is a better and safer approach.

---

## 3. Timing Templates (`-T`)

Nmap provides six timing templates that offer pre-configured sets of performance options, making it easy to adjust the scan's aggressiveness without needing to manually set dozens of individual flags.

*   **Syntax:** `nmap -T<0-5> <target>`

| Template #| Name | Description & Use Case |
| :--- | :--- | :--- |
| **`-T0`** | `paranoid` | **Extremely slow.** Used for IDS evasion. Sends packets very infrequently to avoid detection. Can take hours or days. |
| **`-T1`** | `sneaky` | **Very slow.** Also used for IDS evasion, slightly faster than `paranoid`. |
| **`-T2`** | `polite` | **Slow.** Uses less bandwidth and fewer resources. Good for scanning on unreliable networks without causing congestion. |
| **`-T3`** | **`normal`** | **The default.** Nmap's standard timing, which provides a good balance between speed and accuracy. |
| **`-T4`** | **`aggressive
