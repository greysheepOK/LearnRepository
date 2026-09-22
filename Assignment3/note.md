# 笔记

## 重心坐标

设三角形ABC中任意一点P，可以按照面积比值计算得重心坐标$(α，β，γ)$：

$$S=AB \times AC$$

$$\alpha=\frac{PB \times PC}{S} $$

$$\beta = \frac{PC \times PA}{S} $$

$$\gamma = \frac{PA \times PB}{S}$$

于是所有三角形内部属性可根据顶点属性线性插值得到，例如P的z坐标:

$$Z_P = \alpha Z_A + \beta Z_B + \gamma Z_C$$

但当我们经过透视投影后，由于三维上的三角形坐标要经过透视除法（$p = \frac{P}{Z_P}$），内部属性不可再由顶点插值得到。取而代之的是透视校正插值：

$$\frac{1}{Z_p} = \alpha \frac{1}{Z_a} + \beta \frac{1}{Z_b} + \gamma \frac{1}{Z_c}$$

推导如下：

设视图空间上三角形 $V_0V_1V_2$ 透视投影后成为三角形 $v_0v_1v_2$ ，原点$P$ 对应后者点 $p$ ，重心坐标分别为 $(A, B, C)$ 与 $(\alpha, \beta, \gamma)$，则在各自三角形上线性插值有： 

$$P = AV_0 + BV_1 + CV_2 \tag{1}$$

$$p = \alpha v_0 + \beta v_1 + \gamma v_2 \tag{2}$$

透视除法有：

$$v_0 = \frac{V_0}{Z_0}, \quad v_1 = \frac{V_1}{Z_1}, \quad v_2 = \frac{V_2}{Z_2}, \quad p = \frac{P}{Z_P}$$

代入$(2)$式：

$$ \frac {P}{Z_P} = \alpha \frac{V_0}{Z_0} + \beta \frac{V_1}{Z_1} + \gamma \frac{V_2}{Z_2} \tag{3}$$

比较$(1)(3)$式可得：
$$A = \alpha \frac{Z_P}{Z_0}, \quad B = \beta \frac{Z_P}{Z_1}, \quad C = \gamma \frac{Z_P}{Z_2}$$

又因为$A + B + C = 1$，因此：

$$\alpha \frac{Z_P}{Z_0} + \beta \frac{Z_P}{Z_1} + \gamma \frac{Z_P}{Z_2} = 1$$

整理得

$$\frac{1}{Z_P} = \alpha \frac{1}{Z_0} + \beta \frac{1}{Z_1} + \gamma \frac{1}{Z_2}$$

故 $1/Z_p$ 可由重心坐标线性插值，这也称为透视校正除法。

可以推广到任意三维属性 $I = A I_0 + B I_1 + C I_2$，由 $A = \alpha \frac{Z_P}{Z_0}, B = \beta \frac{Z_P}{Z_1}, C = \gamma \frac{Z_P}{Z_2}$ 可得：

$$I = \frac {\alpha Z_P}{Z_0} I_0 + \frac{\beta Z_P}{Z_1} I_1 + \frac{\gamma Z_P}{Z_2} I_2$$

两边除以$Z_P$得到：

$$\frac{I_P}{Z_P} = \alpha \frac{I_0}{Z_0} + \beta \frac{I_1}{Z_1} + \gamma \frac{I_2}{Z_2}$$

故对任何三维属性$I$，$\frac {I}{Z}$可由重心坐标线性插值。

## TBN矩阵

TBN矩阵是用于将法线贴图从纹理空间转换到世界空间的矩阵。它由三个正交向量组成：切线（Tangent）、副切线（Bitangent）和法线（Normal）。TBN矩阵组成可以表示为
$$TBN = (T, B, N)$$

其中

$$T = (T_x, T_y, T_z)，为切线方向的单位向量$$

$$B = (B_x, B_y, B_z)，为副切线方向的单位向量$$

$$N = (N_x, N_y, N_z)，为法线方向的单位向量$$

对纹理空间计算得到的法线，通过乘以TBN矩阵转化到实际世界空间对应的方向。