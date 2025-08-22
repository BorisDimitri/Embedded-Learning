# FOC

FOC本质上是一个电机旋转运动的数学模型

电机控制：改变电机定子线圈的电流交变频率和波形，在定子周围形成磁场，驱动转子永磁体转动

六个MOS管控制，电机控制限制的本质是mos管开关的速率



![image-20250822152556579](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250822152556579.png)

## 克拉克变换

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250822193453193.png" alt="image-20250822193453193" style="zoom:25%;" />

交替开关的MOS是以极快的速度交替运行的

三个相的曲线存在120度的相位差

相与相之间相互耦合，MOS管一旦打开就一定会打开至少两个相

**克拉克变换**：三相相位差120的电机波形**降解**为二维矢量

​	电流**曲线的纵坐标**变化为**矢量长度**

​	将三相120的波形抽象为120度的矢量，再通过克拉克变换把三相投影在正交的两个轴上

​	这样可以省去一路电流传感器

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250822194540204.png" alt="image-20250822194540204" style="zoom:25%;" />

> $I_\alpha = I_{a} - (I_{b} + I_{c})\cos{30}$
> $I_{\beta} = I_{b} - I_{c}$

基尔霍夫电流定律：在任何时刻，流入电流节点的电流之和等于流出节点的电流之和

>  $I_{a} + I _{b} + I_{c} $

**等幅值变换系数**：为了使得a相输入为1A时，反应在Alpha轴上的**电流的幅值**也是1A没有被改变，我们就得**乘上系数**$\frac{2}{3}$ (简化输入环境 )

> 原式为：$I_\alpha = I_{a} - (I_{b} + I_{c})\cos{30}$
> 					$I_{\beta} = I_{b} - I_{c}$
>
> 如果**输入$I_a = 1$** ，则在原本克拉克变换算出的 $I_{\alpha},I_{\beta}$ 的基础上算出**新的$I_{\alpha},I_{\beta}$** 
>
> $I_{\alpha} = I_{a}	$
>
> 根据基尔霍夫电流定律：$I_{\beta} = \frac{1}{\sqrt{3}} \times (2i_b + i_a)$
>
> 移项可得克拉克变换的逆变换 

## 帕克变换

 研究能使得电机旋转的 $I_{\alpha},I_{\beta} $ 的变化规律

定义了一个新的坐标系Q-D坐标系，随转子旋转而旋转

只要知道D轴和$\alpha$轴的角度，就可以把Q-D坐标系投影到 $\alpha, \beta$ 轴上

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250822233820698.png" alt="image-20250822233820698" style="zoom:25%;" />

 

电角度$\theta$是由编码器实时测出的值

$I_q,I_d$ 为建系时指定的，可以视为定值

通过$I_q,I_d,\theta$ 可以计算出 $I_{\alpha},I_{\beta}$,进而通过克拉克逆变换转为为波形$I_{a} , I _{b} , I_{c} $

