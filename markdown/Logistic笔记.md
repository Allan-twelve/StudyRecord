# 笔记

[toc]

## 公式推导

### logistics回归推导

假设函数为：
$$
h_{\theta }(x)=\frac{1}{1+e^{-Z_{\theta }(x)}}
$$

$$
Z_{\theta }(x)=\theta ^{T}x=\theta _{0}x_{0}+\theta _{1}x_{1}+\theta _{2}x_{2}+...+\theta _{n}x_{n}
$$

代价函数为：
$$
J(\theta)=-\frac{1}{m}\sum_{i=1}^{m}(y_{i}logh_{\theta }(x)+(1-y_{i})log(1-h_{\theta }(x)))
$$
梯度一般更新公式为：
$$
\theta _{j}=\theta _{j}-\alpha \frac{\partial }{\partial \theta _{j}}J (\theta )
$$
求代价函数的偏导数：
$$
\frac{\partial }{\partial \theta _{j}}J (\theta )=\frac{\partial J(\theta)}{\partial h_{\theta}(x)}\cdot \frac{\partial h_{\theta}(x)}{\partial Z_{\theta}(x)}\cdot \frac{\partial Z_{\theta}(x)}{\partial \theta_j}
$$

$$
\frac{\partial J(\theta)}{\partial h_{\theta}(x)}=-\frac{1}{m}\sum_{i=1}^{m}(\frac{y_{i}}{h_{\theta}(x)}-\frac{1-y_{i}}{1-h_{\theta}(x)})----1
$$

$$
\frac{\partial h_{\theta}(x)}{\partial Z_{\theta}(x)}=\frac{e^{-Z_{\theta}(x)}}{(1+e^{-Z_{\theta}(x)})^{2}}----2
$$

$$
=\frac{1}{1+e^{-Z_{\theta}(x)}}\cdot \frac{e^{-Z_{\theta}(x)}}{1+e^{-Z_{\theta}(x)}}
$$

$$
=\frac{1}{1+e^{-Z_{\theta}(x)}}\cdot (1-\frac{1}{1+e^{-Z_{\theta}(x)}})
$$

$$
=h_{\theta}(x)\cdot (1-h_{\theta}(x))
$$

$$
\frac{\partial Z_{\theta}(x)}{\partial \theta_{j}}=x_{j}----3
$$

1，2，3式相乘：
$$
\frac{\partial }{\partial \theta _{j}}J (\theta )=-\frac{1}{m}\sum_{i=1}^{m}(y_{i}(1-h_{\theta}(x))-(1-y_{i})h_{\theta}(x))x_{i}
$$

$$
=\frac{1}{m}\sum_{i=1}^{m}(h_{\theta}(x)-y_{i})x_{i}
$$

很神奇，和线性回归如此相似，所以梯度公式为：
$$
\theta _{j}=\theta _{j}-\alpha \frac{1}{m}\sum_{i=1}^{m}(h_{\theta}(x)-y_{i})x_{i}
$$


## 代码说明

由于梯度下降的更新公式和线性回归的基本一致，所以我基本上改了个假设函数就能直接搬来用，因此代码完成的很快。

而多分类问题我只实现了one vs all(one vs rest)，通过使y的各种值在一定情况下只分为0或1，就可以回到二分类的问题上，从而解决。one vs one也是一样，由于时间关系就没有完成代码。
