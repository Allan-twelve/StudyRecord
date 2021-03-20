# 笔记

[toc]

## 公式

假设在m个训练集中，y一共有k类。

任意的一个x在k个类中的概率为：
$$
h_{\theta }(xi)=\frac{1}{\sum_{k}^{j=1}e^{\theta _{j}^{T}x_{i}}}\cdot \begin{bmatrix}
e^{\theta _{1}^{T}x_{i}}\\ 
e^{\theta _{2}^{T}x_{i}}\\ 
...\\ 
e^{\theta _{k}^{T}x_{i}}
\end{bmatrix}
$$
这里通过除它们的总和，使k个类的概率和为1

代价函数为：
$$
J(\theta )=-\frac{1}{m}[\sum_{i=1}^{m}\sum_{j=1}^{k}1\{y_{i}=j\}log\frac{e^{\theta _{j}^{T}x_{i}}}{\sum_{l=1}^{k}e^{\theta _{l=1}^{k}x_{i}}}]
$$

$$
这里1\{y_{i}=j\}为示性函数或者指示函数(随便叫啥都好了)，当y_{i}=j时返回1的值，否则返回0
$$

求导后为：（过程略）
$$
-\frac{1}{m}\sum_{i=1}^{m}[x_{i}(1\{y_{i}=j\}-\frac{e^{\theta _{j}^{T}x_{i}}}{\sum_{l=1}^{k}e^{\theta _{l=1}^{k}x_{i}}})]
$$
梯度公式：
$$
\theta_{j}=\theta_{j}+\alpha \frac{1}{m}\sum_{i=1}^{m}[x_{i}(1\{y_{i}=j\}-\frac{e^{\theta _{j}^{T}x_{i}}}{\sum_{l=1}^{k}e^{\theta _{l=1}^{k}x_{i}}})]
$$


## 代码说明

由于吴恩达教授讲softmax回归是用神经网络算法实现的，所以我用别的方法实现花了很长的时间，代码也写的很复杂，主要是y的0或1输出实现卡了很久，最后代码写好以后总感觉哪里有点问题，但是它既然能运行，成功地估测概率，效果还不错，那应该就是没问题了，我也不想再检查了，由于matplotlib绘图能力有限，所以有些图我画不出来，就只能根据数据来判断了。之所以没有把它正则化，是因为代码写的我自己都看不懂了，精力有限，尽力了。:broken_heart:

logistics的one vs all和softmax进行对比，softmax在有重复性或者说多个类别的归类中，效果会更好。
