# 机器学习笔记
2021李宏毅老师机器学习课程链接：https://www.bilibili.com/video/BV1Wv411h7kN
## 类神经网络训练不起来怎么办
### 局部最优(local minima)与鞍点(saddle point)
![ink-image](https://user-images.githubusercontent.com/56083834/142728141-8373f352-d983-4054-88ad-e29a03097273.png)
当gradient=0的时候，参数就会停止更新，
判断优化是否还能继续进行，需要看Hessian矩阵。
#### 局部最优和鞍点的区别
当H矩阵的特征值都为**负**时，就为**局部最优**；  

当H矩阵的特征值都为正时，就为local maxima；  

当H矩阵的特征值有正有负时，处于**鞍点**的状态，负特征值对应的特征向量表示模型可以优化的方向。  

### 批次(batch)和动量(momentum)
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

### 自动调整学习率
gradient比较大时,learning_rate理论上应该小一点；  

gradient比较小时,learning-rate理论上应该大一点

