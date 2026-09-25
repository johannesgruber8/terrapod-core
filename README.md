# 🤖 ROS2 Tracked Robot Stack (Jetson Orin Nano)

An autonomous navigation and AI-driven control stack for a tracked vehicle robot running **ROS2** on the **Nvidia Jetson Orin Nano** platform. The system integrates LiDAR SLAM, camera vision, edge voice recognition, and a Local Large Language Model (LLM) for intelligent decision-making.

---

## 🚀 Key Features

* 📍 **Autonomous Navigation:** 2D/3D SLAM and path planning using LiDAR (`nav2` & `slam_toolbox`).
* 👁️ **Computer Vision:** Object detection, tracking, and spatial awareness accelerated by Nvidia Jetson TensorRT.
* 🎙️ **Voice Control:** Offline speech-to-text (STT) for processing natural language robot commands.
* 🧠 **Edge LLM Integration:** Local LLM reasoning running on the Orin Nano GPU to handle complex multi-step tasks.
* ⚙️ **Tracked Kinematics:** Custom differential-drive controller optimized for tracked/skid-steer vehicle physics.

---

## 🛠️ Hardware Architecture

* **Compute:** Nvidia Jetson Orin Nano (8GB Developer Kit)
* **OS / Middleware:** Ubuntu 22.04 LTS + ROS2 Humble / Iron
* **Sensors:** 
  * 360° RPLIDAR (or equivalent)
  * IMU (for odometry filtering via `robot_localization`)
  * USB/CSI Camera Module
* **Actuators:** Dual DC Motor Setup with Skid-Steer / Tracked Kinematics Driver

---

## 📦 Repository Structure

```text
├── robot_bringup/        # Launch files for sensors, controllers, and core nodes
├── robot_description/    # URDF/Xacro models and meshes for the tracked chassis
├── robot_navigation/     # Nav2 configuration, costmaps, and AMCL parameters
├── robot_vision/         # Nvidia TensorRT / OpenCV nodes for camera perception
├── robot_voice/          # Speech recognition and LLM interface nodes
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
* JetPack 5.x / 6.x installed on your Jetson Orin Nano
* ROS2 (Humble or newer)
* CUDA, TensorRT, and DeepStream SDKs (for vision acceleration)

### Installation
1. Clone this repository into your ROS2 workspace:
   ```bash
   cd ~/ros2_ws/src
   git clone https://github.com
   ```

2. Install system dependencies:
   ```bash
   cd ~/ros2_ws
   rosdep install --from-paths src --ignore-src -r -y
   ```

3. Build the workspace:
   ```bash
   colcon build --symlink-install
   source install/setup.bash
   ```

### Running the Robot
To launch the core hardware drivers and sensors:
```bash
ros2 launch robot_bringup robot.launch.py
```

To launch navigation and mapping:
```bash
ros2 launch robot_navigation nav2_slam.launch.py
```
