# Installing ROS 2 Foxy Fitzroy

This guide covers the installation of ROS 2 Foxy Fitzroy on Ubuntu 20.04 (Focal Fossa) environment[^1].

## Prerequisites

- **Ubuntu 20.04 (Focal Fossa)** environment
- Enabled `Main` and `Universe` repositories in Ubuntu Repositories
  > Main and Universe repositories are usually enabled by default when installing Ubuntu. If they are not enabled, or not sure if they are enabled, follow the next instruction to ensure they are enabled

- Setting Locale to `UTF-8`
  > Most regions use UTF-8 Encoding, if not sure, follow the instructions for it to ensure that Ubuntu usses UTF-8 Encoding

### Enabling repositories in Ubuntu

#### Using the Graphical Interface

1. **Open Software & Updates:**
   - Go to Activities and search for "Software & Updates."
   - Click on the "Software & Updates" application.

2. **Enable Repositories:**
   - Under the **Ubuntu Software** tab, you will see options for different repositories:
     - **Main:** Free and open-source software supported by Canonical.
     - **Universe:** Community-maintained free and open-source software.
     - **Restricted:** Proprietary drivers and firmware.
     - **Multiverse:** Software that is not free.
   - Check the boxes next to the repositories you want to enable.

3. **Update the Package List:**
   - After enabling the repositories, click **Close**.
   - You will be prompted to reload the package information. Click **Reload**.

#### Using the Command Line Interface

1. **Open a Terminal:**
   - Press `Ctrl + Alt + T` to open a terminal if using a GUI like GNOME.

2. **Enable the Repositories:**
   - If you don't have `software-properties-common`, or not sure if you have it, install it using:

     ```bash
     sudo apt install software-properties-common
     ```

   - Run the following commands to enable each repository:

     ```bash
     sudo add-apt-repository main
     sudo add-apt-repository restricted
     sudo add-apt-repository universe
     sudo add-apt-repository multiverse
     ```

3. **Update the Package List:**
   - After enabling the repositories, update your package list:

     ```bash
     sudo apt update
     ```

### Setting Locale to UTF-8

- To check if `locale` is set to `UTF-8`, run

   ```bash
   locale
   ```

- If it's not set, or if you don't have the locale configured, run the following commands to ensure your locale is set to `UTF-8`.

   ```bash
   sudo apt update && sudo apt install locales
   sudo locale-gen en_US en_US.UTF-8
   sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
   export LANG=en_US.UTF-8
   ```

## Installing ROS 2

1. Install Dependencies:

   ```bash
   sudo apt update && sudo apt upgrade
   sudo apt install curl -y
   ```

2. Add ROS 2 Repository:
   - Import the ROS 2 GPG key:

     ```bash
     sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
     ```

   - Add the ROS 2 repository to your sources list:
  
     ```bash
     echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
     ```

3. Install ROS 2 Foxy (for Ubuntu 20.04):

    ```bash
    sudo apt update && sudo apt upgrade
    sudo apt install ros-foxy-desktop python3-argcomplete
    sudo apt install ros-dev-tools
    ```

4. Sourcing the setup script, depending of what shell you are using, to run `ros2` commands.

    To check what shell is beeing used, run:

    ```bash
    echo $SHELL
    ```

    - For `bash` shell, run:

      ```bash
      source /opt/ros/foxy/setup.bash
      ```

    - For `sh` shell, run:

      ```bash
      source /opt/ros/foxy/setup.sh
      ```

    - For `zsh` shell, run:

      ```bash
      source /opt/ros/foxy/setup.zsh
      ```

> [!NOTE]
> The command `source /opt/ros/foxy/setup.bash` is used to configure your shell environment to work with a ROS Foxy. You need to run the command each time you open a new terminal session or each time you start a new shell that needs a ROS environment configuration.

## Configure ROS Command to Start With Your Shell Environment

> [!TIP]
> To avoid having to manually run this command every time you open a new terminal, you can automate it by adding it to your shell’s startup files. Follow the following set of instructions to do that.

- For `Bash` Shell, add the command to your `.bashrc` file:

  ```bash
  echo "source /opt/ros/foxy/setup.bash" >> ~/.bashrc
  source ~/.bashrc
  ```

- For `Sh` Shell, add the command to your `.shrc` file:

   ```sh
   echo "source /opt/ros/foxy/setup.sh" >> ~/.shrc
   source ~/.zshrc
   ```

- For Zsh Shell, add the command to your `.zshrc` file:

   ```zsh
   echo "source /opt/ros/foxy/setup.zsh" >> ~/.zshrc
   source ~/.zshrc
   ```

## Uninstalling ROS 2

- If you need to uninstall ROS 2 or switch to a source-based installation, run the following commands:

  ```bash
  sudo apt remove ~nros-foxy-* && sudo apt autoremove
  ```

- To remove the ROS 2 Repository, run the following commands:

  ```bash
  sudo rm /etc/apt/sources.list.d/ros2.list
  sudo apt update
  sudo apt autoremove
  sudo apt upgrade
  ```

[^1]: Those set of instructions are based on the official installation instruction for ROS 2 Foxy as of 08/28/2024 > https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html
