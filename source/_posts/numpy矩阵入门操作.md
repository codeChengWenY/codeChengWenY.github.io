## numpy矩阵

矩阵是numpy.matrix类型的对象，该类继承自numpy.ndarray，任何针对多维数组的操作，对矩阵同样有效，但是作为子类矩阵又结合其自身的特点，做了必要的扩充，比如：乘法计算、求逆等。

### 1. 矩阵对象的创建

1. 通过ndarray创建matrix对象

```python
numpy.matrix(
    ary,		# 任何可被解释为矩阵的二维容器
  	copy=True	# 是否复制数据(缺省值为True，即复制数据)
)
```

2. `numpy.mat()`
```python
# 等价于：numpy.matrix(..., copy=False)
# 由该函数创建的矩阵对象与参数中的源容器一定共享数据，无法拥有独立的数据拷贝
numpy.mat(任何可被解释为矩阵的二维容器)

# 该函数可以接受字符串形式的矩阵描述：
# 数据项通过空格分隔，数据行通过分号分隔。例如：'1 2 3; 4 5 6'
numpy.mat(拼块规则)
```

**示例**

```python
# 创建matrix操作
import numpy as np

arr = np.arange(1, 10).reshape(3, 3)
print(arr)

# 第一种方式
m = np.matrix(arr, copy=True)
print(m, m.shape, type(m))

# 第二种方式:共享方式
m2 = np.mat(arr)

# 第三种方式
m3 = np.mat("1 2 3;4 5 6.0")
```

### 2. 矩阵的乘法运算

```python
# 矩阵乘法
import numpy as np

arr = np.array([[1, 1, 1],
                [2, 2, 2],
                [3, 3, 3]])
# 数组相乘, 各对应位置元素相乘
print(arr * arr)

# 矩阵相乘，第n行乘m列之和，作为结果的n,m个元素
# 矩阵相乘，第一个矩阵行数必须等于第二个矩阵列数
m = np.mat(arr)
print(m * m)
```

### 3. 矩阵的逆矩阵

若两个矩阵A、B满足：AB = E （E为单位矩阵），则称B为A的逆矩阵。

**单位矩阵**

- 在矩阵的乘法中，有一种矩阵起着特殊的作用，如同数的乘法中的1，这种矩阵被称为单位矩阵。
- 它是个方阵，从左上角到右下角的对角线（称为主对角线）上的元素均为1，除此以外全都为0，记为$I_n$或$E_n$ ，通常用I或E来表示。
- 根据单位矩阵的特点，任何矩阵与单位矩阵相乘都等于本身，而且单位矩阵因此独特性有广泛用途。
$$
E_3 =
\left[ \begin{array}{ccc}
1 & 0 & 0\\
0 & 1 & 0\\
0 & 0 & 1\\
\end{array} 
\right ]
$$

<!--more-->

**逆矩阵示例：**

```python
e = np.mat("1 2 6; 3 5 7; 4 8 9")
print(e.I)
print(e * e.I)

# 非方阵的逆（称为广义逆矩阵）
e = np.mat("1 2 6; 3 5 7")
print(e.I)
print(e * e.I)
```

注意：在计算过程中，可能出现`numpy.linalg.LinAlgError: Singular matrix`错误，说明该矩阵不可逆。

### 4. ndarray提供的矩阵API

ndarray提供了方法让多维数组替代矩阵的运算： 

```python
a = np.array([
    [1, 2, 6],
    [3, 5, 7],
    [4, 8, 9]])
# 点乘法求ndarray的点乘结果，与矩阵的乘法运算结果相同
k = a.dot(a)
print(k)
# linalg模块中的inv方法可以求取a的逆矩阵
l = np.linalg.inv(a)
print(l)
```

**执行结果：**

```python
[[ 31  60  74]
 [ 46  87 116]
 [ 64 120 161]]
[[-0.73333333  2.         -1.06666667]
 [ 0.06666667 -1.          0.73333333]
 [ 0.26666667  0.         -0.06666667]]
```

### 5. 矩阵应用

**案例：解线性方程组**

假设一帮孩子和家长出去旅游，去程坐的是bus，小孩票价为3元，家长票价为3.2元，共花了118.4；回程坐的是Train，小孩票价为3.5元，家长票价为3.6元，共花了135.2。分别求小孩和家长的人数。使用矩阵求解。表达成方程为：
$$
3x + 3.2y = 118.4\\
3.5x + 3.6y = 135.2
$$
表示成矩阵相乘：
$$
\left[ \begin{array}{ccc}
	3 & 3.2 \\
	3.5 & 3.6 \\
\end{array} \right]
\times
\left[ \begin{array}{ccc}
	x \\
    y \\
\end{array} \right]
=
\left[ \begin{array}{ccc}
	118.4 \\
	135.2 \\
\end{array} \right]
$$

```python
import numpy as np

# 解方程
prices = np.mat('3 3.2; 3.5 3.6')
totals = np.mat('118.4; 135.2')

x = np.linalg.lstsq(prices, totals)[0]  # 求最小二乘解
print(x)

x = np.linalg.solve(prices, totals)  # 求解线性方程的解
print(x)

x = prices.I * totals  # 利用矩阵的逆进行求解
print(x)
```

**案例：斐波那契数列**

1	1	 2	 3	5	8	13	21	34 ...

```python
X    |  1   1  |  1   1  |  1   1
     |  1   0  |  1   0  |  1   0
    --------------------------------
1  1 |  2   1  |  3   2  |  5   3
1  0 |  1   1  |  2   1  |  3   2
 F^1     F^2       F^3 	     F^4  ...  f^n
```

```python
import numpy as np
n = 35
# 使用递归实现斐波那契数列
def fibo(n):
    return 1 if n < 3 else fibo(n - 1) + fibo(n - 2)
print(fibo(n))

# 使用矩阵实现斐波那契数列
print(int((np.mat('1. 1.; 1. 0.') ** (n - 1))[0, 0]))
```

