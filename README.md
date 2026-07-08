<div align="center">
  <h1>Intelligent Swarm-Based Bots for Continuous Area Patrolling and Detection</h1>
  <p><strong>Smart Border Surveillance System</strong></p>
</div>

## 📖 Abstract

Border surveillance is a major factor in national security. Yet, existing systems often suffer from limitations like limited coverage and delayed response times. This repository presents the codebase and methodology for a **Smart Border Surveillance System** utilizing ESP32 microcontrollers with swarm nodes, integrated with a multi-sensor array including Radar, Time-of-Flight (ToF), GPS, and Camera modules. 

The system provides real-time environmental data, detects motion, captures images, and verifies intrusions using sensor fusion and lightweight object detection. Powered by **micro-ROS** and the **ROS 2 Jazzy framework**, this decentralized, cost-effective, and low-power system is designed for deployment in remote areas with low human coverage, offering high reliability, scalability, and autonomy.

---

## 🚀 System Architecture & Methodology

The project operates using a combination of multi-sensor detection, edge processing, and swarm-based communication to ensure real-time monitoring, accurate intrusion detection, and effective response.

### Multi-Sensor Fusion
1. **Continuous Monitoring:** Radar continuously scans the environment, effectively detecting movement even in low visibility (darkness, fog).
2. **Image Capture & Detection:** Upon motion detection, the ESP32 activates the ESP32-CAM to capture images, which are analyzed using lightweight object detection to identify humans or potential threats.
3. **Distance Verification:** A Time-of-Flight (ToF) sensor measures the distance between the system and the detected object to filter out environmental noise (like moving leaves) and reduce false alarms.
4. **Tracking & Localization:** A servo motor adjusts the camera angle to track movement, while the GPS module records exact coordinates for effective tracking.

<div align="center">
  <img src="images/img-000.jpg" width="600" alt="Block Diagram">
  <br>
  <em>Fig 1: Block diagram showing the system flow</em>
</div>

---

## 🤖 Bot Systems

The hardware is designed for robustness and ease of deployment. The swarm consists of Admin and Subordinate bots coordinating seamlessly.

<div align="center">
  <table>
    <tr>
      <td align="center"><img src="images/img-004.jpg" width="400" alt="Admin Bot System"><br><em>Fig 2: Admin Bot System</em></td>
      <td align="center"><img src="images/img-005.jpg" width="400" alt="Subordinate Bot System"><br><em>Fig 3: Subordinate Bot System</em></td>
    </tr>
  </table>
</div>

---

## 📊 Data Analysis & Results

By processing sensor data locally on the ESP32 edge nodes, the system achieves much faster response times compared to fully cloud-dependent setups.

### Inference Latency & Temporal Smoothing

The asynchronous handling of camera data ensures low and stable latency. Furthermore, to eliminate false positives, the system utilizes **temporal smoothing**—verifying detections across multiple consecutive frames before triggering an alert.

<div align="center">
  <table>
    <tr>
      <td align="center"><img src="images/img-002.png" width="400" alt="Inference Latency"><br><em>Fig 4: Comparison of inference latency (Synchronous vs. Asynchronous)</em></td>
      <td align="center"><img src="images/img-003.png" width="400" alt="Temporal Smoothing"><br><em>Fig 5: False Positive Reduction Using Temporal Smoothing</em></td>
    </tr>
  </table>
</div>

### Mapping and Dashboard Integration

Through the micro-ROS communication framework, odometry and sensor data are reliably transmitted with low latency to a ROS 2 workstation. SLAM Toolbox is utilized to generate real-time occupancy maps for autonomous navigation. 

A WebSocket-based dashboard displays sensor values, alerts, and system status clearly in real time.

<div align="center">
  <table>
    <tr>
      <td align="center"><img src="images/img-001.jpg" width="400" alt="ROS Mapping"><br><em>Fig 6: Mapping of the assigned location using ROS</em></td>
      <td align="center"><img src="images/img-007.jpg" width="400" alt="Live Mapping"><br><em>Fig 7: Live Mapping using GPS module</em></td>
    </tr>
  </table>
</div>

<div align="center">
  <img src="images/img-006.jpg" width="600" alt="Dashboard">
  <br>
  <em>Fig 8: Dashboard showing real-time data</em>
</div>

---

## 💻 Code Structure

- `/esp32_slam_bot/esp32_slam_bot.ino`: Main ROS 2 / micro-ROS source code for the ESP32 SLAM Robot.

## 🛠️ Setup & Deployment

1. Open `/esp32_slam_bot/esp32_slam_bot.ino` in the Arduino IDE.
2. Install the necessary libraries (`micro_ros_arduino`, `ESP32Servo`).
3. Configure your WiFi credentials (`ssid`, `pass`) and ROS 2 agent IP (`agent_ip`).
4. Flash the code to the ESP32.
5. Run the `micro-ROS-agent` on your workstation to bridge the ESP32 to the ROS 2 Jazzy ecosystem.

---
*Authors: Preetham Krishan K J, Vaishak D Karkera, Ashwin Suresh, Neha Raj, Mrs. Mehnaz Fathima C*
*Dept. of Electronics and Communication, Sahyadri College of Engineering and Management, Mangalore, India.*
