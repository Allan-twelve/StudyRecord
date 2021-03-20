# 笔记

[toc]

## 公式推导

### 梯度下降的公式推导

线性方程中，预测函数为：（n为x变量的总数，如一元线性n=1）
$$
h_{\theta }(x)=\theta ^{T}x=\theta _{0}x_{0}+\theta _{1}x_{1}+\theta _{2}x_{2}+...+\theta _{n}x_{n}
$$
代价函数：(其中m为样本总数)
$$
J(\theta )=\frac{1}{2m} \sum_{i=1}^{m}\left ( h_{\theta }(x_{i})-y_{i} \right )^{2}
$$
梯度下降的一般更新公式为：
$$
\theta _{j}=\theta _{j}-\alpha \frac{\partial }{\partial \theta _{j}}J (\theta )
$$
对代价函数求偏导数：
$$
\frac{\partial J (\theta )}{\partial \theta _{j}}=\frac{\partial J (\theta )}{\partial h_{\theta }(x)}\cdot \frac{\partial h_{\theta }(x)}{\partial \theta _{j}}
$$

$$
\frac{\partial J (\theta )}{\partial h_{\theta }(x)}=\frac{1}{m}\sum_{i=1}^{m}(h_{\theta }(x_{i})-y_{i})
$$

$$
\frac{\partial h_{\theta }(x)}{\partial \theta _{j}}=x_{j}
$$

$$
\frac{\partial J (\theta )}{\partial \theta _{j}}=\frac{1}{m}\sum_{i=1}^{m}(h_{\theta }(x_{i})-y_{i})x_{ij}
$$

所以梯度更新公式为：
$$
\theta _{j}=\theta _{j}-\alpha \frac{1}{m}\sum_{i=1}^{m}(h_{\theta }(x_{i})-y_{i})x_{ij}
$$
推导完毕

### 最小二乘法推导

目的：使平方和最小------求J函数最小值
$$
J(\theta _{0},\theta _{1})=\sum_{i=1}^{m}(y_{i}-(\theta _{0}+\theta _{1}x_{i}))^{2}
$$
求偏导数，并令它们等于0：
$$
\frac{\partial }{\partial \theta _{0}}J(\theta _{0},\theta _{1})=2\sum_{i=1}^{m}(y_{i}-(\theta _{0}+\theta _{1}x_{i}))=0
$$

$$
\frac{\partial }{\partial \theta _{1}}J(\theta _{0},\theta _{1})=2\sum_{i=1}^{m}(y_{i}-(\theta _{0}+\theta _{1}x_{i}))x_{i}=0
$$

$$
先是\theta_{0}
$$


$$
\sum_{i=1}^{m}(y_{i}-(\theta _{0}+\theta _{1}x_{i}))=0
$$

$$
\sum_{i=1}^{m}y_{i}-\theta _{0}m-\theta _{1}\sum_{i=1}^{m}x_{i}=0
$$

$$
\frac{\sum_{i=1}^{m}y_{i}-\theta _{1}\sum_{i=1}^{m}x_{i}}{m}=\theta _{0}----公式1
$$

$$
\theta_{0}=\overline{y}-\theta _{1}\overline{x}
$$

$$
然后\theta_{1}
$$

$$
\sum_{i=1}^{m}(y_{i}-(\theta _{0}+\theta _{1}x_{i}))x_{i}=0
$$

$$
\sum_{i=1}^{m}x_{i}y_{i}-\theta _{0}\sum_{i=1}^{m}x_{i}-\theta _{1}\sum_{i=1}^{m}x_{i}^{2}=0
$$

调用公式1
$$
\sum_{i=1}^{m}x_{i}y_{i}-\frac{\sum_{i=1}^{m}x_{i}\sum_{i=1}^{m}y_{i}-\theta_{1}(\sum_{i=1}^{m}x_{i})^{2}}{m}-\theta _{1}\sum_{i=1}^{m}x_{i}^{2}=0
$$

$$
\theta_{1}(\sum_{i=1}^{m}x_{i}^{2}-\frac{(\sum_{i=1}^{m}x_{i}) ^{2}}{m})=\sum_{i=1}^{m}x_{i}y_{i}-\frac{\sum_{i=1}^{m}x_{i}\sum_{i=1}^{m}y_{i}}{m}
$$

$$
\theta_{1}(\sum_{i=1}^{m}x_{i}^{2}-m\overline{x}^{2})=\sum_{i=1}^{m}x_{i}y_{i}-mx_{i}y_{i}
$$

$$
\theta_{1}=\frac{\sum_{i=1}^{m}x_{i}y_{i}-mx_{i}y_{i}}{\sum_{i=1}^{m}x_{i}^{2}-m\overline{x}^{2}}
$$

推导完毕

### 矩阵公式法推导

代价函数：
$$
X,Y,\Theta都是矩阵或向量
$$

$$
J(\theta )=(Y-X\Theta )^{2}
$$

$$
=(Y-X\Theta)^{T}\cdot (Y-X\Theta )
$$

$$
=(Y^{T}-\Theta ^{T}X^{T})\cdot (Y-X\Theta )
$$

$$
=Y^{T}Y-\Theta ^{T}X^{T}Y-Y^{T}X\Theta +\Theta ^{T}X^{T}X\Theta
$$

对J函数求偏导数：
$$
\frac{\partial }{\partial \theta }J(\theta )=-X^{T}Y-X^{T}Y +2X^{T}X\Theta
$$
令J函数为0：
$$
X^{T}Y=X^{T}X\Theta
$$

$$
\Theta=(X^{T}X)^{-1}X^{T}Y
$$

推导完毕

## 代码说明

线性回归是花了最长时间学习和实现的

一开始先用高中学过的公式也就是最小二乘法化简后的公式实现了简单线性回归，后来听了吴恩达的机器学习课后尝试了梯度下降法解决，也实现了。

随着学习深入开始尝试用矩阵相乘代替逐个计算求和，从而进行简化代码，以及之后的从一元到多元，后来学习了正则化后，在原有的代码上进行修改，速度便快了很多。

由于课上并没有讲岭回归，后来查阅资料后发现其实已经实现了，

就是：
$$
\Theta=(X^{T}X)^{-1}X^{T}Y
$$
这个方法加上正则化，从而也避免了逆矩阵不存在的情况(虽然求伪逆也不影响结果)
