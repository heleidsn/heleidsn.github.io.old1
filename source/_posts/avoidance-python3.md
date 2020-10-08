---
layout: '[post]'
title: 解决px4 avoidance和python3环境同时存在的问题
date: 2020-09-01 23:20:50
tags: ROS
---

今天用了很长时间来解决px4 avoidance和python3共处的问题。试过很多办法，发现avoidance只能使用python2进行编译，用python3编译之后还是会遇到`tf`的问题。

最终解决办法：

先加载avoidance环境，然后运行avoidance之后加载python3环境。

`source ~/catkin_avoidance/devel/setup.bash`

然后

`roslaunch local_planner local_planner_depth.launch`

等`avoidance`运行起来之后加载python3环境并运行代码

`source ～/catkin_python3/devel/setup.bash`

