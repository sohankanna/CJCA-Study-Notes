# The OSI model

The OSI model is hierarchical. When a device sends data, the process starts at Layer 7 and moves down to Layer 1. When a device receives data, the process is reversed, moving from Layer 1 up to Layer 7.

### Application-Oriented Layers (Layers 7, 6, 5)
These layers deal with application-level data and are closest to the end-user.

| Layer # | Layer Name | Key Function | PDU | Analogy |
| :--- | :--- | :--- | :--- | :--- |
| **7** | **Application**| The **user interface** to the network. This layer provides network services directly to the end-user's applications. It's what the user sees and interacts with. | Data | The application you are using (e.g., your web browser, email client). |
| **6** | **Presentation**| The **translator** of the network. It ensures that data sent from one system's application layer can be understood by the application layer of another system. It handles data formatting, character encoding (e.g., ASCII), data compression, and **encryption/decryption** (e.g., SSL/TLS). | Data | A diplomat who translates one language into another so two leaders can communicate. |
| **5** | **Session**| The **conversation manager**. It is responsible for establishing, managing, maintaining, and terminating sessions (logical connections) between two applications. | Data | A telephone operator who establishes the call, ensures it stays connected, and hangs it up when finished. |

### Transport-Oriented Layers (Layers 4, 3, 2, 1)
These layers deal with the actual transmission of data across the network.

| Layer # | Layer Name | Key Function | PDU | Analogy |
| :--- | :--- | :--- | :--- | :--- |
| **4** | **Transport** | Provides **end-to-end data delivery** and error checking. It breaks large files into smaller chunks (**segmentation**) on the sending end and reassembles them on the receiving end. It also manages flow control to prevent network congestion. This is where **TCP (reliable)** and **UDP (unreliable)** operate. | Segment | The postal service's packaging department, which puts letters into envelopes, numbers them, and ensures they are all accounted for. |
| **3** | **Network** | The **router** of the network. This layer is responsible for forwarding data packets across different networks. It handles **logical addressing (IP addresses)** and determines the best path for data to travel from source to destination. | Packet | The postal service's sorting hub, which reads the city and street address on an envelope to route it to the correct destination city. |
| **2** | **Data Link** | Provides reliable, node-to-node data transfer across a **single, local network link**. It organizes bits from Layer 1 into **frames** and handles **physical addressing (MAC addresses)**. It is also responsible for error detection on the local link. | Frame | The local mail carrier who delivers the mail to a specific physical mailbox on their route. |
| **1** | **Physical** | The **hardware** layer. It is responsible for the actual transmission of raw bits (1s and 0s) over a physical medium. This includes everything from the voltage of the electrical signals to the layout of pins on a connector. | Bits | The physical mail truck, the roads, and the paper the letter is written on. |

---

## The Data Flow Process

*   **Sending Data (Encapsulation):** An application creates data at Layer 7. As the data passes *down* through the layers, each layer adds its own header (and sometimes a trailer), wrapping the data from the layer above.
*   **Receiving Data (Decapsulation):** The raw bits are received at Layer 1. As the data passes *up* through the layers, each layer reads and strips off its corresponding header, passing the unwrapped data up to the next layer until it reaches the application at Layer 7.

