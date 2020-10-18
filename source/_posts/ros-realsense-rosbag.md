---
title: 使用rosbag录制intelrealsense相机的数据
date: 2020-10-18 16:07:02
tags: ros, realsense
---

最近需要对px4 avoidance进行一些测试，由于wifi连接感觉不是很靠谱，因此需要在无人机上的jetson nano进行实时录制。

## rosbag

ref：http://wiki.ros.org/rosbag

rosbag可以很好的对ros中的所有信息进行录制，常用命令有：
`rosbag record -a`录制所有topics

然而对于realsense相机来说，其正常运行状态下以30fps的速度发布多个图像，如果对所有topic进行记录，10秒钟就可以得到1G的rosbag，要录制长时间的图像信息完全不可能，因此需要录制压缩后的图像topic。

## compressed_image_transport

ref: http://wiki.ros.org/compressed_image_transport

Compressed_image_transport provides a plugin to image_transport for transparently sending images encoded as JPEG or PNG.

我们直接记录压缩后的图像将大大降低rosbag的大小。

要得到压缩后的图像需要先安装`compressed_image_transport`包，然后使用`rosbag record /camera/color/image_raw/compressed`即可。

此外还可以使用`rqt_reconfigure`对压缩率进行控制。

## 压缩前后对比

`roslaunch realsense2_camera rs_rgbd.launch`

### 压缩前

```
path:        2020-10-18-16-24-04.bag
version:     2.0
duration:    12.2s
start:       Oct 18 2020 16:24:05.02 (1603034645.02)
end:         Oct 18 2020 16:24:17.23 (1603034657.23)
size:        322.7 MB
messages:    367
compression: none [367/367 chunks]
types:       sensor_msgs/Image [060021388200f6f0f447d0fcd9c64743]
topics:      /camera/color/image_raw   367 msgs    : sensor_msgs/Image
```

### 压缩后

```
path:        2020-10-18-16-23-44.bag
version:     2.0
duration:    10.9s
start:       Oct 18 2020 16:23:44.68 (1603034624.68)
end:         Oct 18 2020 16:23:55.59 (1603034635.59)
size:        15.9 MB
messages:    328
compression: none [21/21 chunks]
types:       sensor_msgs/CompressedImage [8f7a12909da2c9d3332d540a0977563f]
topics:      /camera/color/image_raw/compressed   328 msgs    : sensor_msgs/CompressedImage
```

## 深度图像压缩后无法显示问题

rgb图像压缩后可以直接显示，但是深度图像压缩后无法显示。

**compressed_depth_image_transport**

Compressed_depth_image_transport provides a plugin to image_transport for transparently sending depth images (raw, floating-point) using PNG compression.

安装上述插件之后发现相机发布的消息多了一个
```
<base_topic>/compressedDepth (sensor_msgs/CompressedImage)
```

只需要将这个消息进行记录即可记录压缩后的深度信息。

## 记录点云

对`/camera/depth_registered/points`消息进行记录，发现大的惊人，想办法压缩之。

对点云问题的讨论： https://discourse.ros.org/t/compressed-pointcloud2/10616/4

```
path:        points_2020-10-18-17-02-23.bag
version:     2.0
duration:    14.2s
start:       Oct 18 2020 17:02:23.88 (1603036943.88)
end:         Oct 18 2020 17:02:38.11 (1603036958.11)
size:        3.9 GB
messages:    428
compression: none [428/428 chunks]
types:       sensor_msgs/PointCloud2 [1158d486dd51d683ce2f1be655c3c181]
topics:      /camera/depth_registered/points   428 msgs    : sensor_msgs/PointCloud2
```

## ref

https://github.com/IntelRealSense/realsense-ros/issues/1076