# 机器学习笔记
2021李宏毅老师机器学习课程链接：https://www.bilibili.com/video/BV1Wv411h7kN
## 类神经网络训练不起来怎么办
### 1)局部最优(local minima)与鞍点(saddle point)
![ink-image](https://user-images.githubusercontent.com/56083834/142728141-8373f352-d983-4054-88ad-e29a03097273.png)
当gradient=0的时候，参数就会停止更新，
判断优化是否还能继续进行，需要看Hessian矩阵。
#### 局部最优和鞍点的区别
当H矩阵的特征值都为**负**时，就为**局部最优**；  

当H矩阵的特征值都为正时，就为local maxima；  

当H矩阵的特征值有正有负时，处于**鞍点**的状态，负特征值对应的特征向量表示模型可以优化的方向。  

### 2)批次(batch)和动量(momentum)
#### batch size的影响
![ink-image](https://user-images.githubusercontent.com/56083834/142729524-8dafb17d-f12f-4026-80a7-ab9b825e6380.png)

每一步中所有的batch都做过一次shuffle，因此每一个epoch中的batch中的样本可能都不一样；  

每一个batch都会计算出一个gradient和loss  

少量的batch(一个batch的size比较大)：更稳，技能冷却时间比较长(在GPU平行运算的情况下，运行时间在1000size内相差不大,但是更新的次数较少，**因此相对大的batch size比较快**)；  

大量的batch(一个batch的size比较小)：曲折，技能冷却时间比较短。  

**大的batch size会造成拟合结果变差**，是optimization的问题  

小的batch size在测试集上表现更好：local minima有两种，平缓地带为**flat minima**，峡谷地带为**sharp minima**(**大的batch size容易达到sharp minima**)。  

#### 动量的问题
加入动量之后，模型优化的方向不仅要向gradient的反方向移动，同时也会考虑到上一步移动的方向。

### 3)自动调整学习率
gradient比较大时,learning_rate理论上应该小一点；  

gradient比较小时,learning-rate理论上应该大一点

### 4)loss函数的影响
分类问题的**MSE**和**交叉熵函数**  
预测目标 **on-hot vector**  
和回归的区别:在output层重复n次操作(*weight+bias,n为类别数)  
y是一个向量，通常用softmax(y)得到y'
计算y和y^的距离  
1）MSE;2)Cross-trophy(避免梯度下降时stuck的情况)

### 5)批次标准化(batch normalization)
把error surface铲平，更容易train，当dimension之间的差距很大的时候，训练时不同特征的梯度变化不同，因此需要让feature中不同的dimension有相同的范围。  
feature normalization将输入值统一做标准化  
batch normalization可以放在激活函数前，也可以放在激活函数后。加入了这个操作后，每一个神经元都会有关联。  
注意只能针对于比较大的batch  
在test的时候，比如进行流计算的时候,一个batch是不足以算出mu和thigema，因此是采用移动平均的额方法去计算的  


