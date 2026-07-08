<div align="center">
  
# 🚀 Intelligent Swarm-Based Bots for Continuous Area Patrolling and Detection 🛡️

**A Smart Border Surveillance System** 🚔 

[![ROS 2](https://img.shields.io/badge/ROS_2-Jazzy-blue.svg)](https://docs.ros.org/en/jazzy/index.html)
[![micro-ROS](https://img.shields.io/badge/micro--ROS-ESP32-green.svg)](https://micro.ros.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

</div>

---

## 🌟 The Future of Border Security is Here!

Say goodbye to delayed response times and limited surveillance coverage. We are bringing **swarm intelligence** to national security! 🌍 

By utilizing an army of affordable **ESP32 microcontrollers**, our system deploys a swarm of autonomous bots that communicate continuously, patrolling borders efficiently. Powered by **micro-ROS** and the cutting-edge **ROS 2 Jazzy framework**, this decentralized, low-power system is built to thrive in harsh, remote environments.

<div align="center">
  <img src="images/img-000.jpg" width="700" alt="Block Diagram">
  <br>
  <em>⚙️ Fig 1: The Core Brain — Block diagram showing the system flow</em>
</div>

---

## 🤖 What Makes These Bots So Smart? 

It’s all about the data! Our bots use **Multi-Sensor Fusion** to process the environment like a living creature:

* 📡 **Radar Sensor:** Continuously scans the environment. It doesn't care if it's pitch black or foggy; the radar sees everything!
* 👁️ **ESP32-CAM:** The eyes of the operation! Once the radar detects movement, the camera snaps a picture and runs lightweight object detection to identify humans or potential threats.
* 📏 **Time-of-Flight (ToF):** Ever had an alarm triggered by a falling leaf? 🍃 ToF measures the exact distance to an object, filtering out environmental noise and slashing false alarms.
* 🗺️ **GPS Tracking:** Whenever an intrusion occurs, the exact real-time coordinates are transmitted to the dashboard.
* 🎯 **Dynamic Tracking:** A servo motor automatically pans the camera to track moving targets!

<div align="center">
  <table>
    <tr>
      <td align="center"><img src="images/img-004.jpg" width="400" alt="Admin Bot System"><br><em>👑 Fig 2: The Admin Bot</em></td>
      <td align="center"><img src="images/img-005.jpg" width="400" alt="Subordinate Bot System"><br><em>🦾 Fig 3: The Subordinate Bot</em></td>
    </tr>
  </table>
</div>

---

## ⚡ Edge Computing & Blazing Fast Responses

Why wait for a cloud server when you can think on your feet? By processing sensor data locally on the ESP32 edge nodes, the bots achieve **lightning-fast response times**.

We use **Asynchronous Processing** to handle camera data, which keeps latency low and stable. To make sure we never get fooled by shadows or bugs, we use **Temporal Smoothing**—the bot verifies the detection across multiple consecutive frames before sounding the alarm! 🚨

<div align="center">
  <table>
    <tr>
      <td align="center"><img src="images/img-002.png" width="400" alt="Inference Latency"><br><em>⏱️ Fig 4: Synchronous vs. Asynchronous Latency</em></td>
      <td align="center"><img src="images/img-003.png" width="400" alt="Temporal Smoothing"><br><em>📉 Fig 5: False Positive Reduction</em></td>
    </tr>
  </table>
</div>

---

## 🗺️ Live Mapping & The Command Dashboard

Through our custom **micro-ROS** framework, odometry and sensor data fly over Wi-Fi directly to the ROS 2 command center. We use the **SLAM Toolbox** to generate real-time occupancy maps while the bots autonomously navigate the terrain.

Everything is monitored on a sleek, WebSocket-based live dashboard. 💻

<div align="center">
  <table>
    <tr>
      <td align="center"><img src="images/img-001.jpg" width="400" alt="ROS Mapping"><br><em>📍 Fig 6: Live ROS Occupancy Map</em></td>
      <td align="center"><img src="images/img-007.jpg" width="400" alt="Live Mapping"><br><em>🛰️ Fig 7: Real-Time GPS Tracking</em></td>
    </tr>
  </table>
</div>

<div align="center">
  <img src="images/img-006.jpg" width="700" alt="Dashboard">
  <br>
  <em>📊 Fig 8: The Command Center Dashboard</em>
</div>

---

## 🛠️ Step-by-Step ROS 2 Setup

Want to fire up the bots yourself? Run these commands **one by one**, each in a **separate terminal** (unless mentioned otherwise).

### 🖥️ Terminal 1: Start the micro-ROS Agent
```bash
source /opt/ros/jazzy/setup.bash
ros2 run micro_ros_agent micro_ros_agent udp4 --port 8888
```

### 🖥️ Terminal 2: Publish Odometry (odom → base_link TF)
```bash
source /opt/ros/jazzy/setup.bash
python3 ~/odom_to_tf.py
```

### 🖥️ Terminal 3: Static Transform (base_link → laser TF)
```bash
source /opt/ros/jazzy/setup.bash
ros2 run tf2_ros static_transform_publisher 0 0 0 0 0 0 base_link laser
```

### 🖥️ Terminal 4: Verify the Topics
First, check what topics are alive:
```bash
source /opt/ros/jazzy/setup.bash
ros2 topic list
```
Then, make sure data is actually flowing:
```bash
ros2 topic echo /scan --once
ros2 topic echo /odom --once
```

### 🖥️ Terminal 5: Verify the Transforms (TF)
```bash
source /opt/ros/jazzy/setup.bash
ros2 run tf2_ros tf2_echo odom base_link
```
*(Stop with `Ctrl+C` after it prints values)*

Next, verify the laser:
```bash
ros2 run tf2_ros tf2_echo base_link laser
```
*(Stop with `Ctrl+C`)*

### 🖥️ Terminal 6: Start SLAM! 🗺️
```bash
source /opt/ros/jazzy/setup.bash
ros2 launch slam_toolbox online_async_launch.py
```

### 🖥️ Terminal 7: Check & Save the Map
```bash
source /opt/ros/jazzy/setup.bash
ros2 topic echo /map --once
```
*Note: Only if this prints map data, save it using the command below:*
```bash
ros2 run nav2_map_server map_saver_cli -f my_room_map --ros-args -p map_subscribe_transient_local:=true
```

### 🖥️ Terminal 8: Visualize Everything in RViz 🕶️
```bash
source /opt/ros/jazzy/setup.bash
rviz2
```
**In RViz, set up your display:**
* Set **Fixed Frame** to `map`
* Click **Add** → **Map**
* Click **Add** → **LaserScan** (Topic: `/scan`)
* Click **Add** → **Odometry** (Topic: `/odom`)

---

## 🔮 The Road Ahead: Next Advances

Our journey doesn't stop here. We are actively working on turning this from a single proof-of-concept into a massive decentralized army!

* 🐝 **Advanced Swarm Intelligence Systems:** True decentralized coordination. Bots will soon communicate directly with each other to divide patrolling sectors automatically, avoiding redundant scanning.
* 🧩 **Multi-Map Merging:** What happens when multiple bots map different areas? We are building a system to stitch and connect different maps generated by different bots into a single, massive global map of the surveillance frontier!

---

<div align="center">
  
### 👨‍💻 Meet the Masterminds Behind the Bots

**[Ashwin](https://github.com/Ashwin-Sahyadri-ECE022)** | **[Neha](https://github.com/neharaj123346)** | **[Vaishak](https://github.com/VaishakSCEM543)** | **Preetham**

</div>
