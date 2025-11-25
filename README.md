# ROS2 JAZZY

Trong hướng dẫn này sẽ thực hành những kiến thức cơ bản của ROS2 nhưng với hướng tiếp cận sâu hơn về robot, làm việc với robot.

## 1. Tạo work space

Mở terminal và nhập lệnh sau để tạo 1 workSpace
```bash
mkdir -p 01.work_space/20.ROS2_TRAINING/src
```
build
```bash
colcon build
```
khi này trong thư mục làm việc sẽ có các folder sau nhưng kệ nó
```bash
dev@Embedded:~/01.work_space/20.ROS2_TRAINING$ ls
build  install  log  src
```
kiểm tra phụ thuộc
```bash
rosdep install -i --from-path src --rosdistro jazzy -y
```
nếu trên terminal hiện lên dòng "#All required rosdeps installed successfully" là xong

## 2. Mô tả robot bằng sdf trong GAZEBO
Trước khi tìm hiểu xem ROS là cái gì, dùng làm gì thì ta sẽ học các mô phỏng robot của chính chúng ta trước
Trong thư mục src của workSpace đã tạo tạo ra 1 thư mục để chứa các file mô tả
```bash
mkdir -p  01.gz_sim/meshes
```
```bash
cd 01.gz_sim/
```
Tạo file mô tả:
```bash
touch myrobot.sdf
```
truy cập vào đường link sau và copy code trong đó paste vào trong file myrobot.sdf

```bash
https://github.com/Lam-Embedded/Gazebo-2-wheel-differential-robot-simulator/blob/main/building_robot.sdf
```
Sau khi paste xong thì thử chạy mô phỏng trong gazebo xem hình dạng của robot thế nào:
Mở terminal vào trong thư mục chứa file myrobot.sdf
```bash
cd 01.work_space/20.ROS2_TRAINING/src/01.gz_sim/
```
chạy lệnh sau để mô phỏng:
```bash
gz sim myrobot.sdf
```
Đây sẽ là mô hình robot 2 bánh vi sai đơn giản của chúng ta:
![alt text](image/image.png)

Trong đó cấu trúc cơ bản của 1 file sdf mô tả robot như sau:
```bash
<?xml version="1.0" ?>
<sdf version="1.8">
    <world name="Moving_robot">
    ...
    ...
    </world>
</sdf>
```
Mọi thứ sẽ được viết bên trong thẻ <world> </world>
Trước tiên là tạo 1 thế giới cơ bản:
```bash
<?xml version="1.0" ?>
<sdf version="1.8">
    <world name="Moving_robot">
        <physics name="1ms" type="ignored">
            <max_step_size>0.001</max_step_size>
            <real_time_factor>1.0</real_time_factor>
        </physics>
        <plugin
            filename="gz-sim-physics-system"
            name="gz::sim::systems::Physics">
        </plugin>
        <plugin
            filename="gz-sim-user-commands-system"
            name="gz::sim::systems::UserCommands">
        </plugin>
        <plugin
            filename="gz-sim-scene-broadcaster-system"
            name="gz::sim::systems::SceneBroadcaster">
        </plugin>

        <light type="directional" name="sun">
            <cast_shadows>true</cast_shadows>
            <pose>0 0 10 0 0 0</pose>
            <diffuse>0.8 0.8 0.8 1</diffuse>
            <specular>0.2 0.2 0.2 1</specular>
            <attenuation>
                <range>1000</range>
                <constant>0.9</constant>
                <linear>0.01</linear>
                <quadratic>0.001</quadratic>
            </attenuation>
            <direction>-0.5 0.1 -0.9</direction>
        </light>

        <model name="ground_plane">
            <static>true</static>
            <link name="link">
                <collision name="collision">
                <geometry>
                    <plane>
                    <normal>0 0 1</normal>
                    </plane>
                </geometry>
                </collision>
                <visual name="visual">
                <geometry>
                    <plane>
                    <normal>0 0 1</normal>
                    <size>100 100</size>
                    </plane>
                </geometry>
                <material>
                    <ambient>0.8 0.8 0.8 1</ambient>
                    <diffuse>0.8 0.8 0.8 1</diffuse>
                    <specular>0.8 0.8 0.8 1</specular>
                </material>
                </visual>
            </link>
        </model>
    </world>
</sdf>
```































