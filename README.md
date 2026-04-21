# agv_ros

ROS 2 package cho mo hinh AGV dung URDF, mesh STL, launch file cho RViz2/Gazebo, va mot so script dieu khien co ban.

File mo hinh chinh hien tai la `urdf/demo2.urdf`. File nay duoc giu nguyen, khong chinh sua trong phan sap xep repo nay.

## Cau truc chinh

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

## Nhung gi dang co trong package

- `urdf/demo2.urdf`: mo hinh robot chinh.
- `urdf/demo2.csv`: file du lieu lien quan den mo hinh.
- `meshes/`: cac file STL duoc tham chieu trong URDF qua `package://agv_ros/...`.
- `launch/display.launch.py`: hien thi robot voi `robot_state_publisher`, `joint_state_publisher_gui`, `rviz2`.
- `launch/gazebo_display.launch.py`: spawn robot trong Gazebo.
- `launch/slam_hexagon.launch.py`: chay SLAM.
- `scripts/mecanum_keyboard_teleop.py`: teleop cho de mecanum.
- `scripts/arm_teleop.py`: dieu khien canh tay co ban.

## Kiem tra nhanh file URDF

Qua kiem tra cau truc:

- URDF hop le ve mat to chuc file trong package ROS 2.
- Mesh dang duoc tham chieu theo dang `package://agv_ros/meshes/...`, phu hop voi cau truc hien tai.
- Package da cai dat cac thu muc `config`, `launch`, `maps`, `meshes`, `urdf` trong `CMakeLists.txt`, nen layout hien tai co the dung de build va chay.

## Chay Gazebo va RViz

Lenh duoi day dung de mo Gazebo va RViz voi robot hien tai:

```bash
pkill -f gzserver
pkill -f gzclient
cd ~/ros2_ws
colcon build --packages-select agv_ros --symlink-install
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 launch agv_ros gazebo_display.launch.py
```

## Huong dan su dung

### Mecanum controller

```bash
cd ~/ros2_ws
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 run agv_ros mecanum_keyboard_teleop.py
```

### Arm controller

```bash
cd ~/ros2_ws
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 run agv_ros arm_teleop.py
```

### Camera view

```bash
cd ~/ros2_ws
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 run rqt_image_view rqt_image_view
```

### Du lieu GPS

```bash
cd ~/ros2_ws
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 topic echo /gps/data
```

### Chay SLAM scan map

```bash
cd ~/ros2_ws
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 launch agv_ros slam_hexagon.launch.py
```

### Kiem tra cay TF parent-child

```bash
cd ~/ros2_ws
source install/setup.bash
export ROS_DOMAIN_ID=69
ros2 run tf2_tools view_frames
```

## Dua len GitHub

Repo nay nen dua len cung cac thu muc nguon:

- `config/`
- `launch/`
- `maps/`
- `meshes/`
- `scripts/`
- `urdf/`
- `CMakeLists.txt`
- `package.xml`
- `README.md`

Khong nen dua cac thu muc sinh ra khi build nhu `build/`, `install/`, `log/`.

