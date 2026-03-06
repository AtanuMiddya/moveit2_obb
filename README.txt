# MoveIt2 OBB Detection Robot (ROS2 + YOLOv8)

This project demonstrates **object detection and robotic arm manipulation** using:

* ROS2 Humble
* MoveIt2
* Gazebo Simulation
* YOLOv8 Oriented Bounding Box (OBB)
* Panda Robotic Arm
* Python UI for object selection

The robot detects bolts using YOLOv8 and performs pick-and-place operations in simulation.

---

# System Requirements

Recommended OS

Ubuntu 22.04 LTS

Recommended Hardware

* 8GB RAM minimum
* GPU recommended
* SSD recommended

Important

Running Gazebo + MoveIt + YOLO inside **VirtualBox is not recommended**.
Use **Ubuntu dual boot** for best performance.

---

# 1. Install Ubuntu

Install **Ubuntu 22.04 LTS**.

After installation update the system:

sudo apt update
sudo apt upgrade -y

---

# 2. Install Required Tools

sudo apt install curl gnupg lsb-release git python3-pip -y

---

# 3. Install ROS2 Humble

Add ROS repository

sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/ros2.list

Update packages

sudo apt update

Install ROS2

sudo apt install ros-humble-desktop -y

---

# 4. Setup ROS Environment

Add ROS2 to bash

echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc

Activate

source ~/.bashrc

Test ROS installation

ros2

---

# 5. Install ROS Development Tools

sudo apt install python3-colcon-common-extensions python3-rosdep -y

Initialize rosdep

sudo rosdep init
rosdep update

---

# 6. Install MoveIt2 and Gazebo

sudo apt install ros-humble-moveit -y
sudo apt install ros-humble-ros-gz -y
sudo apt install ros-humble-ros-gz-sim -y
sudo apt install ros-humble-gz-ros2-control -y

---

# 7. Install Python Libraries

pip3 install ultralytics
pip3 install opencv-python
pip3 install numpy
pip3 install PyQt5

---

# 8. Clone the Project

cd ~

git clone https://github.com/AtanuMiddya/moveit2_obb.git

---

# 9. Build the Workspace

cd ~/moveit2_obb

Install dependencies

rosdep install --from-paths src --ignore-src -r -y

Build workspace

colcon build --symlink-install

---

# 10. Source the Workspace

source ~/moveit2_obb/install/setup.bash

---

# 11. Run the Simulation

Open three terminals.

Terminal 1

source ~/moveit2_obb/install/setup.bash

ros2 launch panda_moveit_config moveit_gazebo_obb.py

This launches

* Gazebo simulator
* Panda robot
* MoveIt motion planner

---

Terminal 2

source ~/moveit2_obb/install/setup.bash

ros2 launch yolov8_obb yolov8_obb.launch.py

This starts YOLOv8 object detection.

---

Terminal 3

source ~/moveit2_obb/install/setup.bash

cd ~/moveit2_obb/UI

python3 bolt_selector.py

This opens the UI for selecting bolts.

---

# Project Structure

moveit2_obb/

src
ROS2 packages

UI
Python UI for bolt selection

build
Build files

install
Compiled workspace

log
Build logs

---

# Troubleshooting

If RViz crashes inside VirtualBox run

export LIBGL_ALWAYS_SOFTWARE=1

before launching ROS.

If build fails clean workspace

rm -rf build install log

colcon build --symlink-install

---

# Expected Result

After launching the project you should see

* Gazebo world with table and Panda robot
* RViz MoveIt interface
* YOLO detection running
* Bolt selector UI window

The robot will detect and pick bolts using YOLO detection.

---

# Author

Atanu Middya
Electrical Engineering Student
