# Extended Kalman Filteri Uygulama 2

 https://github.com/dikioth/autoROS/tree/23398ca4315858122633be69a3eec7691d1fdfc3  --> bu githup reposu referans alınmıştır.
 
 ## 1 
 
 Kendi oluşturduğumuz labirent ortamda turtlebot3'ü kullandık.
 
 > roslaunch kalman_uygulama_2 klm_ortam.launch


![2gazebo](https://user-images.githubusercontent.com/59619952/223945175-41d7cd3f-2f51-4db0-a3cd-a6c0e6355e32.png)


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

## 3

> python3 ekf_node_with_twist.py

or

> roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch 
> python3 ekf_node.py







 
 
