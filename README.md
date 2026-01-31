# Multi-Channel-Industrial-Sorting-PLC
An advanced PLC-based industrial automation system featuring multi-channel color sorting, robotic synchronization (interlocking), and a fail-safe global emergency stop architecture developed in Factory I/O.
## Overview
Project Description
Implementation of a multi-stage industrial automation line designed for real-time color detection, material handling, and robotic palletizing. The system architecture is developed using a Digital Twin approach (Factory I/O) and programmed via Function Block Diagram (FBD) logic.

The design emphasizes industrial-grade safety protocols and deterministic process control through hardware-in-the-loop synchronization.

Technical Specifications
1. Safety and Control Architecture
Global Safety Interlocking: A centralized control layer based on RS Latch logic manages the system's operational state (Master_Enable).

Fail-Safe NC Integration: All Emergency Stop nodes and the main Stop button are configured as Normally Closed (NC) circuits.

Logic-Level Safety: NOT gates are utilized to monitor the continuity of the safety chain; any signal interruption results in an immediate, system-wide inhibition of all actuators.

System State Reset: Upon an Emergency Stop or Stop event, the logic triggers a reset of all volatile production memories (Emitter SR Latches) to prevent unintended restarts.

2. Intelligent Sorting and Actuation
Sensing and Identification: Industrial color sensors detect the spectral signature of incoming parts (Green, Blue, Gray) to determine the routing path.

Feedback-Controlled Diverting: Sorting pushers are governed by SR Latches.

Actuator Verification: Retraction of pneumatic cylinders is interlocked with Front Limit sensors, ensuring the item has cleared the diverting zone before the actuator returns to its home position.

3. Robotic Synchronization (Process Interlocking)
Asynchronous Interlock: The 2-axis robotic arms operate under a Wait-for-Box protocol.

State-Machine Execution: The robot executes the pick-and-place cycle but remains in a "Holding" state at the drop coordinates until the S_Box_Ready sensor confirms the presence of a container.

Batching and Throughput: CTU (Up-Counters) monitor the volume of each batch. Upon reaching the setpoint (3 items), the system executes a container-exit sequence and resets the counter for the next cycle.

4. Feed Management
Deterministic Spawning: Emitters are synchronized using Edge-Triggered (R_TRIG) logic.

Bottleneck Prevention: A "One In - One Out" logic gate ensures that new raw material is only introduced when the primary entry conveyor is clear, maintaining constant system pressure without congestion.

Logic Documentation
The repository includes comprehensive FBD screenshots covering:

Master Safety Chain: The implementation of the NC logic and RS Latch control.

Actuator Gating: The AND/OR gate configurations for conveyor flow control.

Pusher Feedback: The SR Latch logic for pneumatic components.

Video Demonstration
Link to Technical Demo on YouTube

The demonstration includes system cold-start, multi-channel sorting, robotic interlock verification, and a Fail-Safe Emergency Stop test.
Author: Georgios Pantazis

Role: Electrical and Computer Engineer 
