# 🤖 UR5 ROS2 Drawing Robot (Gazebo + Web Control + IK)

## 📌 Overview

This project simulates a **UR5 robotic arm** in **ROS 2 Humble + Gazebo** and enables real-time trajectory drawing through a web interface.

The system uses **inverse kinematics (IK)** via `IKPy` to convert user-drawn trajectories into joint commands, allowing the robot to execute smooth motion in simulation.

---

## 🎥 Demo

![UR5 Demo](videos/demo.gif)

▶️ [Watch Demo](https://drive.google.com/file/d/1DiG7gqiEOJPpZ6RzulsZfuZ8Wa0lbqSt/view?usp=sharing)

---

## 🚀 How to Run the Project

### 🖥️ 0. Prerequisites

- Ubuntu 22.04
- ROS 2 Humble
- Gazebo

### 📦 1. Clone the Repository

```bash
git clone https://github.com/ravivkrahul/UR5-ros2-drawing-robot.git
cd UR5-ros2-drawing-robot
```

### ⚙️ 2. Source ROS 2

```bash
source /opt/ros/humble/setup.bash
```

### 📥 3. Install Dependencies

```bash
rosdep update
rosdep install --from-paths src --ignore-src -r -y
```

### 🐍 4. Install Python Libraries

```bash
pip3 install ikpy matplotlib scipy numpy
pip install --upgrade websockets
```

### ⚠️ 5. Fix URDF File Path (IMPORTANT)

Open:

```bash
src/ur5_draw/ur5_draw/web_direct_controller.py
```

Find:

```python
URDF_PATH = "/home/laymbot/UR5-ros2-drawing-robot/src/ur_description/urdf/ur5_robot.urdf"
```

Replace with:

```python
URDF_PATH = "/home/<your-username>/UR5-ros2-drawing-robot/src/ur_description/urdf/ur5_robot.urdf"
```

**Example:**

```python
URDF_PATH = "/home/rahul/UR5-ros2-drawing-robot/src/ur_description/urdf/ur5_robot.urdf"
```

### 🔨 6. Build the Workspace

```bash
colcon build --symlink-install --cmake-args -DBUILD_TESTING=OFF
```

### 🔄 7. Source Workspace

```bash
source install/setup.bash
```

### 🌐 8. Open Web Interface

Right-click `index.html` → **Open with browser**

### ▶️ 9. Run the System (3 Terminals)

**🧪 Terminal 1 — Launch Simulation**

```bash
source /opt/ros/humble/setup.bash
source install/setup.bash

ros2 launch ur_simulation_gazebo ur_sim_control.launch.py ur_type:=ur5
```

**📊 Terminal 2 — Plotter**

```bash
source /opt/ros/humble/setup.bash
source install/setup.bash

ros2 run ur5_draw live_plotter_multiview
```

**🎮 Terminal 3 — Controller**

```bash
source /opt/ros/humble/setup.bash
source install/setup.bash

ros2 run ur5_draw web_direct_controller
```

---

## 🎯 Expected Output

- Gazebo opens with the UR5 robot
- Plot window updates in real time
- Web interface accepts drawing input
- Robot follows the drawn trajectory

---

## 🐛 Troubleshooting

| Issue | Solution |
|---|---|
| ❌ URDF file not found | Fix the path in `web_direct_controller.py` (see Step 5) |
| ❌ Package not found | Run `source install/setup.bash` |
| ❌ Build issues | Clean and rebuild: `rm -rf build install log && colcon build --cmake-args -DBUILD_TESTING=OFF` |

---

## 🚀 Future Work

- **MoveIt integration** — motion planning
- **Vision-based control** — ML + OpenCV
- **Real robot deployment**
- **Improved UI**

---

## 👨‍💻 Author

- **Rahul Ravi VK**
- **Rishi Mehta**
- **Pratham Salvi**
  
Master's in Robotics — University of Maryland

---

## ⭐ Contributions

Feel free to fork and improve!
