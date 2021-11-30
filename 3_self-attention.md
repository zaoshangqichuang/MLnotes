# 背景
自注意力机制适应于复杂的输入情况：  
复杂的输入情况：  
1、当input是一个vector时，输出可能是一个值或一个类别；  
2、当input是一排vector时，输出可能是一排值或一排类别。   
* input和输出的dimension相同(词性辨析)或不同（语义辨析）  
如果直接把input flatten，加入到fully connected vector时，参数过多，因此需要将input压缩，同时考虑到context。


# self-attention的应用场景  
word embedding ：一个句子中有多个词语，一个词语为一个向量，相同语义的词向量相似度会更高。  
* 语音处理，例如[HW2](https://github.com/zaoshangqichuang/MLnotes/blob/main/HW2-1_classification.ipynb),25ms为1个frame,stripe=10ms,1s就有100个frame。  
* 图网络：每一个个体就代表一个vector  
![image](https://user-images.githubusercontent.com/56083834/144010249-ff6fafc0-944b-4fd3-a2d3-36af5abe4014.png)
![image](https://user-images.githubusercontent.com/56083834/144010301-9c7b3c67-8044-40e4-a533-815617a9959c.png)

# self-attention的操作方法  
1）**Dot-product**  
三个矩阵Wq Wk Wv的参数需要进行学习，其它的都是已知的   
![image](https://user-images.githubusercontent.com/56083834/144010549-7d527b09-b7d4-42c6-a1d9-2dd83105dbba.png)
![image](https://user-images.githubusercontent.com/56083834/144011458-4f074880-6c8a-4e6c-bc2b-34c701b6024a.png)

* 每一个向量a都需要映射为向量b  
* 先计算Wq\*a1=q1,再分别计算Wk\*a2、Wk\*a3、Wk\*a4，然后计算α12=q1\*k2,最后再将α向量进行soft-max，最后bi=∑j αij'*vj
2) Additive（不常用）  

# Muti-head self-attention
考虑到不同类型可能有不同的相关性，一个type可能有不同的relevance。  
![image](https://user-images.githubusercontent.com/56083834/144011785-10e47d48-85e7-4ba8-ae4b-44fc9d2dc332.png)

# Positional Encoding  
会在输入向量中加入位置的信息ei+ai  

# truncated self-attention  
attention只考虑到部分范围


# self-attention和CNN的关系  
CNN是self-attention的子集，CNN是规定好的receptive field，但是self-attention还需要进行学习。CNN弹性比较小，更适用于小规模的数据集，防止过拟合。  

# self-attention和RNN的关系
RNN的b不是平行产生的，但是self-attention可以进行并行处理。  
![image](https://user-images.githubusercontent.com/56083834/144017730-0b45718d-0bbf-40dc-b325-b6da5fac09bf.png)
