# V2LA Lab Onboarding

A step-by-step guide for undergraduate research interns in robotics and autonomous systems.

**Your path:** Lab access → Ubuntu & Docker → LaTeX → ROS 2 → F1TENTH simulator → Driving labs → LIMO Pro robot

## ROS 2 Versions

- **Learning and simulation (Sections 3 and 5–7):** use **ROS 2 Humble on Ubuntu 22.04**.
- **LIMO Pro robot (Section 8):** the robot runs **ROS 2 Foxy on Ubuntu 20.04**. You will port and test your code on Foxy before running it on the robot.
- Always use the documentation that matches the ROS 2 version you are running.

---

## 1. Get Lab Access

Submit the [Building Access Request Form](https://www.eng.ufl.edu/facilities/service-requests/building-access-request-form/):

- **Supervisor or Professor Name:** Dung Tran
- **Position Type:** Student
- **Access requested for:** your name and UFID
- **Request type:** Electronic Door Access Request
- **Building:** Malachowsky Hall
- **Access:** Building Exterior Door Access, and Lab 5225 (not "HCC Labs Combined")
- **Acknowledgement of Lab Safety Training Completion:** check the box

## 2. Lab Rules and Weekly Routine

**Contacts:** Yuntao Li ([yli17@ufl.edu](mailto:yli17@ufl.edu)) and Dr. Dung Tran ([dungtran@ufl.edu](mailto:dungtran@ufl.edu))

**In the lab:**

- No food or drinks.
- Study and work quietly so you don't disturb others.
- Follow the robot safety rules in [Section 8](#8-limo-pro-robot).

**Every week:**

- **Work schedule:** Share your working schedule with Yuntao Li in advance, so Yuntao knows when you will be in the lab, can plan discussions with you, and can coordinate lab space if needed.
- **Progress notes:** Keep your own Overleaf project with detailed updates: what you studied, what you built, results, and errors. Share the project with Yuntao Li (yli17@ufl.edu).
- **Email update:** Before each meeting, send a brief update to Yuntao Li and Dr. Tran.
- **Weekly meeting:** Every **Tuesday at 1:00 pm** in the lab, **Malachowsky Hall 5225**. Bring one result to show and any questions you are stuck on.

## 3. Ubuntu, Virtual Machines, and Docker

Set up ROS 2 Humble with a virtual machine or with Docker. If your laptop already runs Ubuntu 22.04, skip both and [install ROS 2 Humble](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html) directly.

**Virtual machine:** run Ubuntu 22.04 in VirtualBox, then [install ROS 2 Humble](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html).

- Follow [Run Ubuntu in VirtualBox](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox), but download the [Ubuntu 22.04 image](https://releases.ubuntu.com/jammy/). The tutorial uses Ubuntu 22.10.
- Change the default username and password when you create the VM. The defaults create a user without `sudo`, and you need `sudo` to install ROS 2.
- Give the VM at least 8 GB of RAM and 4 CPUs if your laptop allows it.

**Docker:** run ROS 2 inside a container, starting from the [`osrf/ros:humble-desktop`](https://hub.docker.com/r/osrf/ros) image, which includes RViz and turtlesim.

- [Docker concepts](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/): containers, images, and Compose
- On Ubuntu, [install Docker Engine](https://docs.docker.com/engine/install/ubuntu/), then follow the [post-install steps](https://docs.docker.com/engine/install/linux-postinstall/) to run without `sudo`. On Windows or Mac, install [Docker Desktop](https://docs.docker.com/desktop/).
- Apps with windows, such as RViz and turtlesim, need extra display setup to appear from a container. On a Linux laptop, see [Setup ROS 2 with VSCode and Docker](https://docs.ros.org/en/humble/How-To-Guides/Setup-ROS-2-with-VSCode-and-Docker-Container.html). On Windows, the virtual machine is the simpler choice.

**Newer Macs (M1 or later):** the Ubuntu 22.04 desktop image and the `osrf/ros:humble-desktop` image are built for Intel/AMD computers and do not run on these Macs. Use Docker with the official [`ros:humble`](https://hub.docker.com/_/ros) image, and install the desktop tools inside the container with `apt update && apt install ros-humble-desktop`. Windows such as RViz cannot be forwarded to a Mac reliably; show them in your web browser with noVNC instead, as the F1TENTH simulator's Docker setup does for RViz ([Section 6](#6-f1tenth-simulator)).

## 4. LaTeX and Overleaf

- [Learn LaTeX in 30 minutes](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes)
- [Overleaf documentation](https://www.overleaf.com/learn): look up topics as needed

## 5. ROS 2 Humble

Complete these [Humble tutorials](https://docs.ros.org/en/humble/Tutorials.html) in order, using the Python version when a tutorial offers C++ and Python:

1. [Beginner: CLI tools](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools.html): configuring your environment, turtlesim and rqt, nodes, topics, services, parameters, actions, logs, launching nodes, and recording data
2. [Beginner: Client libraries](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries.html): colcon, workspaces, packages, publishers and subscribers, services, custom messages, and parameters. Custom message packages use CMake even when your nodes are in Python. Skip the C++-only tutorials (implementing custom interfaces and plugins).
3. Launch files: [Creating a launch file](https://docs.ros.org/en/humble/Tutorials/Intermediate/Launch/Creating-Launch-Files.html) and [Integrating launch files into ROS 2 packages](https://docs.ros.org/en/humble/Tutorials/Intermediate/Launch/Launch-system.html)
4. [tf2](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Tf2-Main.html): coordinate frames and transforms. Some later tf2 tutorials are C++ only; do the Python ones.

## 6. F1TENTH Simulator

- [F1TENTH Gym ROS 2 bridge, `dev-humble` branch](https://github.com/f1tenth/f1tenth_gym_ros/tree/dev-humble) (**start here**): install (native or Docker), launch, drive, and connect your own node. The `main` branch is for Foxy, and `dev-jazzy` is for ROS 2 Jazzy.
- [Course documentation](https://f1tenth-coursekit.readthedocs.io/en/latest/): lectures (the course is now named RoboRacer)
- [Lab starter code](https://github.com/f1tenth/f1tenth_labs_openrepo): clone with `git clone --recurse-submodules https://github.com/f1tenth/f1tenth_labs_openrepo.git`, or the lab folders will be empty.

**Stay on Humble:** the current lab handouts use ROS 2 Jazzy and the `dev-jazzy` simulator branch. Use `dev-humble` instead, and replace `jazzy` with `humble` in commands and documentation links. The lap counter mentioned in Labs 3 and 4 exists only on `dev-jazzy`; the maps those labs use are on `dev-humble`.

## 7. Autonomous Driving Labs

Each link below opens the lab's handout and starter code. Read the handout and the matching lecture, then complete the **simulation** parts. Skip anything that needs an F1TENTH car, and skip the course's submission and autograder steps; hardware work is done on the LIMO Pro.

1. [Introduction to ROS 2](https://github.com/f1tenth/f1tenth_lab1_template): packages, nodes, and launch files
2. [Automatic Emergency Braking](https://github.com/f1tenth/f1tenth_lab2_template): LiDAR and collision detection
3. [Wall Following](https://github.com/f1tenth/f1tenth_lab3_template): PID control
4. [Follow the Gap](https://github.com/f1tenth/f1tenth_lab4_template): reactive obstacle avoidance. Skip the real-car video.
5. [SLAM and Pure Pursuit](https://github.com/f1tenth/f1tenth_lab5_template): do pure pursuit on an existing simulator map, using the simulator's ground-truth pose. Skip the on-car mapping and particle filter; you will map and localize on the LIMO Pro.
6. [Motion Planning](https://github.com/f1tenth/f1tenth_lab6_template): *optional*. Skip the on-car video.

For perception or vision work, choose additional labs with Yuntao Li.

## 8. LIMO Pro Robot

The robot runs **ROS 2 Foxy**. Use the [LIMO Pro ROS 2 Foxy manual](https://github.com/agilexrobotics/limo_pro_doc/blob/master/Limo%20Pro%20Ros2%20Foxy%20user%20manual%28EN%29.md). Study these chapters in order:

1. **Ch. 1 LIMO Introduction:** specifications, mode switching, operation, and remote desktop
2. **Ch. 2 Chassis Electrical Information:** battery, charging, and safety precautions
3. **Ch. 3–4 Chassis Driver and Kinematics:** starting the chassis, motion modes, and keyboard control
4. **Ch. 5 LiDAR Mapping**
5. **Ch. 6 LiDAR Navigation:** localization and navigation
6. **Ch. 7–8, as needed:** depth camera mapping and vision

**Robot safety:**

- Fully go through Chapters 1–4 before you operate the physical robot, so you understand how to operate it safely.
- Charge the battery outside the robot: turn the robot off, remove the battery, and use only the original charger. Keep an eye on it while it charges, and never leave it charging unattended.
- When charging is done, or if you need to leave, unplug the battery from the charger first, then unplug the charger from the wall.

**Moving your code from Humble to the robot:**

- Port and test your code on Foxy first, for example in a `ros:foxy` Docker container. Parameters, launch files, and navigation settings may need changes.
- Use Foxy on any computer that connects to the robot (for example, to run RViz). Different ROS 2 versions are not guaranteed to work together.
- Compare the command interface, coordinate frames, vehicle geometry, drive mode, and sensors with your simulation setup.
- Skip the ROS 1 commands in the manual's appendices.
- For source code, see the [`foxy` branch of limo_ros2](https://github.com/agilexrobotics/limo_ros2/tree/foxy). The workspace already on the robot (`~/limo_ros2_ws`) is the version to follow; the repository's default `humble` branch does not match the robot.

---

## Reference (As Needed)

**Robotics background:** read topics when a lab needs them.

- [Modern Robotics](https://hades.mech.northwestern.edu/index.php/Modern_Robotics) (free book): Ch. 2 (configuration space), Ch. 3 (rigid-body motions: rotations and transforms), Ch. 13 (wheeled mobile robots)
- [Planning Algorithms](https://lavalle.pl/planning/): discrete and sampling-based planning, for the Motion Planning lab
- [MIT 18.06 Linear Algebra](https://ocw.mit.edu/courses/18-06-linear-algebra-spring-2010/): vectors, matrices, and linear systems

**ROS 1:** only for reading older code.

- [ROS 1 tutorials](https://wiki.ros.org/ROS/Tutorials) (archived). Key differences: catkin_make → colcon build, catkin → ament, rosrun → ros2 run, roslaunch → ros2 launch, rospy → rclpy.

---

*Links checked September 12, 2026.*
