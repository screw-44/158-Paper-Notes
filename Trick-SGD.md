# SGD是什么？
Stochastic Gradient Descent(SGD),计算梯度，方向传播。相对与批量梯度下降算法，随机梯度下降只是随机选择一个样本进行计算梯度来更新模型参数，提高了学习速度。下面介绍的是SGD的优化参数。
## Momentum 动量
在梯度下降的过程中，有小的局部最优结。显而易见，我们希望求到的是全局最优解。引入动量(Momentum)可以在到达局部最优结的时候，仍然继续优化，从而跳出局部最优解。
## Learning Rate 学习率
$x_{n+1} = x_n - lr * dx_n$ 从这个公式中显然可以知道学习率的作用了。  
在实际我们的算法过程中，算法一开始我们会使用较高的学习率来快速拟合，随着epoch的增加，我们会指数级别的减少学习率（通常是10倍去除）。在减少学习率的同时，error rate也会猛的下降，具体原因还不太清楚，但是在部分论文中观察到了这个现象。
## Weight Decay 权值衰减
Weight Decay的使用是为了防止过拟合。Weight Decay等价于L2正则化。有Drop out的效果。$x_{n+1}=x_n-lr*dx_n-lr*wd*x_n$
## 为什么现在还在用SGD，而不使用更先进的梯度下降算法
以Adam为代表，现在已经有了更好的，基本上不需要调参的优化器。但是在效果上，CV上往往不如传统的SGD，NLP中已经大量使用Adam去配合Transformer。