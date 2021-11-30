# CNN
## 关于CNN的两种理解方式  
背景：**图像识别**  
识别的对象为一维向量，dimension个数为n。  
假设一个图片的size是100\*100px,如果有红黄蓝三个维度，就是3个**channel**，如果是黑白两个维度，就是2个channel。总体就是3个100\*100的矩阵，每一个元素代表对应channel中对应位置的颜色深浅程度。
如果直接套用fully connected神经网络就会产生维度爆炸的问题。因此诞生了CNN。  
一、  
1）可以将一个网络分成多个**receptive field**，每个receptive field的大小相同，(最经典的receptive field的设置方式：kernal size3\*3)且可以重叠；  
2）**stride=2**，表示移动的量，如果移动后的receptive field超出了影像的范围，则需要通过**padding**来补充矩阵中的数值：补0/补平均值；  
3）一个pattern可能会在不同的额region涌现。假设一个neural可以识别一个pattern,涉及到一个receptive field,**一个receptive field可以对应多个neural**,不同neural可以实现参数共享：**sharing parameter**，参数的名称为filter；  
4）假设一个receptive field有64个neural,就有filter1、filter2...filter64，则对应的filter有相同的parameter。  
![image](https://user-images.githubusercontent.com/56083834/143990711-ee2cfcc6-6518-4a3b-a0c4-19536b991eb9.png)
![image](https://user-images.githubusercontent.com/56083834/143990951-e15b615e-0c0e-4c1b-87b4-bf95d7a46e71.png)

二、   
从filter的角度出发，假设一个filter是3\*3\*channel的tensor，将这个tensor扫描整张图片，和不同的receptive field做**内积**，假设图片的size=6,stride=1,最后会得到4\*4的矩阵，64个neural会得到64个4\*4的矩阵,则可以看成大小为4\*4,channel=64的图片，则下一层filter的dimension=64;  
![image](https://user-images.githubusercontent.com/56083834/143991708-122dd671-8622-4d57-a5c8-7cd31f476dc3.png)
![image](https://user-images.githubusercontent.com/56083834/143991868-bc1cb3ae-92ea-4cc7-abcb-8b8109927049.png)

**subsampling**  
对于图片我们可以进行压缩，可以用更少的parameter去进行训练。  
**pooling**  
convoluntion+pooling可以对于图片进行压缩。一般为两次convoluntion加一次pooling。  
**flatten**
flatten之后用fully connected network进行分类。  
![image](https://user-images.githubusercontent.com/56083834/143992345-e59aeda5-9eb9-43bc-a12c-c0291d71159e.png)



