机器学习
=======

****
### Author:Song
### E-mail:Z.S.Chang@qq.com
****
参考自李航《统计学习方法》
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
    **输入：** 训练数据集$T={(x_1,y_1),(x_2,y_2),...,(x_N,y_N)}$ ，其中$x_i$∈$R^n$,$y_i$∈$\{+1,-1\}$，学习率$η(0<η≤1)$  
**输出：** w，b，感知机模型$f(x)=sign(w·x+b)$   
**步骤：**  
（1）选取初始值w0，b0；  
（2）在训练集中选取数据$(x_i,y_i)$；  
（3）如果存在误分类点，即$y_{i}(w·x+b)≤0$，则  
            　　　　　　　　　　$w=w+ηy_ix_i$  
            　　　　　　　　　　$b=b+ηy_i$  
（4）转（2），直至训练集中没有误分类点。   
**解释:**   
（1）目标是求参数w，b，使得损失函数：$min_{w,b}$ $L(w,b)=- \sum_{x_{i}∈M} y_{i}(w·x_i+b)$极小化。其中M为误分类点的集合。  
（2）采用随机梯度下降法（SGD）求解，即极小化过程中不是一次使M中所有误分类点的梯度下降，而是一次随机选取一个误分类点使其梯度下降。随机梯度下降的效率要高于批量梯度下降（batch gradient descent）  
（3）当一个实例点被误分类，即位于分离超平面的错误一侧时，则调整w，b的值，使分离超平面向该误分类点的一侧移动，以减少该误分类点与超平面简的距离，直至超平面越过该误分类点使其被正确分类。    
优缺点：  
（1）在感知机模型中，只要给出的数据是线性可分的，那么我们就能证明在有限次迭代过程中，能够收敛；  
（2）算法着重考虑是否将所有训练数据分类正确，而不考虑分的有多好，即存在无穷多个解，其解由于初值或不同的迭代顺序而可能有所不同；  
（3）感知机主要的本质缺陷是它不能处理线性不可分问题；  
（4）感知机因为是线性模型，所以不能表示复杂的函数，如异或，即感知机是无法处理异或问题，因为训练集线性不可分。  

    ```为什么叫“感知机”：感知机是生物神经细胞的简单抽象。神经细胞结构大致可分为：树突、突触、细胞体及轴突。单个神经细胞可被视为一种只有两种状态的机器——激动时为‘是’，而未激动时为‘否’。神经细胞的状态取决于从其它的神经细胞收到的输入信号量，及突触的强度（抑制或加强）。当信号量总和超过了某个阈值时，细胞体就会激动，产生电脉冲。电脉冲沿着轴突并通过突触传递到其它神经元。为了模拟神经细胞行为，与之对应的感知机基础概念被提出，如权量（突触）、偏置（阈值）及激活函数（细胞体）。```  

    * #### **对偶形式**  
    **输入：** 训练数据集 ，其中 ，学习率   
**输出：** a，b，感知机模型$f(x)=sign(\sum_{j=1}^{N}a_jy_jx_j·x+b)$ ,其中$a=(a_i,a_2,...,a_N)}$  
**步骤：**  
（1）选取初始值a=0，b=0；  
（2）在训练集中选取数据$(x_i,y_i)$；  
（3）如果存在误分类点，即$y_{i}(\sum_{j=1}^{N}a_jy_jx_j·x+b)≤0$，则  
　　　　　　　　　　$a=a_i+η$  
　　　　　　　　　　$b=b+ηy_i$  
（4）转（2），直至训练集中没有误分类点。  
为了方便，可以预先将训练集中实例间的内积计算出来并以矩阵的形式存储，即Gram矩阵。$G_{N×N}=[x_{i}·y_{j}]$，可加快计算速度。  
由 $w=w+ηy_ix_i$，$b=b+ηy_i$， 可知，对于误分类点$(x_i, y_i)$，w, b关于该点的增量分别为$a_iy_ix_i$ ， $a_iy_i$，其中 ，$n_i$表示第i个实例点由于误分而进行更新的次数。因此最终w, b可表示为：  
$w=\sum_{i=1}^{N}a_iy_ix_i$  
$b=\sum_{i=1}^{N}a_iy_i$  
----
2.k近邻法
输入：训练数据集 ，其中 为实例的特征向量， 为实例的类别；实例特征向量x。
输出：实例x所属的类y
步骤：
（1）根据给定的距离度量，在训练集中T中找出与x最邻近的k个点，涵盖着k个点的邻域记做 
（2）在 中根据分类决策规则（如多数表决）决定x的类别y：
 
其中I为指示函数，即当 时I为1，否则为0.
解释：
（1）给定一个训练数据集，对新的输入实例，在训练数据集中找到与该实例最邻近的k个实例，这k个实例的多数属于某个类，就把该输入实例分为这个类。
（2）分类决策规则通常采用多数表决，多数表决等价于经验风险最小化。
（3）通常采用交叉验证法来选取最优的k值。
实现：
A.构造平衡kd树
 
B.用kd树的最近邻搜索
输入：以构造的kd树，目标点x；
输出：x 的最近邻
步骤：
（1）在kd树种找出包含目标点x的叶结点：从根结点出发，递归地向下搜索kd树。若目标点x当前维的坐标小于切分点的坐标，则移动到左子结点，否则移动到右子结点，直到子结点为叶结点为止。
（2）以此叶结点为“当前最近点”。
（3）递归的向上回溯，在每个结点进行以下操作：
（3.a）如果该结点保存的实例点比当前最近点距离目标点更近，则更新“当前最近点”，也就是说以该实例点为“当前最近点”。
（3.b）当前最近点一定存在于该结点一个子结点对应的区域，检查子结点的父结点的另一子结点对应的区域是否有更近的点。具体做法是，检查另一子结点对应的区域是否以目标点位球心，以目标点与“当前最近点”间的距离为半径的圆或超球体相交：
如果相交，可能在另一个子结点对应的区域内存在距目标点更近的点，移动到另一个子结点，接着，继续递归地进行最近邻搜索；
如果不相交，向上回溯。
（4）当回退到根结点时，搜索结束，最后的“当前最近点”即为x 的最近邻点。
kd树解释：
（1）节点的数据结构：
 
（2）如果实例点是随机分布的，那么kd树搜索的平均计算复杂度是O（logN），这里的N是训练实例树。所以说，kd树更适用于训练实例数远大于空间维数时的k近邻搜索，当空间维数接近训练实例数时，它的效率会迅速下降，一降降到“解放前”：线性扫描的速度。
（3）kd树中，kd代表k-dimension，每个节点即为一个k维的点。每个非叶节点可以想象为一个分割超平面，用垂直于坐标轴的超平面将空间分为两个部分，这样递归的从根节点不停的划分，直到没有实例为止。
（4）建立kd-tree的时间复杂度为O(k*n*logn)。
（5）怎样确定在哪个维度上进行划分：①.轮着来：j = (i mod k) + 1。②.最大方差法。
（6）怎样确保在这一维度上的划分得到的两个子集合的数量尽量相等，即左子树和右子树中的结点个数尽量相等：中位数

 
3.朴素贝叶斯
输入：训练数据 ,其中 ， 是第i个样本的第j个特征， ， 是第j个特征可能取的第l个值， ， ， ；实例 。
输出：实例 的分类。
步骤：
（1）计算先验概率及条件概率
 
 
（2）对于给定的实例 ，计算
 
（3）确定实例 的分类
 
解释：
（1）极大似然估计可替换为贝叶斯估计，用来防止极大似然估计会出现估计的概率值为0的情况。
 
 
 
4.决策树
信息增益算法
输入：训练数据集D和特征A
输出：特征A对训练数据集D的信息增益g(D,A)
步骤：
（1）计算数据集D的经验熵H(D)
 
其中， 为样本个数， 为属于类 的个数，k=1,2,…,K
（2）计算特征A对数据集D的经验条件熵H(D|A):
 
其中，特征A有n个不同的取值 ,根据特征A的取值将D划分为n个子集D1，D2，…,Dn，|Di|为特征值取an时的样本个数，子集Di中属于类Ck的样本集合为Dik。
（3）计算信息增益
 
ID3算法
输入：训练数据集D和特征集A，阈值ε；
输出：决策树T
步骤：
（1）若D中所有实例属于同一类Ck，则T为单节点树，并将类Ck作为该节点的类标记，返回T；
（2）若A= ，则T为点节点树，并将D中为实例数最大的类Ck作为该节点的类标记，返回T；
（3）否则，按信息增益算法计算A中各特征对D的信息增益，选择信息增益最大的特征Ag；
（4）如果Ag的信息增益小于阈值ε，则置T为单节点树，并将D中实例数最大的类Ck作为该节点的类标记，返回T；
（5）否则，对Ag的每一可能值ai，依Ag=ai将D分割为若干非空子集Di,将Di中实例数最大的类作为标记，构建子节点，由节点及子节点构成树T，返回T；
（6）对第i个子节点，以Di为训练集，以A-{Ag}为特征集，递归地调用（1）~（5），得到子树Ti，返回Ti。
C4.5的生成算法
输入：训练数据集D和特征集A，阈值ε；
输出：决策树T
步骤：
（1）若D中所有实例属于同一类Ck，则T为单节点树，并将类Ck作为该节点的类标记，返回T；
（2）若A= ，则T为点节点树，并将D中为实例数最大的类Ck作为该节点的类标记，返回T；
（3）否则，按信息增益比公式( )计算A中各特征对D的信息增益比，选择信息增益比最大的特征Ag；
（4）如果Ag的信息增益小于阈值ε，则置T为单节点树，并将D中实例数最大的类Ck作为该节点的类标记，返回T；
（5）否则，对Ag的每一可能值ai，依Ag=ai将D分割为若干非空子集Di,将Di中实例数最大的类作为标记，构建子节点，由节点及子节点构成树T，返回T；
（6）对第i个子节点，以Di为训练集，以A-{Ag}为特征集，递归地调用（1）~（5），得到子树Ti，返回Ti。
树的剪枝算法
输入：生成算法产生的整个数T，参数α；
输出：修剪后的子树Tα
步骤：
（1）计算每个节点的经验熵；
（2）递归的从树的叶节点向上回缩，若回缩后的整体树TA的损失函数值小于回缩到父节点之前TB的损失函数值则进行剪枝( )，即将父节点变为新的叶节点。
其中决策树的损失函数为 ，树T的叶节点个数为|T|，t是树T的叶节点，该叶节点有Nt个样本点，其中k类样本点有Ntk个，叶节点t上的经验熵为 
（3）返回（2），直至不能继续为止，得到损失函数最小的子数Tα
CART算法

最小二乘回归树生成算法
输入：训练数据集D
输出：回归树f(x)
步骤：
在训练数据集所在的输入空间中，递归地将每一个区域划分为两个子区域并决定每个子区域上的输出值，构建二叉决策树：
（1）选择最优切分变量j与切分点s，求解
 
（2）用选定的(j,s)对划分区域并决定相应的输出值：
 
 
（3）继续对两个子区域调用步骤（1），（2），直至满足停止条件；
（4）将输入空间划分为M个区域 ，生成决策树：
 
