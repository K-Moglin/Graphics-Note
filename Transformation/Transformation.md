# Transformation（几何变换）

- **Scale（缩放）**
- **Reflection（对称）**
- **Shear（切变）**
- **Rotate（旋转）**
- **Translation（平移）**

---

## Homogeneous coordinates（齐次坐标）

### 核心概念

- **同一点的等价类：** $(x,y,w) \sim (\lambda x,\lambda y,\lambda w)$（$\lambda \neq 0$）。
- **2D 点 ↔ 齐次：** $(x,y) \mapsto (x,y,1)$；反变换：$(x,y,w)\mapsto\left(\dfrac{x}{w},\dfrac{y}{w}\right)$（$w\neq 0$）。
- **3D 点 ↔ 齐次：** $(x,y,z) \mapsto (x,y,z,1)$；反变换除以 $w$。
- **方向/无穷远点：** $w=0$ 表示方向（点在无穷远），常用来表示平行方向。

### 为什么用齐次坐标

- **把平移也纳入矩阵乘法：** 2D 用 $3\times 3$，3D 用 $4\times 4$，统一旋转/缩放/错切/平移/透视。
- **自然描述无穷远与透视：** 更便于图形学和射影几何中的判定与计算。

---

## 常见 2D 变换（列向量右乘）

**平移 $(t_x,t_y)$**

$$
\begin{bmatrix}
x'\\y'\\1
\end{bmatrix}
=
\begin{bmatrix}
1&0&t_x\\
0&1&t_y\\
0&0&1
\end{bmatrix}
\begin{bmatrix}
x\\y\\1
\end{bmatrix}
$$

**缩放 $(s_x,s_y)$**

$$
\begin{bmatrix}
x'\\y'\\1
\end{bmatrix}
=
\begin{bmatrix}
s_x&0&0\\
0&s_y&0\\
0&0&1
\end{bmatrix}
\begin{bmatrix}
x\\y\\1
\end{bmatrix}
$$

**绕原点旋转 $\theta$**

$$
\begin{bmatrix}
x'\\y'\\1
\end{bmatrix}
=
\begin{bmatrix}
\cos\theta&-\sin\theta&0\\
\sin\theta&\ \cos\theta&0\\
0&0&1
\end{bmatrix}
\begin{bmatrix}
x\\y\\1
\end{bmatrix}
$$

> 组合变换 = 矩阵相乘（右乘列向量时，应用顺序与矩阵从右到左一致）。

---

## 常见 3D 仿射骨架
（点：$(x,y,z,1)^\top$；向量/方向：$(v_x,v_y,v_z,0)^\top$）

$$
\begin{bmatrix}
x'\\y'\\z'\\1
\end{bmatrix}
=
\begin{bmatrix}
R_{3\times3} & \mathbf{t} \\
\mathbf{0}^{\top} & 1
\end{bmatrix}
\begin{bmatrix}
x\\y\\z\\1
\end{bmatrix}
$$

其中 $R_{3\times3}$ 可由旋转/缩放/错切合成，$\mathbf{t}=(t_x,t_y,t_z)^\top$ 为平移。

- **点（$w=1$）会受平移影响**；**方向（$w=0$）不受平移影响**。

---

## 透视投影（简化针孔模型示意）

设相机坐标为 $(x,y,z,1)^\top$，焦距 $f$，做透视除法得到 $w_c$ 后再除：

$$
\begin{bmatrix}
x_c\\y_c\\z_c\\w_c
\end{bmatrix}
=
\begin{bmatrix}
f&0&0&0\\
0&f&0&0\\
0&0&1&0\\
0&0&\dfrac{1}{d}&0
\end{bmatrix}
\begin{bmatrix}
x\\y\\z\\1
\end{bmatrix},
\qquad
(x',y')=\left(\dfrac{x_c}{w_c},\ \dfrac{y_c}{w_c}\right)
$$

> 实作里常见做法：先用 $4\times4$ 矩阵变换到裁剪空间（clip space），再做 **perspective divide**（除以 $w$）。

---

## 点线关系与相交（2D 射影）

- 直线 $ax+by+c=0$ 的齐次表示：$\ell=(a,b,c)^\top$。  
  点 $p=(x,y,1)^\top$ 在线上当且仅当 $\ell^\top p=0$。

- 两线 $\ell_1,\ell_2$ 的交点：
$$
p=\ell_1 \times \ell_2 \quad (\text{在 }\mathbb{R}^3\text{ 中做叉乘})
$$

- 两点 $p_1,p_2$ 的连线：
$$
\ell=p_1 \times p_2
$$

若交点 $p$ 的 $w=0$，说明交点在无穷远（两直线平行）。

---

## 实战提醒

- 需要欧氏坐标就**除以 $w$**；$(x,y,w)\sim(\lambda x,\lambda y,\lambda w)$ 可适当归一化。
- **点**用 $w=1$；**方向/法向量**用 $w=0$（不受平移影响）。
- 注意矩阵与向量的乘法约定（本笔记默认**列向量右乘**）。
- 在 GitHub 上，块公式 `$$...$$` **不要缩进**、上下各空一行，避免放在 HTML 容器里（如 `<details>`、`<table>`）。

---

## 参考链接

- [GAMES 101 Lecture 03（UCSB / Lingqi Yan）](https://sites.cs.ucsb.edu/~lingqi/teaching/resources/GAMES101_Lecture_03.pdf)
