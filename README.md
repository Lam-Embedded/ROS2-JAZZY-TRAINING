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
nếu trên terminal hiện lên dòng '''#All required rosdeps installed successfully''' là xong

