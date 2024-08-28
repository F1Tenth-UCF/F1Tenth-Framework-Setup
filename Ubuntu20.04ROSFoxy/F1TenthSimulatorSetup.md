# Setting Up F1Tenth Gym ROS

This guide walks you through configuring your system to set up the F1Tenth Gym ROS environment.[^1].

-- *Last Tested: 08/28/2024*

## Prerequisites

- **Ubuntu 20.04 (Focal Fossa)** environment
- **ROS 2 Foxy Fitzroy**
- **Python 3** *(Comes with Ros 2 Foxy Flitzroy)*

## System preparation

1. **Update and Upgrade System Packages:**

   ```bash
   sudo apt update && sudo apt upgrade
   ```

2. **Install Pip for Python 3:** *(if not already installed)*

   ```bash
   sudo apt install python3-pip
   ```

## Setting Up F1tenth Gym

1. **Navigate to the Home Folder or Desired Directory:**

   ```bash
   cd $HOME
   ```

2. **Clone the F1Tenth Gym Repository:**

   ```bash
   git clone https://github.com/f1tenth/f1tenth_gym
   cd f1tenth_gym
   ```

3. **Install the Python Dependencies For the F1Tenth Gym:**

   ```bash
   pip3 install -e .
   ```

## Setting Up ROS Environment for F1tenth Gym

1. **Create a Workspace:**

   ```bash
   cd $HOME && mkdir -p sim_ws/src
   ```

2. **Clone the F1Tenth Gym ROS Repository into the Workspace:**

   ```bash
   cd $HOME/sim_ws/src
   git clone https://github.com/f1tenth/f1tenth_gym_ros
   ```

3. **Confirm/Update the Map Path Parameter:**

    - Open the `sim.yaml` file located in your cloned repository at `config/sim.yaml`.
    - Change the map_path parameter to point to the correct location:

      ```bash
      map_path: "<your_home_dir>/sim_ws/src/f1tenth_gym_ros/maps/levine"
      ```

4. **Initialize and Update `rosdep`:**

   ```bash
   sudo rosdep init
   rosdep update --include-eol-distros
   ```

5. **Navigate to the Top Level of the Simulation Workspace Folder `sim_ws` and Install ROS Dependencies:**

   ```bash
   rosdep install -i --from-path src --rosdistro foxy -y
   ```

6. **Build The Workspace**

   ```bash
   colcon build
   ```

## Run the Simulation Environment

1. **Source the ROS 2 Setup Script if not Already Sourced**

   ```bash
   source /opt/ros/foxy/setup.bash
   ```

2. **Navigate to the Top Level of the Simulation Workspace Folder `sim_ws`and Source the Local Workspace Setup Script:**

   ```bash
   source install/local_setup.bash
   ```

3. **Run the Simulation Environment**

   ```bash
   ros2 launch f1tenth_gym_ros gym_bridge_launch.py
   ```

   **An rviz window should pop up showing the simulation**

[^1]: Those set of instructions are based on the [Installation Instruction](https://github.com/f1tenth/f1tenth_gym_ros) for F1Tenth Gym ROS Simulation as of 08/28/2024
