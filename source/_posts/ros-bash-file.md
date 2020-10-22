---
title: Difference between execute a bash file vs source it 
date: 2020-10-22 10:22:05
tags: ros
---

最近在使用bash file创建新的环境变量的时候，发现直接执行该bash file并不能改变环境变量，于是搜索了一下，发现source和直接执行bash file还是有区别的。

Ref：
https://superuser.com/questions/176783/what-is-the-difference-between-executing-a-bash-script-vs-sourcing-it

原回答：

> `Sourcing` a script will run the commands in the current shell process.
> `Executing` a script will run the commands in a new shell process.
> Use source if you want the script to change the environment in your currently running shell. use execute otherwise.

总结：

直接执行bash file的话会在一个新的shell process中进行，而source的话会在当前shell process中进行。