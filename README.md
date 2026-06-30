# ARTIMES 🛸
### Autonomous Reconnaissance and Threat Intelligence Mission Execution System

> A ROS 2 drone that doesn't just navigate — it *understands* its environment.  
> Multi-modal sensor fusion (Camera + LiDAR + IMU) powers adaptive surveillance patrol with real-time anomaly detection.

---

![ROS 2](https://img.shields.io/badge/ROS_2-Humble-blue?style=flat-square&logo=ros)
![Gazebo](https://img.shields.io/badge/Simulator-Gazebo_Harmonic-orange?style=flat-square)
![Python](https://img.shields.io/badge/Language-Python_3.10-green?style=flat-square&logo=python)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square)
![Status](https://img.shields.io/badge/Status-Phase_1_In_Progress-yellow?style=flat-square)

---

## What is ARTIMES?

Most drone projects bolt YOLO onto Nav2 and call it "intelligent."  
ARTIMES is different.

The core innovation is a **unified sensor fusion decision layer** — the drone continuously fuses:

| Sensor | What it contributes |
|--------|-------------------|
| 📷 RGB Camera | Visual target detection and classification (YOLO) |
| 📡 LiDAR | 3D mapping, obstacle geometry, spatial awareness |
| 🔄 IMU | Orientation, vibration, motion state estimation |

These three streams feed a single **Mission State Machine** that decides in real time whether to patrol, investigate an anomaly, or recover from failure.

---

## Innovation vs Standard Projects

| Feature | Typical Nav2 + YOLO Drone | ARTIMES |
|---------|--------------------------|---------|
| Perception | Camera only | Camera + LiDAR + IMU fusion |
| Decision making | None | Autonomous mission state machine |
| Anomaly response | None | Detect → investigate → resume |
| Architecture | Monolithic | Modular, one package per phase |

---

## Project Structure

> One package per phase. You build it exactly as you learn it.

```
artimes/
│
├── artimes_description/     # Phase 1 — drone URDF model
├── artimes_control/         # Phase 1 — movement + teleop
├── artimes_slam/            # Phase 2 — mapping
├── artimes_navigation/      # Phase 3 — patrol + Nav2
├── artimes_vision/          # Phase 4 — YOLO + anomaly
│
└── README.md
```

Each package is unlocked as you complete the previous phase.  
No overwhelming folders. No files you don't understand yet.

---

## Build Phases

```
Phase 1 ──► Phase 2 ──► Phase 3 ──► Phase 4
  🟢            🟡            🔵           🔴
Fly drone     Build map    Auto patrol   Detect &
in Gazebo    with SLAM     + Nav2        react
```

### 🟢 Phase 1 — Fly it
Packages: `artimes_description` + `artimes_control`
- URDF drone model in Gazebo
- Keyboard teleoperation
- RViz2 visualization

### 🟡 Phase 2 — Map it
Package: `artimes_slam`
- LiDAR + depth camera
- SLAM Toolbox live mapping
- TF tree: `map → odom → base_link`

### 🔵 Phase 3 — Navigate it
Package: `artimes_navigation`
- Nav2 stack
- Patrol waypoints
- Obstacle avoidance

### 🔴 Phase 4 — See it
Package: `artimes_vision`
- YOLO object detection
- Anomaly trigger
- Investigate + resume patrol

---

## Requirements

```bash
# ROS 2 Humble (Ubuntu 22.04)
sudo apt install ros-humble-desktop
sudo apt install ros-humble-gazebo-ros-pkgs
sudo apt install ros-humble-nav2-bringup
sudo apt install ros-humble-slam-toolbox
pip install ultralytics opencv-python
```

---

## Quick Start

```bash
git clone https://github.com/YOUR_USERNAME/artimes.git
cd artimes
colcon build --symlink-install
source install/setup.bash

# Phase 1 — launch drone in Gazebo
ros2 launch artimes_description gazebo.launch.py
```

---

## Roadmap

- [x] README + project structure
- [ ] Phase 1 — drone in simulation
- [ ] Phase 2 — SLAM mapping
- [ ] Phase 3 — autonomous patrol
- [ ] Phase 4 — vision + anomaly detection

---

## Author

**Built by:** [Your Name]  
**Stack:** ROS 2 Humble · Gazebo · Nav2 · SLAM Toolbox · OpenCV · YOLO

---

## License

MIT — free to use and build on.
