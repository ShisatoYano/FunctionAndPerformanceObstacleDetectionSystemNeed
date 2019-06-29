## Table of content
<!-- TOC -->

- [Table of content](#table-of-content)
- [Introduction](#introduction)
- [Reference](#reference)
- [Finding boundary of obstacle](#finding-boundary-of-obstacle)
    - [Taking a detour](#taking-a-detour)
- [Detecting an obstacle in a short term](#detecting-an-obstacle-in-a-short-term)
    - [Case of running out into road](#case-of-running-out-into-road)
    - [How to calculate a braking distance](#how-to-calculate-a-braking-distance)

<!-- /TOC -->

## Introduction

Obstacle detection system needs multiple functions to detect an obstacle and escape a collision. When we develop the system, it is very important to decide that the system should have what kind of function and how performance the functions should satisfy.  
In this article, I'm introducing how to consider functions and performance the obstacle detection system should satisfy.  

## Reference

I read the following book as a reference. This book has good exlanations about techniques of perception with LiDAR, RADAR and Camera.  
[トランジスタ技術2019年3月号](https://www.amazon.co.jp/%E3%83%88%E3%83%A9%E3%83%B3%E3%82%B8%E3%82%B9%E3%82%BF%E6%8A%80%E8%A1%93-2019%E5%B9%B4-03%E6%9C%88%E5%8F%B7/dp/B07MFM728X/ref=sr_1_6?__mk_ja_JP=%E3%82%AB%E3%82%BF%E3%82%AB%E3%83%8A&crid=MPFWCSQ48JBI&keywords=%E3%83%88%E3%83%A9%E3%83%B3%E3%82%B8%E3%82%B9%E3%82%BF%E6%8A%80%E8%A1%93&qid=1561774997&s=gateway&sprefix=%E3%83%88%E3%83%A9%E3%83%B3%E3%82%B8%E3%82%B9%E3%82%BF%2Caps%2C1016&sr=8-6)  

## Finding boundary of obstacle

There are two ways of escaping a collision with an obstacle as follow.  

* Stopping by brake
* Taking a detour by handle

### Taking a detour

An important information when the car escape an obstacle by taking a detour is "How is a colliding object blocking a road?" Especially, It is important to recognize where a lateral boundary of the object is.  
The follwing figures are two patterns of escaping. On the left figure, an obstacle does not occupancy much on the road area, so the car can change the moving direction and escape the obstacle. On the other hand, the area where the obstacle occupancies is very large on the right figure. There is not enough to escape the obstacle, so the car should stop driving before colliding with the obstacle.  
![](2019-06-29-21-56-26.png)  

If the obstacle was sensed as an image data by a camera, the position of lateral boundary can be recognized easily like the following figure because the image data has a high resolution on the lateral direction.  
![](2019-06-29-22-10-37.png)  

On the other hand, if the obstacle was detected by a sensor which has a low lateral resolution like a LiDAR, the position of lateral boundary can not be recognized as follow.  
![](2019-06-29-22-13-11.png)  

## Detecting an obstacle in a short term

This system should not take a long time to detect an obstacle. Firstly, we need to decide a concrete valuable of time to detect the obstacle. The valueable is used for designing the system as a target valuable of processing speed.  

### Case of running out into road
We assumed that the car was driving at 36km/h(10m/s) and a pedestrian ran out into the road at 3.6km/h(1m/s). In this case, how far will the car move for until stopping by emergency brake?  
![](2019-06-29-22-41-35.png)  

### How to calculate a braking distance

* [ブレーキに関する常識を覆す 車両重量と制動距離の真の関係](https://macasakr.sakura.ne.jp/braking.html#7)  

* [交通事故における車速と停止距離を考える](http://www5d.biglobe.ne.jp/Jusl/Keisanki/JTSL/TeisiSyasoku.html)  