# Gazebo Simulation Environment for Underwater Robots Control Validation

This repository provides the Gazebo simulation environment required to perform control validation and testing for various Underwater Robots controllers. It is not a standalone project; instead, it serves as the common simulation platform for the following three controller implementations:
* [IBVS-UKF Observer](https://github.com/DEEP-UNDER-ROV/IBVS_Observer-based_Controller/tree/FIFISH)
* [Obstacle-avoidance](https://github.com/m4ttroy/obstacle_avoidance)
* [ROMV Formation Control](https://github.com/m4ttroy/romv)


## Requirements

Please ensure that the following requirements have been met prior to installing the gazebo simulation environment

* [Gazebo Harmonic](https://gazebosim.org/docs/harmonic/install)
* [ardupilot_gazebo for Harmonic](https://github.com/ArduPilot/ardupilot_gazebo)
* [ArduSub and MAVProxy](https://ardupilot.org/dev/docs/building-setup-linux.html)
* [MAVROS](https://github.com/mavlink/mavros/blob/ros2/docs/installation.md)


## Running Gazebo Simulation

A dedicated launch file have been created to run the prefered simulation

~~~bash
ros2 launch supri_sim.launch.xml  # Run the IBVS-UKF using SUPRI model
ros2 launch rov_sim.launch.xml    # Run the obstacle-avoidance control using BlueROV2 model with FLS ping-sonar
ros2 launch romv_sim.launch.xml   # Run ROMV Formation Control with 3 ROVs using BlueROV2 model
~~~

Each launch file runs 3 commands simultaneously; gz sim, MAVLink, and MAVROS<br>
N.B. SUPRI simulation still under numerous bugs due to different frame configuration, which needs different SITL model in [Ardusupri](https://github.com/DEEP-UNDER-ROV/Ardusupri)


## GZ Topic to ROS2 Bridge 

This are the following topics recorded for offline analysis

| Topic                | Description                     |
| -------------------- | ------------------------------- |
| `/model/rov/pose`    | ROV pose in world coordinate    |
| `/model/rov/odom`    | ROV odom in body coorinate      |
| `/model/rov/sonar`   | Ping-sonar data readings        |
| `/model/rov/imu`     | FCU IMU sensor data             |

for ROMV, the topics become /model/rov_x/topics with rov_x are the assigned id 0 (Central ROV), 1-n (Slave ROVs)

## References

* https://github.com/ardupilot/ardupilot_gazebo/wiki
* https://github.com/clydemcqueen/bluerov2_gz
* https://ardupilot.org/dev/docs/building-setup-linux.html
* https://ardupilot.org/dev/docs/setting-up-sitl-on-linux.html
* https://ardupilot.org/mavproxy/docs/getting_started/download_and_installation.html
* https://www.ardusub.com/developers/rc-input-and-output.html