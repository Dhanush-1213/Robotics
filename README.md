
# 🤖 UR5e Robotic Arm — Colour-Based Sorting Simulation

A Webots robotics simulation in which a **Universal Robots UR5e** arm — mounted with a **Robotiq 3F gripper** and a **colour-recognition camera** — autonomously sorts coloured boxes arriving on a conveyor belt into separate crates.

---

## 🎬 Overview

| Property | Value |
|----------|-------|
| Simulator | [Webots](https://cyberbotics.com/) R2021a |
| Robot | Universal Robots UR5e |
| Gripper | Robotiq 3-Finger Adaptive Gripper |
| Sensor | Camera (with built-in object recognition) + Distance Sensor |
| Controller | Python (`ure5_sorting.py`) |
| Environment | Factory floor with an 8 m conveyor belt and plastic sorting crates |

---

## 📁 Project Structure

```
Arm_Robo/
├── arm_robot.wbt       # Webots world file — scene, robot, belt, objects
└── ure5_sorting.py     # Python robot controller
```

---

## 🏭 Simulation Scene

The factory environment (`arm_robot.wbt`) contains:

- **UR5e arm** mounted on a metal workbench at the head of the conveyor belt
- **Robotiq 3F Gripper** attached to the tool slot for grasping boxes
- **Camera** (with recognition enabled, up to 10 objects) mounted on the tool — detects object colour
- **Distance Sensor** for proximity detection during pick operations
- **Conveyor Belt** — 8 m long, speed `0.2 m/s`, carrying mixed-colour boxes
- **Coloured boxes** — 3 colours, 2 boxes each:
  - 🔴 Red (`1 0 0`)
  - 🔵 Blue (`0 0 1`)
  - 🟢 Green (`0 1 0`)
- **3 Plastic Crates** positioned near the base for sorted output

---

## ⚙️ How It Works

```
Conveyor Belt
     │  boxes approach
     ▼
┌─────────────┐
│   Camera    │  ──► detects colour via object recognition
└─────────────┘
     │
     ▼
┌─────────────┐
│  Distance   │  ──► triggers pick when box is in range
│   Sensor    │
└─────────────┘
     │
     ▼
┌─────────────┐
│  UR5e Arm   │  ──► moves to grasp position
│  + 3F Grip  │  ──► picks up box
└─────────────┘
     │
     ▼
Sort by colour → place in corresponding crate
```

1. The conveyor belt carries boxes toward the robot at 0.2 m/s.
2. The camera recognises each box's colour using Webots' built-in `Recognition` system.
3. The distance sensor triggers the pick sequence when a box is within reach.
4. The UR5e arm moves to the box, closes the Robotiq gripper, lifts and transports it.
5. The arm deposits the box into the crate assigned to that colour.
6. The arm returns to home and waits for the next box.

---

## 🚀 Getting Started

### Prerequisites

- [Webots R2021a](https://github.com/cyberbotics/webots/releases/tag/R2021a) (or later)
- Python 3.x

### Running the Simulation

1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/Robotics.git
   cd Robotics/Arm_Robo
   ```

2. Open Webots and load the world file:
   ```
   File → Open World → arm_robot.wbt
   ```

3. Ensure the controller `ure5_sorting.py` is set as the UR5e controller in the scene tree (field: `controller "try1"`), or update the controller name in the world file to match.

4. Press **Play** ▶ in Webots to start the simulation.

---

## 🧩 Key Webots Nodes Used

| Node | Role |
|------|------|
| `UR5e` | 6-DOF industrial robot arm |
| `Robotiq3fGripper` | 3-finger adaptive gripper for grasping |
| `Camera` + `Recognition` | Colour-based object detection (up to 10 objects) |
| `DistanceSensor` | Detects proximity of objects on the belt |
| `ConveyorBelt` | Moving surface transporting boxes |
| `Solid` (×6) | Physics-enabled coloured boxes |
| `PlasticCrate` (×3) | Sorting destination bins |

---

## 📚 Concepts Demonstrated

- **Robot arm kinematics** — joint-space control of a 6-DOF industrial arm
- **Computer vision in robotics** — colour recognition via onboard camera
- **Pick-and-place automation** — sensor-triggered grasping and placement
- **Gripper control** — 3-finger adaptive gripper actuation
- **Physics simulation** — rigid-body dynamics for boxes and crates
- **Webots world description** — VRML-based scene authoring (`.wbt`)
- **Python robot controller API** — Webots Python bindings

---

