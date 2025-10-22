# Linear Algebra

## Vectors

向量的意义：Direction and Length

### Dot Product

$\vec a \cdot \vec b = \lVert \vec a \rVert \, \lVert \vec b \rVert \cos\theta$



点乘的结果是一个值

点乘在图形学中的意义：

* Find angle between two vectors(e.g. cosine of angle between light source and surface)
* Finding projection(投影) of one vector on another
* Measure how close two directions are
* Decompose a vector
* Determine forward /backward

### Cross Product

叉乘的结果是一个向量

Cross product is orthogonal to two initial vectors

Direction determined by **right-hand rule**

叉乘在图形学中的意义：

* Useful in constructing coordinate systems
* Determine left / right
* Determine inside / outside

## Matrices

什么是矩阵：Array of numbers (m × n = m rows, n columns)

### Matrix-Matrix Multiplication

(number of) columns in A must = # rows in B 即 (M x **N**) (**N** x P) = (M x P)

Element (i, j) in the product is the dot product of row i from A and column j from B

Properties：

- Non-commutative(AB and BA are different in general)
- Associative and distributive
- (AB)C=A(BC)
- A(B+C) = AB + AC
- (A+B)C = AC + BC

### Matrix-Vector Multiplication

Treat vector as a column matrix (m×1)

## 链接

[课件](https://sites.cs.ucsb.edu/~lingqi/teaching/resources/GAMES101_Lecture_02.pdf)
