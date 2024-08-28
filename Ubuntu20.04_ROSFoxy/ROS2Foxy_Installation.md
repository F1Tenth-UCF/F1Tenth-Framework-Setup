# Installing ROS 2 Foxy Fitzroy

This guide covers the installation of ROS 2 Foxy Fitzroy on Ubuntu 20.04 (Focal Fossa) environment.

## Prerequisites

- Ubuntu 20.04 (Focal Fossa) environment
- Enabled 'Main' and 'Universe' repositories in Ubuntu Repositories
- Setting Locale to 'UTF-8'

> [!Note]
>***Main and Universe repositories are usually enabled by default when installing Ubuntu. If they are not enabled, or not sure if they are enabled, follow the next instruction to ensure they are enabled***

***Most regions use UTF-8 Encoding, if not sure, follow the instructions for it to ensure that Ubuntu usses UTF-8 Encoding***

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

## Setting Locale to UTF-8

Ensure your locale is set to `UTF-8`. If it's not set, or if you don't have the locale configured, run the following commands:

```bash
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```
