# 笔记

## 重心坐标

设三角形ABC中任意一点P，可以按照面积比值计算得重心坐标 $(\alpha, \beta, \gamma)$ ：

$$S=AB \times AC$$

$$\alpha=\frac{PB \times PC}{S} $$

$$\beta = \frac{PC \times PA}{S} $$

$$\gamma = \frac{PA \times PB}{S}$$

于是所有三角形内部属性可根据顶点属性线性插值得到，例如P的z坐标:

$$Z_P = \alpha Z_{A} + \beta Z_{B} + \gamma Z_{C}$$

但当我们经过透视投影后，由于三维上的三角形坐标要经过透视除法（ $p = \frac{P}{Z_{P}}$ ），内部属性不可再由顶点插值得到。取而代之的是透视校正插值：

$$\frac{1}{Z_p} = \alpha \frac{1}{Z_{a}} + \beta \frac{1}{Z_{b}} + \gamma \frac{1}{Z_{c}}$$

推导如下：

设视图空间上三角形 $V_0V_1V_2$ 透视投影后成为三角形 $v_{0}v_{1}v_{2}$ ，原点$P$ 对应后者点 $p$ ，重心坐标分别为 $(A, B, C)$ 与 $(\alpha, \beta, \gamma)$，则在各自三角形上线性插值有： 

$$
P = AV_0 + BV_1 + CV_2 \quad (1)
$$

$$
p = \alpha v_{0} + \beta v_{1} + \gamma v_{2} \quad (2)
$$

透视除法有：

$$v_{0} = \frac{V_{0}}{Z_{0}}, \quad v_{1} = \frac{V_{1}}{Z_{1}}, \quad v_{2} = \frac{V_{2}}{Z_{2}}, \quad p = \frac{P}{Z_{P}}$$

代入 $(2)$ 式：

$$
 \frac {P}{Z_{P}} = \alpha \frac{V_{0}}{Z_{0}} + \beta \frac{V_{1}}{Z_{1}} + \gamma \frac{V_{2}}{Z_{2}} \quad (3)
$$

比较 $(1)(3)$ 式可得：
$$A = \alpha \frac{Z_{P}}{Z_{0}}, \quad B = \beta \frac{Z_{P}}{Z_{1}}, \quad C = \gamma \frac{Z_{P}}{Z_{2}}$$

又因为 $A + B + C = 1$ ，因此：

$$\alpha \frac{Z_{P}}{Z_{0}} + \beta \frac{Z_{P}}{Z_{1}} + \gamma \frac{Z_{P}}{Z_{2}} = 1$$

整理得

$$\frac{1}{Z_{P}} = \alpha \frac{1}{Z_{0}} + \beta \frac{1}{Z_{1}} + \gamma \frac{1}{Z_{2}}$$

故 $1/Z_{P}$ 可由重心坐标线性插值，这也称为透视校正除法。

可以推广到任意三维属性 $I = A I_0 + B I_1 + C I_2$，由 $A = \alpha \frac{Z_{P}}{Z_{0}}, B = \beta \frac{Z_{P}}{Z_{1}}, C = \gamma \frac{Z_{P}}{Z_{2}}$ 可得：

$$I = \frac {\alpha Z_{P}}{Z_{0}} I_0 + \frac{\beta Z_{P}}{Z_{1}} I_1 + \frac{\gamma Z_{P}}{Z_{2}} I_2$$

两边除以 $Z_{P}$ 得到：

$$\frac{I_{P}}{Z_{P}} = \alpha \frac{I_{0}}{Z_{0}} + \beta \frac{I_{1}}{Z_{1}} + \gamma \frac{I_{2}}{Z_{2}}$$

故对任何三维属性 $I$ ， $\frac {I}{Z}$ 可由重心坐标线性插值。

## TBN矩阵

TBN矩阵是用于将法线贴图从纹理空间转换到世界空间的矩阵。它由三个正交向量组成：切线（Tangent）、副切线（Bitangent）和法线（Normal）。TBN矩阵组成可以表示为
$$TBN = (T, B, N)$$

其中

$$T = (T_{x}, T_{y}, T_{z})，为切线方向的单位向量$$

$$B = (B_{x}, B_{y}, B_{z})，为副切线方向的单位向量$$

$$N = (N_{x}, N_{y}, N_{z})，为法线方向的单位向量$$

对纹理空间计算得到的法线，通过乘以TBN矩阵转化到实际世界空间对应的方向。