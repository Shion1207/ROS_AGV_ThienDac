# agv_ros

ROS 2 package cho mô hình AGV dùng URDF, mesh STL, launch file cho RViz2/Gazebo, và một số script điều khiển cơ bản.

File mô hình chính hiện tại là `urdf/demo2.urdf`. File này được giữ nguyên, không chỉnh sửa trong phần sắp xếp repo này.

## Cấu trúc chính

```text
agv_ros/
├── CMakeLists.txt
├── package.xml
├── config/
├── launch/
├── maps/
├── meshes/
├── scripts/
└── urdf/
    ├── demo2.urdf
    └── demo2.csv
```

## Những gì đang có trong package

- `urdf/demo2.urdf`: mô hình robot chính.
- `meshes/`: các file STL được tham chiếu trong URDF qua `package://agv_ros/...`.
- `launch/display.launch.py`: hiển thị robot với `robot_state_publisher`, `joint_state_publisher_gui`, `rviz2`.
- `launch/gazebo_display.launch.py`: spawn robot trong Gazebo.
- `scripts/`: script teleop và điều khiển cơ bản.

## Kiểm tra nhanh file URDF

Qua kiểm tra cấu trúc:

- URDF hợp lệ về mặt tổ chức file trong package ROS 2.
- Mesh đang được tham chiếu theo dạng `package://agv_ros/meshes/...`, phù hợp với cấu trúc hiện tại.
- Package đã cài đặt các thư mục `config`, `launch`, `maps`, `meshes`, `urdf` trong `CMakeLists.txt`, nên layout hiện tại có thể dùng để build/chạy.

## Chạy robot len Rviz va Gazebo

Spkill -f gzserver
pkill -f gzclient
cd ~/ros2_ws
colcon build --packages-select agv_ros --symlink-install
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 launch agv_ros gazebo_display.launch.py

## Chạy robot len Rviz va Gazebo

Chạy với Gazebo:

```bash
source install/setup.bash
ros2 launch agv_ros gazebo_display.launch.py
```
## Mecanum controller

cd ~/ros2_ws
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 run agv_ros mecanum_keyboard_teleop.py

## Arms controller

cd ~/ros2_ws
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 run agv_ros arm_teleop.py


## Cam view

cd ~/ros2_ws
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 run rqt_image_view rqt_image_view

## GPS

cd ~/ros2_ws
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 topic echo /gps/data


## SLAM Scan map

cd ~/ros2_ws
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 launch agv_ros slam_hexagon.launch.py

## Đưa lên GitHub

Repo này nên đưa lên cùng các thư mục nguồn:

- `config/`
- `launch/`
- `maps/`
- `meshes/`
- `scripts/`
- `urdf/`
- `CMakeLists.txt`
- `package.xml`
- `README.md`

Không nên đưa các thư mục sinh ra khi build như `build/`, `install/`, `log/`.
