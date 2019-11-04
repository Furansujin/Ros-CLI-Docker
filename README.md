# Ros-CLI-Docker
Use Ros in Docker just by command Line


We will start by creating a workspace to contain our project.

Open a terminal, move to a working directory, for example ros (not necessarily the same as for the construction of the Docker image ) and execute the following command to create the skeleton of the workspace directory:

```console
$ mkdir -p workspace/src
```

We will then create a package that will be named after the example of the official documentation. The package creation with ROS is done from the tool catkin_create_pkg . To create a beginner_tutorials package when ROS is installed natively on your system, you would have done this: $ catkin_create_pkg beginner_tutorials std_msgs rospy . We will now invoke the same command using our ROS Docker image .

From the same terminal, enter the following command line:

```console
$ docker run --rm -it -e WORKSPACE_NAME=workspace -v $(pwd)/workspace:/root/workspace -w /root/workspace/src ros:mykinetic catkin_create_pkg beginner_tutorials std_msgs rospy
```

First observation, this command is longer than the previous one. We notice at the end of this long command the following content catkin_create_pkg beginner_tutorials std_msgs rospy which is the same as the command we would have invoked without Docker to create a package. Let's unpack the rest of the new Docker- specific command  : docker is the tool for creating containers; run indicates that a container must be created; --rm specifies that the container will be automatically destroyed when it stops; -itallows to use the interactive mode on the current tty, basically, otherwise we would not have the return of the terminal and we could not enter additional commands if needed; -e WORKSPACE \ _NAME = workspace creates an environment variable called WORKSPACE \ _NAME with workspace value  ; -v $ (pwd) / workspace: / root / workspace creates a volume that is a shared folder of $ (pwd) / workspace of the host system with the folder / root / workspace of the container; -w / root / workspace / src forces the current directory from the container, any interaction will be done from this directory; finally ros: mykineticis the name of the image that Docker will use to create the container.

In the rest of our experiments, a command pattern identical to this one will be used: $ docker + OPTIONS_DOCKER + rosTool + OPTIONS_ROS . The first part will almost never change, only rosTool + OPTIONS_ROS will be adapted according to the actions to perform.