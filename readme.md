Packet Traffic Arbitration (PTA) Simulation in C
This project demonstrates a basic Packet Traffic Arbitration (PTA) system implemented in C. PTA is a hardware-based approach used to manage traffic priorities between Bluetooth and Wi-Fi communications, ensuring minimal interference between them. In this simulation, Wi-Fi is prioritized during high-throughput transmissions, while Bluetooth traffic is managed accordingly based on availability.

Overview
In real systems, PTA is handled by hardware or firmware. This project, however, provides a simplified software-based simulation to show how PTA can manage the priorities of Bluetooth and Wi-Fi traffic. The project uses threads to simulate Wi-Fi and Bluetooth traffic events, and a control function (PTA_control) decides which protocol gets access based on priority.

How the Project Works
Wi-Fi and Bluetooth Priority: The system assigns Wi-Fi higher priority by default. When Wi-Fi traffic is detected, Wi-Fi gets the channel. If Wi-Fi is idle, Bluetooth traffic is allowed to proceed.

Thread-based Simulation: Wi-Fi and Bluetooth traffic are handled by separate threads to simulate concurrent communication events. These events continuously run and invoke the PTA control logic to arbitrate between the two.

Mutex for Synchronization: A mutex is used to ensure that the PTA status (whether Wi-Fi or Bluetooth is busy) is accessed safely across multiple threads.

Key Components
PTA Control Logic:

Decides whether Wi-Fi or Bluetooth gets priority for transmission.
Wi-Fi Handler:

Simulates Wi-Fi traffic. When Wi-Fi is busy, this function processes the traffic and sets the Wi-Fi state to busy.
Bluetooth Handler:

Simulates Bluetooth traffic. It handles Bluetooth transmissions when Wi-Fi is idle and sets the Bluetooth state to busy.
Threads:

Two threads simulate Wi-Fi and Bluetooth events running continuously, invoking the PTA control function to determine which traffic should proceed.
Getting Started
Requirements
A C compiler (e.g., GCC)
POSIX Threads library (pthread) for thread creation and mutex locking
Linux, macOS, or any system that supports POSIX threads
Compilation
To compile the program, use the following command:

bash
Copy code
gcc -o pta_simulation pta_simulation.c -lpthread
Running the Program
After compiling, run the program with:

bash
Copy code
./pta_simulation
The program simulates Wi-Fi and Bluetooth traffic, allowing you to see how the PTA system decides between the two.

Example Output
When you run the program, you'll see output showing how PTA prioritizes traffic. Below is a sample output:

vbnet
Copy code
PTA: Wi-Fi is busy, prioritizing Wi-Fi traffic...
Handling Wi-Fi traffic...
Wi-Fi traffic handled.
PTA: Wi-Fi not busy, checking Bluetooth...
PTA: Bluetooth is busy, prioritizing Bluetooth traffic...
Handling Bluetooth traffic...
Bluetooth traffic handled.
The simulation runs in an infinite loop where both Wi-Fi and Bluetooth events occur periodically, and the PTA control function determines who gets priority.

Code Structure
pta_simulation.c: This is the main file that contains the PTA control logic, traffic handlers for Wi-Fi and Bluetooth, and the threading logic.
Key Functions
PTA_control(): The core function that manages priority between Wi-Fi and Bluetooth traffic.
handle_wifi_traffic(): Simulates the handling of Wi-Fi traffic.
handle_bluetooth_traffic(): Simulates the handling of Bluetooth traffic.
wifi_event(): Simulates Wi-Fi traffic events using a thread.
bluetooth_event(): Simulates Bluetooth traffic events using a thread.
PTA Logic
Priority Handling: Wi-Fi has higher priority by default. If Wi-Fi is busy, Bluetooth waits. If Wi-Fi is idle, Bluetooth gets to transmit.

Mutex Locking: The pthread_mutex_t ensures that only one thread can modify the PTA status at a time, avoiding race conditions.

Future Improvements
Dynamic Priority Adjustment: In the future, priority can be dynamically adjusted based on traffic demands or packet size.

Real Hardware Integration: In a real system, this logic would interact with hardware registers and interrupts to handle PTA more efficiently.

Traffic Statistics: We can add counters to track the number of packets transmitted by Wi-Fi and Bluetooth and display statistics.
