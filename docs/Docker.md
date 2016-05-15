
# Install Docker

Docker installation from any Linux distro is fairly straightforward. After installing Docker on Linux skip to `Installing ROS on Docker`. Use the relevant package manager to install Docker. Installation of Docker on Windows using Virtualbox is fairly straightforward. If you're using a mostly unmodified version of Windows you can skip to `Start Docker on Windows`. If someone has already installed and activated Hyper-V on your Windows installation then you'll need to proceed to `Configuring Hyper-V`.

## Configuring Hyper-V

In order to install Docker using Hyper-V the current user must be added to the `Hyper-V administrators` group. To do this on Windows 8.1, right click on the start icon and choose `Computer Management`. In the tree on the left side of the `Computer Management` window expand `Local Users and Groups` and click on `Groups`. In the list to the right that results double-click on `Hyper-V Administrators`. In the prompt that appears select `Add...`. In the `Select Users` prompt enter your user name into the provided text box. Select `OK` in the `Select Users` and `Hyper-V Administrators Properties` prompts. Close the `Computer Management` window. Finally, restart the computer to make the changes take effect.

Next, start a Git-Bash prompt and create the docker machine using the commands below:

```bash
docker-machine create --driver hyperv default
```

Verify that the machine was created by running this command:

```bash
docker-machine ls
```

Continue onto the instructions in the `Configuring a command prompt` section.

### Configuring a command prompt

In order to manually enable a running prompt to use the newly created docker machine you can run the commands below for the relevant shells:

#### Command Prompt
```cmd
@FOR /f "tokens=*" %i IN ('docker-machine env default'
```

#### Power Shell
```powershell
docker-machine env default | Invoke-Expression
```

#### Git-Bash
```bash
eval $(docker-machine env default)
```

### Modifying the Docker Quickstart script

The default Docker Quickstart script is configured to use Virtualbox and will fail if Hyper-V is running unless it is modified. This script is usually stored at `C:\Program Files\Docker Toolbox\start.sh`. The script should be modified by prefixing the blocks starting with `STEP="Looking for vboxmanage.exe`, `if [ ! -f "${VBOXMANAGE}" ]; then`, `"${VBOXMANAGE}" list vms | grep \""${VM}"\" &> /dev/null`, `set -e`, and `STEP="Checking if machine $VM exists"`. 

The rest of the script should provide everything needed given the name of your docker machine is `default`.

## Start Docker on Windows

Double-click the `Docker Quickstart` icon to start a Git-Bash shell that will be preconfigured for use with the default docker machine. Ensure that the docker machine runs correctly by running `docker run hello-world`.

## Installing ROS on Docker
In a shell configured for use with Docker, run `docker pull ros` and `docker pull osrf/ros:indigo-desktop-full`. Further details are available on the [ROS website](http://wiki.ros.org/docker/Tutorials/Docker). For development purposes the full desktop installation is preferable.

## Installing Gazebo on Docker

The Open Source Robotics Foundation also makes installing Gazebo using Docker possible. Gazebo will provide the environment for our robot to exist within. Gazebo can be installed in Docker by running `docker pull osrf/gazebo:gzserver5`.

## Running ROS in Docker
Run the default ROS container by running `docker run -it osrf/ros:indigo-desktop-full`.
