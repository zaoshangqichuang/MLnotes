# 机器学习笔记
2021李宏毅老师机器学习课程链接：https://www.bilibili.com/video/BV1Wv411h7kN
## 类神经网络训练不起来怎么办
### 局部最优(local minima)与鞍点(saddle point)
![ink-image](https://user-images.githubusercontent.com/56083834/142728141-8373f352-d983-4054-88ad-e29a03097273.png)
当gradient=0的时候，参数就会停止更新，
判断优化是否还能继续进行，需要看Hessian矩阵。
#### 局部最优和鞍点的区别
当H矩阵的特征值都为负时，就为局部最优
当H矩阵的特征值都为正时，就为local maxima
当H矩阵的特征值有正有负时，处于鞍点的状态，负特征值 $\lambda$
