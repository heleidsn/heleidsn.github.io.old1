---
title: realsense_depth_image
date: 2020-11-16 23:24:00
tags: ROS
---
# Intel RealSense Depth Image

## RealSense相机深度图像获取

Realsense ros: https://github.com/IntelRealSense/realsense-ros

## Aligned Depth Frames

使用`roslaunch realsense2_camera rs_rgbd.launch`会自动开启深度图像对齐。

## 常规深度图像获取

Topic name: `/camera/aligned_depth_to_color/image_raw`

```python
depth_image_msg = msg

# transfer image from msg to cv2 image
try:
    cv_image = self.bridge.imgmsg_to_cv2(depth_image_msg, desired_encoding=depth_image_msg.encoding)
except CvBridgeError as e:
    print(e)
```

此时的`cv_image`是深度图像，以毫米为单位，应该是`16UC1`格式。

## 压缩后的深度图像恢复

Topic name: `/camera/aligned_depth_to_color/image_raw/compressedDepth`

在从rosbag中恢复深度图像的时候用到。

ref: https://answers.ros.org/question/249775/display-compresseddepth-image-python-cv2/

由于压缩后的depth image中包含了多余信息，因此需要先对msg进行一定的处理，得到`16UC1`格式的深度图像：

```python
# 'msg' as type CompressedImage
depth_fmt, compr_type = msg.format.split(';')
# remove white space
depth_fmt = depth_fmt.strip()
compr_type = compr_type.strip()
if compr_type != "compressedDepth":
    raise Exception("Compression type is not 'compressedDepth'."
                    "You probably subscribed to the wrong topic.")

# remove header from raw data
depth_header_size = 12
raw_data = msg.data[depth_header_size:]

depth_img_raw = cv2.imdecode(np.fromstring(raw_data, np.uint8), cv2.IMREAD_UNCHANGED)
```

此时的`depth_img_raw`就是恢复出来的包含深度信息的图像（以mm为单位）。
