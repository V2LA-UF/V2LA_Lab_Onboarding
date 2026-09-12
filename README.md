# V2LA Lab Onboarding

A step-by-step guide for undergraduate research interns in robotics and autonomous systems.

**Your path:** Lab access → Ubuntu & Docker → LaTeX → ROS 2 → F1TENTH simulator → Driving labs → LIMO Pro robot

## ROS 2 Versions

- **Learning and simulation (Sections 3–7):** use **ROS 2 Humble on Ubuntu 22.04**.
- **LIMO Pro robot (Section 8):** the robot runs **ROS 2 Foxy on Ubuntu 20.04**. You will port and test your code on Foxy before running it on the robot.
- Always use the documentation that matches the ROS 2 version you are running.

---

## 1. Get Lab Access

Submit the [Building Access Request Form](https://www.eng.ufl.edu/facilities/service-requests/building-access-request-form/):

- **Request type:** Electronic Door Access
- **Building:** Malachowsky Hall
- **Access:** Exterior Doors and Lab 5225
- **Supervisor/Professor:** Dung Tran

Have your UFID ready.

**In the lab:**

- No food or drinks.
- Study and work quietly so you don't disturb others.
- Follow the robot safety rules in [Section 8](#8-limo-pro-robot).

## 2. Weekly Routine

**Contacts:** Yuntao Li ([yli17@ufl.edu](mailto:yli17@ufl.edu)) and Dr. Dung Tran ([dungtran@ufl.edu](mailto:dungtran@ufl.edu))

- **Work schedule:** Share your working schedule with Yuntao Li in advance, so we know when you will be in the lab, can plan discussions with you, and can coordinate lab space if needed.
- **Progress notes:** Keep your own Overleaf project with detailed updates: what you studied, what you built, results, and errors. Share the project with Yuntao Li (yli17@ufl.edu).
- **Email update:** Before each meeting, send a brief update to Yuntao Li and Dr. Tran.
- **Weekly meeting:** Every **Tuesday at 1:00 pm** in the lab, **Malachowsky Hall 5225**. Bring one result to show and any questions you are stuck on.

## 3. Ubuntu, Virtual Machines, and Docker

Set up Ubuntu 22.04 in one of two ways:

- **Virtual machine:** Install Ubuntu 22.04, then [install ROS 2 Humble](https://docs.ros.org/en/humble/Installation.html).
- **Docker:** Run ROS 2 inside a container, starting from the [`osrf/ros:humble-desktop`](https://hub.docker.com/r/osrf/ros) image, which includes RViz and turtlesim. Apps with windows need display forwarding (X11) to appear from a container.

**Newer Macs (M1 or later):** setup works differently. The Ubuntu and Docker images linked here are built for Intel/AMD computers, so look for ARM64 versions instead.

Resources:

- [Run Ubuntu in VirtualBox](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox), using the [Ubuntu 22.04 image](https://releases.ubuntu.com/jammy/)
- [Docker: Get started](https://docs.docker.com/get-started/introduction/): containers, images, and Compose
- [Install Docker on Ubuntu](https://docs.docker.com/engine/install/ubuntu/), then the [post-install steps](https://docs.docker.com/engine/install/linux-postinstall/) to run without `sudo`. On Windows or Mac, install [Docker Desktop](https://docs.docker.com/desktop/) instead.

## 4. LaTeX and Overleaf

- [Learn LaTeX in 30 minutes](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes)
- [Overleaf documentation](https://www.overleaf.com/learn): look up topics as needed

## 5. ROS 2 Humble

Complete these [Humble tutorials](https://docs.ros.org/en/humble/Tutorials.html) in order:

1. [Beginner: CLI tools](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools.html): nodes, topics, services, parameters, launch, and bags
2. [Beginner: Client libraries](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries.html): workspaces, packages, colcon, publishers, and subscribers (use Python)
3. [tf2](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Tf2-Main.html): coordinate frames and transforms

## 6. F1TENTH Simulator

- [F1TENTH Gym ROS 2 bridge, `dev-humble` branch](https://github.com/f1tenth/f1tenth_gym_ros/tree/dev-humble) (**start here**): install (native or Docker), launch, drive, and connect your own node. The `main` branch is for Foxy.
- [Course documentation](https://f1tenth-coursekit.readthedocs.io/en/latest/): lectures and assignments (now named RoboRacer)
- [Lab starter code](https://github.com/f1tenth/f1tenth_labs_openrepo)

## 7. Autonomous Driving Labs

For each lab, read the handout and lecture, then complete the **simulation** part. Skip F1TENTH hardware instructions; hardware work is done on the LIMO Pro.

1. [Introduction to ROS 2](https://f1tenth-coursekit.readthedocs.io/en/latest/assignments/labs/lab1.html)
2. [Automatic Emergency Braking](https://f1tenth-coursekit.readthedocs.io/en/latest/assignments/labs/lab2.html): LiDAR and collision detection
3. [Wall Following](https://f1tenth-coursekit.readthedocs.io/en/latest/assignments/labs/lab3.html): PID control
4. [Follow the Gap](https://f1tenth-coursekit.readthedocs.io/en/latest/assignments/labs/lab4.html): reactive obstacle avoidance
5. [SLAM and Pure Pursuit](https://f1tenth-coursekit.readthedocs.io/en/latest/assignments/labs/lab5.html): waypoint following on an existing simulator map
6. [Motion Planning](https://f1tenth-coursekit.readthedocs.io/en/latest/assignments/labs/lab6.html): *optional*

Lab numbers differ between course versions, so match starter code by topic. For perception or vision work, choose labs from the [lab index](https://f1tenth-coursekit.readthedocs.io/en/latest/assignments/labs/index.html) with your mentor.

## 8. LIMO Pro Robot

The robot runs **ROS 2 Foxy**. Use the [LIMO Pro ROS 2 Foxy manual](https://github.com/agilexrobotics/limo_pro_doc/blob/master/Limo%20Pro%20Ros2%20Foxy%20user%20manual%28EN%29.md). Study in order:

1. Overview, operation, and motion modes
2. Chassis driver, startup, teleoperation, and sensors
3. Mapping
4. Localization and navigation

Robot safety:

- Fully go through the manual sections above before you operate the physical robot, so you understand how to operate it safely.
- Charge the battery with everything else disconnected, and keep an eye on it while it charges.
- If you leave, unplug the charger first. Never leave the battery charging unattended.

Moving your code from Humble to the robot:

- Port and test your code on Foxy first, for example in a `ros:foxy` Docker container. Parameters, launch files, and navigation settings may need changes.
- Use Foxy on any computer that connects to the robot (for example, to run RViz). Different ROS 2 versions are not guaranteed to work together.
- Compare the command interface, coordinate frames, vehicle geometry, drive mode, and sensors with your simulation setup.
- Skip the ROS 1 commands in the manual's appendices.
- The [limo_ros2 repository](https://github.com/agilexrobotics/limo_ros2) targets Humble. Use it for reference only, and deploy with the lab's Foxy version.

---

## Reference (As Needed)

**Robotics background:** read topics when a lab needs them.

- [Modern Robotics](https://modernrobotics.northwestern.edu/nu-gm-book-resource/): Ch. 2 (configuration space), Ch. 3 (rotations and transforms), Ch. 13 (wheeled robots)
- [Planning Algorithms](https://lavalle.pl/planning/): discrete and sampling-based planning, for the Motion Planning lab
- [MIT 18.06 Linear Algebra](https://ocw.mit.edu/courses/18-06-linear-algebra-spring-2010/): vectors, matrices, and linear systems

**ROS 1:** only for reading older code.

- [ROS 1 tutorials](https://wiki.ros.org/ROS/Tutorials). Key differences: catkin → colcon, roslaunch → ros2 launch, rospy → rclpy.

---

*Links checked September 11–12, 2026.*
