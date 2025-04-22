Today I’d like to talk about **some key bottlenecks that are holding back the development of autonomous driving**. While the technology has come a long way, there are still major challenges we need to overcome—especially when it comes to perception and sensing.

今天我想和大家分享的是 **无人驾驶的瓶颈技术**。虽然技术已经取得了长足进展，但我们仍然面临着一些挑战，尤其是在感知和传感方面。

### 1. **Visual Perception Is Still the Biggest Challenge**

One of the toughest technical problems is improving how self-driving cars **see and understand the world**, just like humans do.

Right now, computer vision systems are still relatively limited. In unexpected situations—like when a pedestrian suddenly walks into the road—many systems, including lidar, **struggle to react in time**.

This limitation in vision directly affects both the safety and decision-making abilities of autonomous vehicles.

其中一个最具挑战性的技术问题是如何提升自动驾驶汽车的**视觉能力**，使其能够像人类一样**看懂世界**。

目前，计算机视觉系统仍然相对有限。在一些突发情况下——例如行人突然出现在路上——许多系统，包括激光雷达，**难以及时作出反应**。

这种视觉能力的局限直接影响到自动驾驶汽车的安全性和决策能力。


### 2. **Perceiving the Environment Is Extremely Complex**

Seeing clearly isn't enough. A self-driving car needs to:

*   **Understand what it sees**—like pedestrians, lanes, stop lines, traffic signs, and lights.
*   **Predict what might happen next**—for example, is the lane going to end? Is that car pulling over?

And things get even trickier in bad weather or poor lighting. In snow, fog, or when shadows cover the road, important lane markings might disappear, and the car can easily get confused or make the wrong decisions.

仅仅看清楚是不够的。自动驾驶汽车需要：

*   **理解它看到的**——如行人、车道、停止线、交通标志和信号灯等。
*   **预测接下来可能发生的事情**——例如，车道是否会结束？那辆车是否在停车？

在恶劣天气或光线不佳的情况下，情况会更加复杂。在雪天、雾霾或阴影遮挡下，重要的车道标记可能会消失，汽车很容易会感到困惑或做出错误的决策。

### 3. **Current Sensor Systems Have Limitations**
Let’s talk a bit about the sensors, which are basically the "eyes" of an autonomous vehicle. Each has its strengths and weaknesses:

1.  **Cameras**
    *   They're sensitive to lighting, angles, and even dirt on the lens;
    *   Images can be low-quality or blurry, which hurts detection accuracy;
    *   They often lack real-time responsiveness and struggle in tough environments.
  
2.  **Radar**
    *   Not very effective in bad weather like rain, snow, or fog;
    *   Has blind spots and can't give a complete picture of the surroundings.
3.  **Lidar**
    *   Offers high precision and fast response—currently one of the best sensors out there;
    *   But the cost is still extremely high, which makes it hard to use on a large scale.

现在我们来谈谈传感器，它们基本上是自动驾驶汽车的“眼睛”。每种传感器都有其优缺点：
1.  **相机**
    *   对光线、角度甚至镜头上的灰尘非常敏感；
    *   图像可能质量低或模糊，影响识别精度；
    *   实时响应能力差，且在复杂环境中表现不佳。
  
2.  **雷达**
    *   在恶劣天气（如雨雪或雾霾）下效果不佳；
    *   有盲区，不能提供完整的周围环境图像。
 
3.  **激光雷达**
    *   提供高精度和快速响应——目前是最先进的传感器之一；
    *   但其成本仍然非常高，这限制了它的大规模应用。
### 4. **Sensor Bottlenecks Affect the Entire System**
Since sensors are the core of perception, **any weaknesses here directly impact the whole autonomous system**.
For example, if a camera produces poor-quality images, the navigation and obstacle-avoidance systems can make wrong decisions. And in autonomous driving, **one bad decision can have serious consequences**.

由于传感器是感知系统的核心，**任何传感器的弱点都会直接影响整个自动驾驶系统**。
例如，如果相机拍摄的图像质量差，导航和避障系统可能会做出错误的决策。而在自动驾驶中，**一次错误的决策可能会带来严重后果**。
