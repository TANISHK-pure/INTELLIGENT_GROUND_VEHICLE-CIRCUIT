## Custom IGV Power & Logic Distribution Architecture – Gujcost Robofest 5.0
📋 Overview
A comprehensive power distribution and centralized command architecture engineered for an Intelligent Ground Vehicle (IGV). This system serves as the nervous system of the robot, seamlessly bridging high-level ROS2 processing with rugged, low-level hardware interfacing. It ensures stable power delivery and reliable communication between heavy-duty motor controllers, vision systems, and microcontrollers.

🔌 Hardware Architecture & Tech Stack
High-Level Compute: NVIDIA Jetson Nano (handling ROS2, Orbbec Astra depth mapping, and RPLidar data)

Low-Level Controller: Arduino Mega 2560 Rev3 (handling kinematics, encoders, MPU-6050, and 4x HC-SR04 ultrasonic sensors)

EDA Software: EasyEDA / KiCad

Power Regulation: Multiple XL4015 5A Buck Converters for isolated step-down routing

🧠 Engineering Challenges Solved
🛡️ Multi-Layered Electrical Safety & E-Stop System
To ensure robust operation and strict compliance with IGV safety standards, the power distribution network features a hardware-level, multi-tiered protection strategy:

Primary Protection: A main 50A Fuse positioned directly at the battery source to prevent catastrophic overcurrent.

Master Control: A heavy-duty 40A Toggle Switch paired with a master Relay designed to integrate a hardware Emergency Stop (E-Stop) kill switch. Activating the kill switch instantly severs power to the drive systems without corrupting the logic state.

Sub-System Isolation: From the central Power Distribution Block, power is routed through individual Branch Fuses (5A, 10A, etc.) dedicated to specific XL4015 buck converters. This isolation guarantees that a stalled motor or shorted peripheral will only trip a localized fuse, keeping the main computer and sensors online.

⚡ Distributed Power Regulation
Supplying power to an Orbbec Astra Cam, RPLidar, and heavy DC motors from a single battery source invites severe voltage drops. I implemented parallel XL4015 buck converters, isolating the noisy motor power lines from the sensitive 5V logic and sensor lines, ensuring the Jetson Nano and Arduino Mega receive clean, uninterrupted current.

🔌 Plug-and-Play Competition Readiness
Designed with modularity in mind. All major peripherals—including the MPU-6050, four independent ultrasonic sensors, and optical motor encoders—utilize custom breakout headers. This plug-and-play approach allows for instant hot-swapping or diagnostics of external hardware during high-pressure live competition scenarios.

📡 Data Segregation & Stability
Maintained strict separation of data pipelines. Heavy RGB-D video bandwidth is routed exclusively through the Jetson's onboard USB 3.0 ports, while the ROS2 cmd_vel and sensor telemetry are transferred to the Arduino Mega via a dedicated, securely routed USB A-to-B serial connection.

📐 PCB Renders & Layout
(Upload your images to the repo and add the links below)

Schematic PDF: https://drive.google.com/file/d/12369RNZ6-LQWs_tLmLJ_DZgLMUVwt2NX/view?usp=sharing


🤝 Let's Connect
I am always open to discussing hardware architecture, custom PCB design, embedded systems, and work for you.

💼 LinkedIn: https://www.linkedin.com/in/tanishk-choudhary-215b95328/

📧 Email: ctanishk8@gmail.com
