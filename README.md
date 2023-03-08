# LogicProject

# ROS Kalman Filter for Sensor Fusion

https://fjp.at/posts/ros/ros-kalman-filter/  --> internet sitesi referans alınmıştır.

sensör füzyonu için kullanılabilecek Extended Kalman filtresi uygulayan bir ROS paketinin nasıl oluşturulacağını açıklar. Bir araya getirilecek sensör verileri olarak imu, wheel odometri ve kamera gelir. Geliştirilen ekf paketi, sensör verilerini karşılaştırmak ve hareket ederken robotun duruşunu tahmin etmek için sensör füzyonu uygulamak için kullanılacaktır. Aşağıdaki paketler kullanılmıştır.

Turtlebot3_gazebo, gazeboda mobil robot ortamı başlatır. 
robot_pose_ekf, robotun konumunu ve yönünü tahmin eder. 
odom_to_trajectory, zaman içinde oluşturulan odometri değerlerini bir yörünge yoluna ekler. 
Turtlebot_teleop, klavye komutlarını kullanarak robotu yönlendirmeye izin verir. 
rviz, robotun tahmini konumunu ve yönünü görselleştirmemizi sağlar.

## 1   

> roslaunch turtlebot3_gazebo turtlebot3_world.launch


![gazebo](https://user-images.githubusercontent.com/59619952/223831138-6a453cee-bc01-4dbc-bed6-3b0e6ed59f0d.png)



> rostopic list 
```
/camera/parameter_descriptions
/camera/parameter_updates
/camera/rgb/camera_info
/camera/rgb/image_raw
/camera/rgb/image_raw/compressed
/camera/rgb/image_raw/compressed/parameter_descriptions
/camera/rgb/image_raw/compressed/parameter_updates
/camera/rgb/image_raw/compressedDepth
/camera/rgb/image_raw/compressedDepth/parameter_descriptions
/camera/rgb/image_raw/compressedDepth/parameter_updates
/camera/rgb/image_raw/theora
/camera/rgb/image_raw/theora/parameter_descriptions
/camera/rgb/image_raw/theora/parameter_updates
/clock
/cmd_vel
/gazebo/link_states
/gazebo/model_states
/gazebo/parameter_descriptions
/gazebo/parameter_updates
/gazebo/performance_metrics
/gazebo/set_link_state
/gazebo/set_model_state
/imu
/joint_states
/odom
/rosout
/rosout_agg
/scan
/tf
```

## 2

> roslaunch robot_pose_ekf robot_pose_ekf.launch

```
<launch>

<node pkg="robot_pose_ekf" type="robot_pose_ekf" name="robot_pose_ekf">
  <param name="output_frame" value="odom_combined"/>
  <param name="base_footprint_frame" value="base_footprint"/>
  <param name="freq" value="30.0"/>
  <param name="sensor_timeout" value="1.0"/>  
  <param name="odom_used" value="true"/>
  <param name="imu_used" value="true"/>
  <param name="vo_used" value="false"/>

  <remap from="imu_data" to="/imu" />
  
</node>

</launch>
```

## 3

> roslaunch odom_to_trajectory create_trajectory.launch


![rosgraph2](https://user-images.githubusercontent.com/59619952/223841291-0ce76eb1-8703-461d-a14c-de75853aabaf.png)



## 4 

> roslaunch turtlebot_teleop keyboard_teleop.launch

## 5 

> rosrun rqt_multiplot rqt_multiplot


![rqt_pilot](https://user-images.githubusercontent.com/59619952/223841858-7df9c8ca-adbd-4e2d-bae8-625efe4d4d65.png)


## 6

rviz gelecek

## 7 

bu çalıştırdığımız launch dosyalarını tek bir launch dosyasında toplayarak daha kolay hale getirdik.


```

<launch>
    <include file="$(find turtlebot3_gazebo)/launch/turtlebot3_empty_world.launch" />
    <include file="$(find robot_pose_ekf)/robot_pose_ekf.launch" />
    <include file="$(find odom_to_trajectory)/launch/create_trajectory.launch" />
    <include file="$(find turtlebot3_teleop)/launch/turtlebot3_teleop_key.launch" />
</launch>

```




