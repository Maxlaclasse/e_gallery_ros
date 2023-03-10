command for convertir xacro into urdf :
rosrun xacro xacro ~/dev_ws/src/e_gallery_ros/description/robot.urdf.xacro > ~/dev_ws/src/e_gallery_ros/description/robot.urdf

for slam_toolbox roslaunch slam_toolbox online_async.launch params_file:=./src/e_gallery_ros/config/mapper_params_online_async.yaml use_sim_time:=true 2> >(grep -v TF_REPEATED_DATA buffer_core)

<?xml version="1.0"?>
<robot xmlns:xacro="http://www.ros.org/wiki/xacro">

    <xacro:include filename="inertial_macros.xacro" />

    <material name="white">
        <color rgba="1 1 1 1"/>
    </material>

    <material name="orange">
        <color rgba="1 0.3 0.1 1"/>
    </material>

    <material name="blue">
        <color rgba="0.2 0.2 1 1"/>
    </material>

    <material name="black">
        <color rgba="0 0 0 1"/>
    </material>

<!-- BASE LINK -->
    <link name="base_link">

    </link>
<!-- CHASSIS LINK -->
    <joint name="chassis_joint" type="fixed">
        <parent link="base_link"/>
        <child link="chassis"/>
        <origin xyz="-0.1 0 0"/>
    </joint>

    <link name="chassis">
        <visual>
            <origin xyz="0.15 0 0.03" rpy="0 0 0"/>
            <geometry>
                <cylinder length="0.015" radius="0.19" />
            </geometry>
            <material name="white"/>
        </visual>
        <collision>
            <origin xyz="0.15 0 0.03" rpy="0 0 0"/>
            <geometry>
                <cylinder length="0.005" radius="0.19" />
            </geometry>
        </collision>
        <xacro:inertial_box mass="0.5" x="0.3" y="0.3" z="0.15">
            <origin xyz="0.15 0 0.03" rpy="0 0 0"/>
        </xacro:inertial_box>
    </link>

    <gazebo reference="chassis">
        <material>Gazebo/White</material>
    </gazebo>
<!-- LEFT WHEEL LINK -->
    <joint name="left_wheel_joint" type="continuous">
        <parent link="base_link"/>
        <child link="left_wheel"/>
        <origin xyz="-0.02 0.125 0" rpy="-${pi/2} 0 0"/>
        <axis xyz="0 0 1"/>
    </joint>

    <link name="left_wheel">
        <visual>
            <geometry>
                <cylinder length="0.025" radius="0.0325" />
            </geometry>
            <material name="blue"/>
        </visual>
        <collision>
            <geometry>
                <cylinder length="0.025" radius="0.0325" />
            </geometry>
        </collision>
        <xacro:inertial_cylinder mass="0.1" length="0.025" radius="0.0325">
            <origin xyz="0 0 0" rpy="0 0 0"/>
        </xacro:inertial_cylinder>
    </link>

    <gazebo reference="left_wheel">
        <material>Gazebo/Blue</material>
    </gazebo>
<!-- RIGHT WHEEL LINK -->

    <joint name="right_wheel_joint" type="continuous">
        <parent link="base_link"/>
        <child link="right_wheel"/>
        <origin xyz="-0.02 -0.125 0" rpy="${pi/2} 0 0"/>
        <axis xyz="0 0 -1"/>
    </joint>

    <link name="right_wheel">
        <visual>
            <geometry>
                <cylinder length="0.025" radius="0.0325" />
            </geometry>
            <material name="blue"/>
        </visual>
        <collision>
            <geometry>
                <cylinder length="0.025" radius="0.0325" />
            </geometry>
        </collision>
        
        <xacro:inertial_sphere mass="0.1" radius="0.325">
            <origin xyz="0 0 0" rpy="0 0 0"/>
        </xacro:inertial_sphere>
    </link>
    <gazebo reference="right_wheel">
        <material>Gazebo/Blue</material>
    </gazebo>

<!-- CASTER WHEEL LINK -->

    <joint name="caster_wheel_joint" type="fixed">
        <parent link="chassis"/>
        <child link="caster_wheel"/>
        <origin xyz="0.25 0 0" rpy="0 0 0"/>
    </joint>

    <link name="caster_wheel">
        <visual>
            <geometry>
                <sphere radius="0.0325" />
            </geometry>
            <material name="black"/>
        </visual>
        <collision>
            <geometry>
                <sphere radius="0.0325" />
            </geometry>
        </collision>
    </link>
    <gazebo reference="caster_wheel">
        <material>Gazebo/Black</material>
        <mu1 value="0"/>
        <mu2 value="0"/>

    </gazebo>

</robot>
