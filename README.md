<!--
 * @Author: HCQ
 * @Date: 2020-10-27 10:18:56
 * @LastEditTime: 2020-12-03 11:35:46
 * @LastEditors: Please set LastEditors
 * @Description: 3D-LIDAR Multi Object Tracking for Autonomous Driving（Master论文）
 * @FilePath: /3D-LIDAR-Multi-Object-Tracking/README.md
-->
# 3D-LIDAR-Multi-Object-Tracking
3D-MOT(多目标检测和追踪)  （2020 · 秋）

参考：https://github.com/k0suke-murakami/object_tracking

@[双愚](https://github.com/HuangCongQing/3D-LIDAR-Multi-Object-Tracking) , 若fork或star请注明来源


#### 版本
*[main](https://github.com/HuangCongQing/3D-LIDAR-Multi-Object-Tracking)
*[kitti](https://github.com/HuangCongQing/3D-LIDAR-Multi-Object-Tracking/tree/kitti)



### Intro
This package includes **Ground Removal, Object Clustering, Bounding Box, IMM-UKF-JPDAF, Track Management and Object Classification** for 3D-LIDAR multi object tracking.
The idea is mainly come from this [paper](https://repository.tudelft.nl/islandora/object/uuid:f536b829-42ae-41d5-968d-13bbaa4ec736?collection=education).


代码对应论文：[3D-LIDAR Multi Object Tracking for Autonomous Driving（Master论文）](https://repository.tudelft.nl/islandora/object/uuid:f536b829-42ae-41d5-968d-13bbaa4ec736?collection=education)

* 论文阅读笔记：https://www.yuque.com/huangzhongqing/hre6tf/pcohs1
* 代码分析笔记：https://www.yuque.com/huangzhongqing/hre6tf/no0h80

### Setup
##### Frameworks and Packages
Make sure you have the following is installed:
 - [ROS Kinetic](http://wiki.ros.org/kinetic)
 - [PCL 1.7.2](http://pointclouds.org/downloads/)
 - [Open CV 3.2](https://opencv.org/)【PCL自带opencv，不用安装】

##### Dataset
* Download the [Kitti Raw data](http://www.cvlibs.net/datasets/kitti/raw_data.php).

```
// 地址已失效

wget http://kitti.is.tue.mpg.de/kitti/raw_data/2011_09_26_drive_0002/2011_09_26_drive_0005_sync.zip
wget http://kitti.is.tue.mpg.de/kitti/raw_data/2011_09_26_calib.zip

// 使用下面下载
https://s3.eu-central-1.amazonaws.com/avg-kitti/raw_data/2011_09_26_calib.zip
https://s3.eu-central-1.amazonaws.com/avg-kitti/raw_data/2011_09_26_drive_0005/2011_09_26_drive_0005_sync.zip
```


* Convert raw data to rosbag by using the tool made by tomas789. This is [his repository](https://github.com/tomas789/kitti2bag).


### Start

各模块代码路径：

* [src/groundremove](object_tracking/src/groundremove)
* [src/cluster](object_tracking/src/cluster)
* [tracking](object_tracking/tracking)

#### ~~PLEASE make sure you load the files, `src/ego_velo.txt` and `src/ego_yaw.txt` in `src/imm_ukf_jpda.cpp` l68, l69~~

##### Terminal 1
```
roscore
```

##### Terminal 2

`--loop`循环paly不推荐加，tracking和上一帧有关，误差越来越大

```
# kitti官方
rosbag play ~/data/KittiRawdata/2011_09_26_drive_0005_sync/kitti_2011_09_26_drive_0005_synced.bag --loop

# changshu bag
rosbag play  ~/data/changshu_bag/2018-06-04-16-46-11.bag --loop

```
##### Terminal 3
```
rviz
```
![arch](object_tracking/pic/setting.png)

##### Terminal 4
```

#  推荐运行launch
roslaunch  object_tracking test.launch
#  复杂
rosrun object_tracking ground
rosrun object_tracking cluster
rosrun object_tracking tracking

```

### Result


![arch](object_tracking//pic/result2.png)

######  Youtube [Clip](https://www.youtube.com/watch?v=zzFpTVk2Uj0)

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/zzFpTVk2Uj0/0.jpg)](https://www.youtube.com/watch?v=zzFpTVk2Uj0)



### License

Copyright (c) [双愚](https://github.com/HuangCongQing/3D-LIDAR-Multi-Object-Tracking). All rights reserved.

Licensed under the [MIT](./LICENSE) License.
