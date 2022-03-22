# Designing Network Design Space
定义： Design Space 含有 network populations的space。  
使用semi-automated procedure 去帮助我们设计网络。

## 创新的实验方法
首先设定一些可以变化的变量和他们可以变化的区间，比如说b, w, g.再去使用数学方法随机采样，生成500个模型，每个模型迭代10个epoch。画图，图中y轴是error，最后选取error最小的那个。分别比较对比研究，从而得出结论。  
以AnyNet为例:  
To obtain valid models, we perform log-uniform sampling of $d_i \leq 16$, $w_i \leq 1024$ and divisible by 8, $b_i \in \{1, 2, 4\}$, and $g_i \in \{1, 2, ..., 32\}$. We repeat the sampling until we obtain n=500 models in our target complexity regime(360MF to 400MF), and train each model fro 10 epochs(for getting robust *population* statistics).

## AnyNet 和其变种
### AnyNet
AnyNet由stem+body+head组成
* stem由stride-2,3x3conv,输出32channels组成。  
* body由4stage组成。
* stage中含有不等数量的block。
* block中为一个resnet block。参数有width, bottleneck ratio, stride。
### AnyNet变种
* AnyNetXA = AnyNet
* AnyNetXB = AnyNetXA + $b_i=b$. 所有的block的bottlenet ratio为同一个。
* AnyNetXC = AnyNetXB + $g_i=g$. A shared group width. 这里认为是block内块conv块的宽度/channel数量。
* AnyNetXD = AnyNetXC + increasing widths.
* AnyNetXE = AnyNetXD + increasing depths.

## RegNet 使用一个线性方程来约束，量化 Stage widths and depths。  
方程：
1. $u_j = w_0 + w_a \cdot j\,$ for $\,0 \leq j < d$   
2. $u_j = w_0 \cdot w_m^{s_j}$ 求出$s_j$
3. $w_j = w_0 \cdot w_m^{|s_j|}$  
### 如何搜索最好的网络
In paticular, given a model, we compute the fit by setting $d$ to the network depth and performing a grid search over $w_0$, $w_a$, $w_m$ to minimize the mean log-ratio(denoted by $e_fit$)of predicted to obsevered per-block widths. 
### 结论 
$w_m = 2$和$u_j = w_a /cdot (j+1)$能稍微改善效果  
经过操作后，RegNet 的 Network Space小了很多，同时也比AnyNet效果要好（10个epoch后）。