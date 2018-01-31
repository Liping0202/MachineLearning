机器学习
=======

****
### Author:Song
### E-mail:Z.S.Chang@qq.com
****
参考自李航《统计学习方法》,使用Google Chrome与GitHub with MathJax插件组合浏览效果最佳！！！
## 目录
* [感知机学习算法](#感知机学习算法)
* [k近邻法](#k近邻法)
* [朴素贝叶斯](#朴素贝叶斯)
* [决策树](#决策树)
***
---
___
* ### 感知机学习算法
    * #### **原始形式**  
    
    |**输入**| 训练数据集$T={(x_1,y_1),(x_2,y_2),...,(x_N,y_N)}$ ，其中$x_i$∈$R^n$,$y_i$∈{$\{+1,-1\}$}，学习率$η(0<η≤1)$  |
    |:---------:|:-------------|
    |**输出**| w，b，感知机模型$f(x)=sign(w·x+b)$ |  
    |**步骤**  |（1）选取初始值w0，b0；<br>（2）在训练集中选取数据$(x_i,y_i)$；<br>（3）如果存在误分类点，即$y_{i}(w·x+b)≤0$，则<br>　　　　　　　　　$w=w+ηy_ix_i$<br>　　　　　　　　　$b=b+ηy_i$  <br>（4）转（2），直至训练集中没有误分类点。   |
    |**解释**  | （1）目标是求参数w，b，使得损失函数：$min_{w,b}$ $L(w,b)=- \sum_{x_{i}∈M} y_{i}(w·x_i+b)$极小化。其中M为误分类点的集合。<br>（2）采用随机梯度下降法（SGD）求解，即极小化过程中不是一次使M中所有误分类点的梯度下降，而是一次随机选取一个误分类点使其梯度下降。随机梯度下降的效率要高于批量梯度下降（batch gradient descent）<br>（3）当一个实例点被误分类，即位于分离超平面的错误一侧时，则调整w，b的值，使分离超平面向该误分类点的一侧移动，以减少该误分类点与超平面简的距离，直至超平面越过该误分类点使其被正确分类。|
    |**优缺点**|（1）在感知机模型中，只要给出的数据是线性可分的，那么我们就能证明在有限次迭代过程中，能够收敛；<br>（2）算法着重考虑是否将所有训练数据分类正确，而不考虑分的有多好，即存在无穷多个解，其解由于初值或不同的迭代顺序而可能有所不同；<br>（3）感知机主要的本质缺陷是它不能处理线性不可分问题；<br>（4）感知机因为是线性模型，所以不能表示复杂的函数，如异或，即感知机是无法处理异或问题，因为训练集线性不可分。|
    
    `为什么叫“感知机”：`感知机是生物神经细胞的简单抽象。神经细胞结构大致可分为：树突、突触、细胞体及轴突。单个神经细胞可被视为一种只有两种状态的机器——激动时为‘是’，而未激动时为‘否’。神经细胞的状态取决于从其它的神经细胞收到的输入信号量，及突触的强度（抑制或加强）。当信号量总和超过了某个阈值时，细胞体就会激动，产生电脉冲。电脉冲沿着轴突并通过突触传递到其它神经元。为了模拟神经细胞行为，与之对应的感知机基础概念被提出，如权量（突触）、偏置（阈值）及激活函数（细胞体）。
    * #### **对偶形式**  
    |**输入** |训练数据集 $T={(x_1,y_1),(x_2,y_2),...,(x_N,y_N)}$，其中$x_i$∈$R^n$,$y_i$∈{$\{+1,-1\}$}，学习率$η(0<η≤1)$|
    |:---------:|:-------------|
    |**输出** |a，b，感知机模型$f(x)=sign(\sum_{j=1}^{N}a_jy_jx_j·x+b)$ ,其中$a=(a_i,a_2,...,a_N)$|
    |**步骤**|（1）选取初始值a=0，b=0；<br>（2）在训练集中选取数据$(x_i,y_i)$；<br>  （3）如果存在误分类点，即$y_{i}(\sum_{j=1}^{N}a_jy_jx_j·x+b)≤0$，则<br>　　　　　　　　　　$a=a_i+η$<br>　　　　　　　　　　$b=b+ηy_i$  <br>（4）转（2），直至训练集中没有误分类点。|  
    |**解释**|（1）为了方便，可以预先将训练集中实例间的内积计算出来并以矩阵的形式存储，即Gram矩阵。$G_{N×N}=[x_{i}·y_{j}]$，可加快计算速度。<br> （2）由 $w=w+ηy_ix_i$，$b=b+ηy_i$， 可知，对于误分类点$(x_i, y_i)$,w, b关于该点的增量分别为$a_iy_ix_i$，$a_iy_i$，其中，$n_i$表示第i个实例点由于误分而进行更新的次数。因此最终w, b可表示为：<br>　　　　　　　　　　$w=\sum_{i=1}^{N}a_iy_ix_i$ <br>　　　　　　　　　　$b=\sum_{i=1}^{N}a_iy_i$  |
----
* ### k近邻法
----

* ### 朴素贝叶斯法
![朴素贝叶斯法](https://github.com/Changzhisong/MachineLearning/blob/master/朴素贝叶斯.jpg) 
----
* ### 决策树
    * #### **决策树学习基本算法**  
    
    |**输入**| 训练数据集$T={(x_1,y_1),(x_2,y_2),...,(x_N,y_N)}$ ,特征集A|
    |:----:|:-----|
    |**输出**| 决策树T 　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　  |  
    |**过程**|　　函数 TreeGenerate(D, A)  <br>1　　生成结点node;  <br>2　　**if** D中样本全属于同一类别C **then**  <br>3　　　　将node标记为C类叶结点; **return**  <br>4　　**end if**  <br>5　　**if** A == ∅ **OR** D中样本在A上取值相同 **then**  <br>6　　　　        将node标记为叶结点，其类别标记为D中样本数最多的类; **return**  <br>7　　**end if**  <br>8　　从A中选择最优划分属性$a_\*$;  <br>9　　**for** $a_\*$ 的每一个值 $a_\*^v$ **do**  <br>10　　　　为node生成一个分支;令$D_v$表示D中在$a_\*$上取值为$a_\*^v$的样本子集;  <br>11　　　　**if** $D_v$ 为空 **then**  <br>12　　　　　　将分支结点标记为叶结点，其类别标记为D(其父节点)中样本最多的类; **return**  <br>13　　　　**else**  <br>14　　　　　　以TreeGenerate($D_v$, A＼{$a_{*}$})为分支结点  <br>15　　　　**end if**  <br>16 　  **end for**  <br>|

