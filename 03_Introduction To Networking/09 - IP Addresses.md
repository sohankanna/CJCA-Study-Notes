# IP Addresses
## Why Subnet?

Creating subnets allows a network administrator to:
*   **Improve Security:** By segmenting a network, you can create isolated zones. For example, you can place all servers on one subnet and all workstations on another, then use a firewall to strictly control the traffic that can pass between them.
*   **Improve Performance:** Reduces network broadcast traffic. Broadcast messages are only sent to devices within the same subnet, which reduces congestion and improves overall network efficiency.
*   **Simplify Management:** Organizes a large network into smaller, more manageable parts.

---

## The Core Concept: Borrowing Bits

Subnetting works by "borrowing" bits from the **host portion** of an IP address and reassigning them to the **network portion**. This is done by extending the subnet mask.

*   Every bit you borrow for the network doubles the number of subnets you can create.
*   Every bit you borrow for the network halves the number of available host addresses within each new subnet.

---

## Calculating a Subnet: A Practical Example

Let's break down a given network and find all its properties.

**Given:**
*   **IP Address:** `192.168.12.160`
*   **Subnet Mask:** `255.255.255.192`
*   **CIDR Notation:** `/26`

### Step 1: Analyze the Subnet Mask
The CIDR `/26` tells us that the first **26 bits** of the address are the **network part**, and the remaining bits (32 - 26 = **6 bits**) are the **host part**.

| Details | 1st Octet | 2nd Octet | 3rd Octet | 4th Octet |
| :--- | :--- | :--- | :--- | :--- |
| **Subnet Mask** | `11111111` | `11111111` | `11111111` | `11000000` |
| **IP Address**  | `11000000` | `10101000` | `00001100` | `10100000` |
| **Division** | --- Network Part (26 bits) --- | - Host Part (6 bits) - |

### Step 2: Find the Network Address
To find the network address, you set all the **host bits** in the given IP address to `0`.

| Details | 4th Octet (Binary) |
| :--- | :--- |
| **IP Address Bits**  | `10` `100000` |
| **Network Address Bits**| `10` `000000` (Set host bits to 0) |

*   Binary `10000000` in the 4th octet is decimal `128`.
*   **Resulting Network Address:** `192.168.12.128`

### Step 3: Find the Broadcast Address
To find the broadcast address, you set all the **host bits** in the given IP address to `1`.

| Details | 4th Octet (Binary) |
| :--- | :--- |
| **IP Address Bits**  | `10` `100000` |
| **Broadcast Address Bits**| `10` `111111` (Set host bits to 1) |

*   Binary `10111111` in the 4th octet is decimal `191`.
*   **Resulting Broadcast Address:** `192.168.12.191`

### Step 4: Determine the Host Range and Total Hosts
*   **First Usable Host:** The network address + 1 (`192.168.12.129`).
*   **Last Usable Host:** The broadcast address - 1 (`192.168.12.190`).
*   **Total Number of Hosts:** The number of host bits is 6. The formula is **2ⁿ - 2**, where `n` is the number of host bits.
    *   2⁶ - 2 = 64 - 2 = **62 usable hosts**.

### Summary of the `192.168.12.128/26` Subnet

| Property | Value |
| :--- | :--- |
| **Network Address** | `192.168.12.128` |
| **First Host** | `192.168.12.129` |
| **Last Host** | `192.168.12.190` |
| **Broadcast Address**| `192.168.12.191` |
| **Number of Hosts** | 62 |

---

## Subnetting a Subnet
You can take an existing subnet and divide it further.

**Scenario:** Divide the `192.168.12.128/26` network into **4** smaller, equal-sized subnets.

1.  **Find the bits to borrow:** To get 4 subnets, we need to borrow **2** bits (since 2² = 4).
2.  **Calculate the new subnet mask:** The old mask was `/26`. We borrow 2 bits, so the new mask is `/28` (`26 + 2`). A `/28` mask is `255.255.255.240`.
3.  **Calculate the new subnet size:** The original `/26` subnet had 64 total addresses. We divide this by the 4 new subnets we are creating: 64 / 4 = **16 addresses per subnet**.
4.  **List the new subnets:** Starting from the original network address (`.128`), we create blocks of 16.

| Subnet # | Network Address | First Host | Last Host | Broadcast Address |
| :--- | :--- | :--- | :--- | :--- |
| **1** | `192.168.12.128` | `...129` | `...142` | `...143` |
| **2** | `192.168.12.144` | `...145` | `...158` | `...159` |
| **3** | `192.168.12.160` | `...161` | `...174` | `...175` |
| **4** | `192.168.12.176` | `...177` | `...190` | `...191` |
