---
title: 第二章 Transformer
tags: [Transformer]
published: true
hideInList: false
isTop: false
date: 
feature:
sticky: 
top: 
category: 学习 # 分类 Python
---
## 2.2 输入部分实现 P4

- 学习目标

  - 了解文本嵌入层和位置编码的作用.

  - 掌握文本嵌入层和位置编码的实现过程.


------

- 输入部分包含:
  - 源文本嵌入层及其位置编码器
  - 目标文本嵌入层及其位置编码器


![image-20231108193413280](https://cdn.jsdelivr.net/gh/beiyoudaxue/pic2023@main/img/image-20231108193413280.png)

### 文本嵌入层的作用

- 无论是源文本嵌入还是目标文本嵌入，都是为了将文本中词汇的数字表示转变为向量表示, 希望在这样的高维空间捕捉词汇间的关系.

------

- pytorch 0.3.0及其必备工具包的安装:

  ### 安装版本

```python
# 使用pip安装的工具包包括pytorch-0.3.0, numpy, matplotlib, seaborn
pip install http://download.pytorch.org/whl/cu80/torch-0.3.0.post4-cp36-cp36m-linux_x86_64.whl numpy matplotlib seaborn

# MAC系统安装, python版本<=3.6
pip install torch==0.3.0.post4 numpy matplotlib seaborn
```

```python
conda create -n postcoding python=3.0
conda activate postcoding

pip3 install torch==1.10.0+cu113 torchvision==0.11.1+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html -i https://pypi.douban.com/simple
pip install xlrd==1.2.0
pip install xlrd==4.64.1
pip install matplotlib==3.2.0 -i https://pypi.douban.com/simple/
```

- 文本嵌入层的代码分析:

```python
# 导入必备的工具包
import torch

# 预定义的网络层torch.nn, 工具开发者已经帮助我们开发好的一些常用层, 
# 比如，卷积层, lstm层, embedding层等, 不需要我们再重新造轮子.
import torch.nn as nn

# 数学计算工具包
import math

# torch中变量封装函数Variable.
from torch.autograd import Variable

# 定义Embeddings类来实现文本嵌入层，这里s说明代表两个一模一样的嵌入层, 他们共享参数.
# 该类继承nn.Module, 这样就有标准层的一些功能, 这里我们也可以理解为一种模式, 我们自己实现的所有层都会这样去写.
class Embeddings(nn.Module):
    def __init__(self, d_model, vocab):
        """类的初始化函数, 有两个参数, d_model: 指词嵌入的维度, vocab: 指词表的大小."""
        # 接着就是使用super的方式指明继承nn.Module的初始化函数, 我们自己实现的所有层都会这样去写.
        super(Embeddings, self).__init__()
        # 之后就是调用nn中的预定义层Embedding, 获得一个词嵌入对象self.lut
        self.lut = nn.Embedding(vocab, d_model)
        # 最后就是将d_model传入类中
        self.d_model = d_model

    def forward(self, x):
        """可以将其理解为该层的前向传播逻辑，所有层中都会有此函数
           当传给该类的实例化对象参数时, 自动调用该类函数
           参数x: 因为Embedding层是首层, 所以代表输入给模型的文本通过词汇映射后的张量"""

        # 将x传给self.lut并与根号下self.d_model相乘作为结果返回
        return self.lut(x) * math.sqrt(self.d_model)	# sqrt(self.d_model)缩放作用
```

`P5`

- nn.Embedding演示:

```python
>>> embedding = nn.Embedding(10, 3)
>>> input = torch.LongTensor([[1,2,4,5],[4,3,2,9]])
>>> embedding(input)
tensor([[[-0.0251, -1.6902,  0.7172],
         [-0.6431,  0.0748,  0.6969],
         [ 1.4970,  1.3448, -0.9685],
         [-0.3677, -2.7265, -0.1685]],

        [[ 1.4970,  1.3448, -0.9685],
         [ 0.4362, -0.4004,  0.9400],
         [-0.6431,  0.0748,  0.6969],
         [ 0.9124, -2.3616,  1.1151]]])


>>> embedding = nn.Embedding(10, 3, padding_idx=0)
>>> input = torch.LongTensor([[0,2,0,5]])
>>> embedding(input)
tensor([[[ 0.0000,  0.0000,  0.0000],
         [ 0.1535, -2.0309,  0.9315],
         [ 0.0000,  0.0000,  0.0000],
         [-0.1655,  0.9897,  0.0635]]])
```

- 实例化参数:

```python
# 词嵌入维度是512维
d_model = 512

# 词表大小是1000
vocab = 1000
```

- 输入参数:

```python
# 输入x是一个使用Variable封装的长整型张量, 形状是2 x 4
x = Variable(torch.LongTensor([[100,2,421,508],[491,998,1,221]]))
```

------

- 调用:

```python
emb = Embeddings(d_model, vocab)
embr = emb(x)
print("embr:", embr)
```

- 输出效果:

```python
embr: Variable containing:
( 0 ,.,.) = 
  35.9321   3.2582 -17.7301  ...    3.4109  13.8832  39.0272
   8.5410  -3.5790 -12.0460  ...   40.1880  36.6009  34.7141
 -17.0650  -1.8705 -20.1807  ...  -12.5556 -34.0739  35.6536
  20.6105   4.4314  14.9912  ...   -0.1342  -9.9270  28.6771

( 1 ,.,.) = 
  27.7016  16.7183  46.6900  ...   17.9840  17.2525  -3.9709
   3.0645  -5.5105  10.8802  ...  -13.0069  30.8834 -38.3209
  33.1378 -32.1435  -3.9369  ...   15.6094 -29.7063  40.1361
 -31.5056   3.3648   1.4726  ...    2.8047  -9.6514 -23.4909
[torch.FloatTensor of size 2x4x512]
```

- 输出效果

```python
import torch
import torch.nn as nn
import torch.nn.functional as F
from torch.autograd import Variable
import math
import matplotlib.pyplot as plt
import numpy as np
import copy


# embedding = nn.Embedding(10, 3)
# input1 = torch.LongTensor([[1,2,4,5],[4,3,2,9]])
# embedding = nn.Embedding(10, 3)
# input1 = torch.LongTensor([[1 ,2, 4, 5], [4, 3, 2, 9]])
# print(embedding(input1))
# embedding = nn.Embedding(10, 3, padding_idx=0)
# input1 = torch.LongTensor([[0, 2, 0, 5]])
# print(embedding(input1))
# 构建Embedding类来实现文本嵌入层
class Embeddings(nn.Module):
    def __init__(self, d_model, vocab):
        # d_model: 词嵌入的维度
        # vocab: 词表的大小
        super(Embeddings, self).__init__()
        # 定义Embedding层
        self.lut = nn.Embedding(vocab, d_model)
        # 将参数传入到类中
        self.d_model = d_model

    def forward(self, x):
        # x：代表输入进模型的文本通过词汇映射后的数字张量
        return self.lut(x) * math.sqrt(self.d_model)


# 实例化参数
d_model = 512
vocab = 1000

x = Variable(torch.LongTensor([[100, 2, 421, 508], [491, 998, 1, 221]]))

emb = Embeddings(d_model, vocab)
embr = emb(x)
print("embr:", embr)
print(embr.shape)
```

`P 6 位置编码器的作用`

因为在Transformer的编码器结构中, 并没有针对词汇位置信息的处理，因此需要在Embedding层后加入位置编码器，将词汇位置不同可能会产生不同语义的信息加入到词嵌入张量中, 以弥补位置信息的缺失

- 位置编码器的代码分析:

```python
# 定义位置编码器类, 我们同样把它看做一个层, 因此会继承nn.Module    
class PositionalEncoding(nn.Module):
    def __init__(self, d_model, dropout, max_len=5000):
        """位置编码器类的初始化函数, 共有三个参数, 分别是d_model: 词嵌入维度, 
           dropout: 置0比率, max_len: 每个句子的最大长度"""
        super(PositionalEncoding, self).__init__()

        # 实例化nn中预定义的Dropout层, 并将dropout传入其中, 获得对象self.dropout
        self.dropout = nn.Dropout(p=dropout)

        # 初始化一个位置编码矩阵, 它是一个0阵，矩阵的大小是max_len x d_model.
        pe = torch.zeros(max_len, d_model)	# 行 和 列

        # 初始化一个绝对位置矩阵, 在我们这里，词汇的绝对位置就是用它的索引去表示. 
        # 所以我们首先使用arange方法获得一个连续自然数向量，然后再使用unsqueeze方法拓展向量维度使其成为矩阵， 
        # 又因为参数传的是1，代表矩阵拓展的位置，会使向量变成一个max_len x 1 的矩阵， 
        position = torch.arange(0, max_len).unsqueeze(1)

        # 绝对位置矩阵初始化之后，接下来就是考虑如何将这些位置信息加入到位置编码矩阵中，
        # 最简单思路就是先将max_len x 1的绝对位置矩阵， 变换成max_len x d_model形状，然后覆盖原来的初始位置编码矩阵即可， 
        # 要做这种矩阵变换，就需要一个1xd_model形状的变换矩阵div_term，我们对这个变换矩阵的要求除了形状外，
        # 还希望它能够将自然数的绝对位置编码缩放成足够小的数字，有助于在之后的梯度下降过程中更快的收敛.  这样我们就可以开始初始化这个变换矩阵了.
        # 首先使用arange获得一个自然数矩阵， 但是细心的同学们会发现， 我们这里并没有按照预计的一样初始化一个1xd_model的矩阵， 
        # 而是有了一个跳跃，只初始化了一半即1xd_model/2 的矩阵。 为什么是一半呢，其实这里并不是真正意义上的初始化了一半的矩阵，
        # 我们可以把它看作是初始化了两次，而每次初始化的变换矩阵会做不同的处理，第一次初始化的变换矩阵分布在正弦波上， 第二次初始化的变换矩阵分布在余弦波上， 
        # 并把这两个矩阵分别填充在位置编码矩阵的偶数和奇数位置上，组成最终的位置编码矩阵.
        div_term = torch.exp(torch.arange(0, d_model, 2) *
                             -(math.log(10000.0) / d_model))
        pe[:, 0::2] = torch.sin(position * div_term)	# 偶数列
        pe[:, 1::2] = torch.cos(position * div_term)

        # 这样我们就得到了位置编码矩阵pe, pe现在还只是一个二维矩阵，要想和embedding的输出（一个三维张量）相加，
        # 就必须拓展一个维度，所以这里使用unsqueeze拓展维度.
        pe = pe.unsqueeze(0)

        # 最后把pe位置编码矩阵注册成模型的buffer，什么是buffer呢，
        # 我们把它认为是对模型效果有帮助的，但是却不是模型结构中超参数或者参数，不需要随着优化步骤进行更新的增益对象. 
        # 注册之后我们就可以在模型保存后重加载时和模型结构与参数一同被加载.
        self.register_buffer('pe', pe)

    def forward(self, x):
        """forward函数的参数是x, 表示文本序列的词嵌入表示"""
        # 在相加之前我们对pe做一些适配工作， 将这个三维张量的第二维也就是句子最大长度的那一维将切片到与输入的x的第二维相同即x.size(1)，
        # 因为我们默认max_len为5000一般来讲实在太大了，很难有一条句子包含5000个词汇，所以要进行与输入张量的适配. 
        # 最后使用Variable进行封装，使其与x的样式相同，但是它是不需要进行梯度求解的，因此把requires_grad设置成false.
        x = x + Variable(self.pe[:, :x.size(1)], 
                         requires_grad=False)
        # 最后使用self.dropout对象进行'丢弃'操作, 并返回结果.
        return self.dropout(x)
```

- nn.Dropout演示:

```python
>>> m = nn.Dropout(p=0.2)
>>> input = torch.randn(4, 5)
>>> output = m(input)
>>> output
Variable containing:
 0.0000 -0.5856 -1.4094  0.0000 -1.0290
 2.0591 -1.3400 -1.7247 -0.9885  0.1286
 0.5099  1.3715  0.0000  2.2079 -0.5497
-0.0000 -0.7839 -1.2434 -0.1222  1.2815
[torch.FloatTensor of size 4x5]
```

- torch.unsqueeze演示:

```python
>>> x = torch.tensor([1, 2, 3, 4])
>>> torch.unsqueeze(x, 0)
tensor([[ 1,  2,  3,  4]])
>>> torch.unsqueeze(x, 1)
tensor([[ 1],
        [ 2],
        [ 3],
        [ 4]])
```

- 实例化参数:

```python
# 词嵌入维度是512维
d_model = 512

# 置0比率为0.1
dropout = 0.1

# 句子最大长度
max_len=60
```

------

- 输入参数:

```python
# 输入x是Embedding层的输出的张量, 形状是2 x 4 x 512
x = embr
Variable containing:
( 0 ,.,.) = 
  35.9321   3.2582 -17.7301  ...    3.4109  13.8832  39.0272
   8.5410  -3.5790 -12.0460  ...   40.1880  36.6009  34.7141
 -17.0650  -1.8705 -20.1807  ...  -12.5556 -34.0739  35.6536
  20.6105   4.4314  14.9912  ...   -0.1342  -9.9270  28.6771

( 1 ,.,.) = 
  27.7016  16.7183  46.6900  ...   17.9840  17.2525  -3.9709
   3.0645  -5.5105  10.8802  ...  -13.0069  30.8834 -38.3209
  33.1378 -32.1435  -3.9369  ...   15.6094 -29.7063  40.1361
 -31.5056   3.3648   1.4726  ...    2.8047  -9.6514 -23.4909
[torch.FloatTensor of size 2x4x512]
```

- 调用:

```python
pe = PositionalEncoding(d_model, dropout, max_len)
pe_result = pe(x)
print("pe_result:", pe_result)
```

------

- 输出效果:

```python
pe_result: Variable containing:
( 0 ,.,.) = 
 -19.7050   0.0000   0.0000  ...  -11.7557  -0.0000  23.4553
  -1.4668 -62.2510  -2.4012  ...   66.5860 -24.4578 -37.7469
   9.8642 -41.6497 -11.4968  ...  -21.1293 -42.0945  50.7943
   0.0000  34.1785 -33.0712  ...   48.5520   3.2540  54.1348

( 1 ,.,.) = 
   7.7598 -21.0359  15.0595  ...  -35.6061  -0.0000   4.1772
 -38.7230   8.6578  34.2935  ...  -43.3556  26.6052   4.3084
  24.6962  37.3626 -26.9271  ...   49.8989   0.0000  44.9158
 -28.8435 -48.5963  -0.9892  ...  -52.5447  -4.1475  -3.0450
[torch.FloatTensor of size 2x4x512]
```

------

- 绘制词汇向量中特征的分布曲线:

```python
import matplotlib.pyplot as plt

# 创建一张15 x 5大小的画布
plt.figure(figsize=(15, 5))

# 实例化PositionalEncoding类得到pe对象, 输入参数是20和0
pe = PositionalEncoding(20, 0)

# 然后向pe传入被Variable封装的tensor, 这样pe会直接执行forward函数, 
# 且这个tensor里的数值都是0, 被处理后相当于位置编码张量
y = pe(Variable(torch.zeros(1, 100, 20)))

# 然后定义画布的横纵坐标, 横坐标到100的长度, 纵坐标是某一个词汇中的某维特征在不同长度下对应的值
# 因为总共有20维之多, 我们这里只查看4，5，6，7维的值.
plt.plot(np.arange(100), y[0, :, 4:8].data.numpy())

# 在画布上填写维度提示信息
plt.legend(["dim %d"%p for p in [4,5,6,7]])
```

- 输出效果:

![img](https://pic3.zhimg.com/80/v2-0c210867908a13e1f477e491ec5a2062_720w.webp)

效果分析:

- 每条颜色的曲线代表某一个词汇中的特征在不同位置的含义.

- 保证同一词汇随着所在位置不同它对应位置嵌入向量会发生变化.

- 正弦波和余弦波的值域范围都是1到-1这又很好的控制了嵌入数值的大小, 有助于梯度的快速计算.

`小节总结` p8

- 学习了文本嵌入层的作用:
  - 无论是源文本嵌入还是目标文本嵌入，都是为了将文本中词汇的数字表示转变为向量表示, 希望在这样的高维空间捕捉词汇间的关系.


------

- 学习并实现了文本嵌入层的类: Embeddings
  - 初始化函数以d_model, 词嵌入维度, 和vocab, 词汇总数为参数, 内部主要使用了nn中的预定层Embedding进行词嵌入.
  - 在forward函数中, 将输入x传入到Embedding的实例化对象中, 然后乘以一个根号下d_model进行缩放, 控制数值大小.
  - 它的输出是文本嵌入后的结果.


------

- 学习了位置编码器的作用:
  - 因为在Transformer的编码器结构中, 并没有针对词汇位置信息的处理，因此需要在Embedding层后加入位置编码器，将词汇位置不同可能会产生不同语义的信息加入到词嵌入张量中, 以弥补位置信息的缺失.


------

- 学习并实现了位置编码器的类: PositionalEncoding
  - 初始化函数以d_model, dropout, max_len为参数, 分别代表d_model: 词嵌入维度, dropout: 置0比率, max_len: 每个句子的最大长度.
  - forward函数中的输入参数为x, 是Embedding层的输出.
  - 最终输出一个加入了位置编码信息的词嵌入张量.


------

- 实现了绘制词汇向量中特征的分布曲线:
  - 保证同一词汇随着所在位置不同它对应位置嵌入向量会发生变化.
  - 正弦波和余弦波的值域范围都是1到-1, 这又很好的控制了嵌入数值的大小, 有助于梯度的快速计算.


## 2.3 编码器部分实现 P10

- 学习目标

  - 了解编码器中各个组成部分的作用.

  - 掌握编码器中各个组成部分的实现过程.


------

- 编码器部分:
  - 由N个编码器层堆叠而成
  - 每个编码器层由两个子层连接结构组成
  - 第一个子层连接结构包括一个多头自注意力子层和规范化层以及一个残差连接
  - 第二个子层连接结构包括一个前馈全连接子层和规范化层以及一个残差连接


![img](https://pic1.zhimg.com/80/v2-306c89830ea9efe5953ae4d8b76492a4_1440w.webp)

- 什么是掩码张量:
  - 掩代表遮掩，码就是我们张量中的数值，它的尺寸不定，里面一般只有`1`和`0`的元素，代表位置被遮掩或者不被遮掩，至于是0位置被遮掩还是1位置被遮掩可以自定义，因此它的作用就是`让另外一个张量中的一些数值被遮掩`，也可以说被替换, 它的表现形式是一个张量.


------

- 掩码张量的作用:
  - 在transformer中, 掩码张量的主要作用在应用`attention`(将在下一小节讲解)时，有一些生成的attention张量中的值计算有可能已知了未来信息而得到的，未来信息被看到是因为训练时会把整个输出结果都一次性进行Embedding，但是理论上解码器的的输出却不是一次就能产生最终结果的，而是一次次通过上一次结果综合得出的，因此，未来的信息可能被提前利用. 所以，我们会进行遮掩. 关于解码器的有关知识将在后面的章节中讲解.


------

- 生成掩码张量的代码分析:

```python
def subsequent_mask(size):
    """生成向后遮掩的掩码张量, 参数size是掩码张量最后两个维度的大小, 它的最后两维形成一个方阵"""
    # 在函数中, 首先定义掩码张量的形状
    attn_shape = (1, size, size)

    # 然后使用np.ones方法向这个形状中添加1元素,形成上三角阵, 最后为了节约空间, 
    # 再使其中的数据类型变为无符号8位整形unit8 
    subsequent_mask = np.triu(np.ones(attn_shape), k=1).astype('uint8')

    # 最后将numpy类型转化为torch中的tensor, 内部做一个1 - 的操作, 
    # 在这个其实是做了一个三角阵的反转, subsequent_mask中的每个元素都会被1减, 
    # 如果是0, subsequent_mask中的该位置由0变成1
    # 如果是1, subsequent_mask中的该位置由1变成0 
    return torch.from_numpy(1 - subsequent_mask)
```

------

- np.triu演示:

```python
>>> np.triu([[1,2,3],[4,5,6],[7,8,9],[10,11,12]], k=-1)
array([[ 1,  2,  3],
       [ 4,  5,  6],
       [ 0,  8,  9],
       [ 0,  0, 12]])


>>> np.triu([[1,2,3],[4,5,6],[7,8,9],[10,11,12]], k=0)
array([[ 1,  2,  3],
       [ 0,  5,  6],
       [ 0,  0,  9],
       [ 0,  0, 0]])


>>> np.triu([[1,2,3],[4,5,6],[7,8,9],[10,11,12]], k=1)
array([[ 0,  2,  3],
       [ 0,  0,  6],
       [ 0,  0,  0],
       [ 0,  0, 0]])
```

------

- 输入实例:

```python
# 生成的掩码张量的最后两维的大小
size = 5
```

- 调用:

```python
sm = subsequent_mask(size)
print("sm:", sm)
```

------

- 输出效果:

```python
# 最后两维形成一个下三角阵
sm: (0 ,.,.) = 
  1  0  0  0  0
  1  1  0  0  0
  1  1  1  0  0
  1  1  1  1  0
  1  1  1  1  1
[torch.ByteTensor of size 1x5x5]
```

------

`P 11 `

- 掩码张量的可视化:

```python
plt.figure(figsize=(5,5))
plt.imshow(subsequent_mask(20)[0])
```

------

- 输出效果:

![img](https://pic1.zhimg.com/80/v2-7e76569222acd94a74de6d2ba5efa824_1440w.webp)

效果分析:

- 通过观察可视化方阵, 黄色是1的部分, 这里代表被遮掩, 紫色代表没有被遮掩的信息, 横坐标代表目标词汇的位置, 纵坐标代表可查看的位置;
- 我们看到, 在0的位置我们一看望过去都是黄色的, 都被遮住了，1的位置一眼望过去还是黄色, 说明第一次词还没有产生, 从第二个位置看过去, 就能看到位置1的词, 其他位置看不到, 以此类推.

`总结`

- 学习了什么是掩码张量:
  - 掩代表遮掩，码就是我们张量中的数值，它的尺寸不定，里面一般只有1和0的元素，代表位置被遮掩或者不被遮掩，至于是0位置被遮掩还是1位置被遮掩可以自定义，因此它的作用就是让另外一个张量中的一些数值被遮掩, 也可以说被替换, 它的表现形式是一个张量.


------

- 学习了掩码张量的作用:
  - 在transformer中, 掩码张量的主要作用在应用attention(将在下一小节讲解)时，有一些生成的attetion张量中的值计算有可能已知量未来信息而得到的，未来信息被看到是因为训练时会把整个输出结果都一次性进行Embedding，但是理论上解码器的的输出却不是一次就能产生最终结果的，而是一次次通过上一次结果综合得出的，因此，未来的信息可能被提前利用. 所以，我们会进行遮掩. 关于解码器的有关知识将在后面的章节中讲解.


------

- 学习并实现了生成向后遮掩的掩码张量函数: subsequent_mask
  - 它的输入是size, 代表掩码张量的大小.
  - 它的输出是一个最后两维形成1方阵的下三角阵.
  - 最后对生成的掩码张量进行了可视化分析, 更深一步理解了它的用途.


### 2.3.2 注意力机制 P13

- 学习目标:
  - 了解什么是注意力计算规则和注意力机制.
  - 掌握注意力计算规则的实现过程.


------

- 什么是注意力:
  - 我们观察事物时，之所以能够快速判断一种事物(当然允许判断是错误的), 是因为我们大脑能够很快把注意力放在事物最具有辨识度的部分从而作出判断，而并非是从头到尾的观察一遍事物后，才能有判断结果. 正是基于这样的理论，就产生了注意力机制.


------

- 什么是注意力计算规则:
  - 它需要三个指定的输入Q(query), K(key), V(value), 然后通过公式得到注意力的计算结果, 这个结果代表query在key和value作用下的表示. 而这个具体的计算规则有很多种, 我这里只介绍我们用到的这一种.


------

- 我们这里使用的注意力的计算规则:
  $$
  \mathrm{Attention}(Q,K,V)=\mathrm{softmax}(\frac{QK^{T}}{\sqrt{d_{k}}})V
  $$
  
- Q, K, V 的比喻解释:

```python
假如我们有一个问题: 给出一段文本，使用一些关键词对它进行描述!
为了方便统一正确答案，这道题可能预先已经给大家写出了一些关键词作为提示.其中这些给出的提示就可以看作是key
而整个的文本信息就相当于是query，value的含义则更抽象，可以比作是你看到这段文本信息后，脑子里浮现的答案信息
这里我们又假设大家最开始都不是很聪明，第一次看到这段文本后脑子里基本上浮现的信息就只有提示这些信息
因此key与value基本是相同的，但是随着我们对这个问题的深入理解，通过我们的思考脑子里想起来的东西原来越多
并且能够开始对我们query也就是这段文本，提取关键信息进行表示.  这就是注意力作用的过程， 通过这个过程，
我们最终脑子里的value发生了变化
根据提示key生成了query的关键词表示方法，也就是另外一种特征表示方法.

刚刚我们说到key和value一般情况下默认是相同，与query是不同的，这种是我们一般的注意力输入形式
# 但有一种特殊情况，就是我们query与key和value相同，这种情况我们称为自注意力机制，就如同我们的刚刚的例子
使用一般注意力机制，是使用不同于给定文本的关键词表示它. 而自注意力机制
需要用给定文本自身来表达自己，也就是说你需要从给定文本中抽取关键词来表述它, 相当于对文本自身的一次特征提取.
```

------

- 什么是注意力机制:
  - 注意力机制是注意力计算规则能够应用的深度学习网络的载体, 除了注意力计算规则外, 还包括一些必要的全连接层以及相关张量处理, 使其与应用网络融为一体. 使用自注意力计算规则的注意力机制称为自注意力机制.


------

- 注意力机制在网络中实现的图形表示:

![img](https://pic1.zhimg.com/80/v2-d7913da8a83d6ca9d67524560b263688_1440w.webp)

`P14` 

- 注意力计算规则的代码分析:

```python
def attention(query, key, value, mask=None, dropout=None):
    """注意力机制的实现, 输入分别是query, key, value, mask: 掩码张量, 
       dropout是nn.Dropout层的实例化对象, 默认为None"""
    # 在函数中, 首先取query的最后一维的大小, 一般情况下就等同于我们的词嵌入维度, 命名为d_k
    d_k = query.size(-1)
    # 按照注意力公式, 将query与key的转置相乘, 这里面key是将最后两个维度进行转置, 再除以缩放系数根号下d_k, 这种计算方法也称为缩放点积注意力计算.
    # 得到注意力得分张量scores
    scores = torch.matmul(query, key.transpose(-2, -1)) / math.sqrt(d_k)

    # 接着判断是否使用掩码张量
    if mask is not None:
        # 使用tensor的masked_fill方法, 将掩码张量和scores张量每个位置一一比较, 如果掩码张量处为0
        # 则对应的scores张量用-1e9这个值来替换, 如下演示
        scores = scores.masked_fill(mask == 0, -1e9)

    # 对scores的最后一维进行softmax操作, 使用F.softmax方法, 第一个参数是softmax对象, 第二个是目标维度.
    # 这样获得最终的注意力张量
    p_attn = F.softmax(scores, dim = -1)

    # 之后判断是否使用dropout进行随机置0
    if dropout is not None:
        # 将p_attn传入dropout对象中进行'丢弃'处理
        p_attn = dropout(p_attn)

    # 最后, 根据公式将p_attn与value张量相乘获得最终的query注意力表示, 同时返回注意力张量
    return torch.matmul(p_attn, value), p_attn
```

- tensor.masked_fill演示:

```python
>>> input = Variable(torch.randn(5, 5))
>>> input 
Variable containing:
 2.0344 -0.5450  0.3365 -0.1888 -2.1803
 1.5221 -0.3823  0.8414  0.7836 -0.8481
-0.0345 -0.8643  0.6476 -0.2713  1.5645
 0.8788 -2.2142  0.4022  0.1997  0.1474
 2.9109  0.6006 -0.6745 -1.7262  0.6977
[torch.FloatTensor of size 5x5]

>>> mask = Variable(torch.zeros(5, 5))
>>> mask
Variable containing:
 0  0  0  0  0
 0  0  0  0  0
 0  0  0  0  0
 0  0  0  0  0
 0  0  0  0  0
[torch.FloatTensor of size 5x5]

>>> input.masked_fill(mask == 0, -1e9)
Variable containing:
-1.0000e+09 -1.0000e+09 -1.0000e+09 -1.0000e+09 -1.0000e+09
-1.0000e+09 -1.0000e+09 -1.0000e+09 -1.0000e+09 -1.0000e+09
-1.0000e+09 -1.0000e+09 -1.0000e+09 -1.0000e+09 -1.0000e+09
-1.0000e+09 -1.0000e+09 -1.0000e+09 -1.0000e+09 -1.0000e+09
-1.0000e+09 -1.0000e+09 -1.0000e+09 -1.0000e+09 -1.0000e+09
[torch.FloatTensor of size 5x5]
```

------

- 输入参数:

```python
# 我们令输入的query, key, value都相同, 位置编码的输出
query = key = value = pe_result
Variable containing:
( 0 ,.,.) = 
  46.5196  16.2057 -41.5581  ...  -16.0242 -17.8929 -43.0405
 -32.6040  16.1096 -29.5228  ...    4.2721  20.6034  -1.2747
 -18.6235  14.5076  -2.0105  ...   15.6462 -24.6081 -30.3391
   0.0000 -66.1486 -11.5123  ...   20.1519  -4.6823   0.4916

( 1 ,.,.) = 
 -24.8681   7.5495  -5.0765  ...   -7.5992 -26.6630  40.9517
  13.1581  -3.1918 -30.9001  ...   25.1187 -26.4621   2.9542
 -49.7690 -42.5019   8.0198  ...   -5.4809  25.9403 -27.4931
 -52.2775  10.4006   0.0000  ...   -1.9985   7.0106  -0.5189
[torch.FloatTensor of size 2x4x512]
```

------

- 调用:

```python
attn, p_attn = attention(query, key, value)
print("attn:", attn)
print("p_attn:", p_attn)
```

- 输出效果:

```python
# 将得到两个结果
# query的注意力表示:
attn: Variable containing:
( 0 ,.,.) = 
   12.8269    7.7403   41.2225  ...     1.4603   27.8559  -12.2600
   12.4904    0.0000   24.1575  ...     0.0000    2.5838   18.0647
  -32.5959   -4.6252  -29.1050  ...     0.0000  -22.6409  -11.8341
    8.9921  -33.0114   -0.7393  ...     4.7871   -5.7735    8.3374

( 1 ,.,.) = 
  -25.6705   -4.0860  -36.8226  ...    37.2346  -27.3576    2.5497
  -16.6674   73.9788  -33.3296  ...    28.5028   -5.5488  -13.7564
    0.0000  -29.9039   -3.0405  ...     0.0000   14.4408   14.8579
   30.7819    0.0000   21.3908  ...   -29.0746    0.0000   -5.8475
[torch.FloatTensor of size 2x4x512]

# 注意力张量:
p_attn: Variable containing:
(0 ,.,.) = 
  1  0  0  0
  0  1  0  0
  0  0  1  0
  0  0  0  1

(1 ,.,.) = 
  1  0  0  0
  0  1  0  0
  0  0  1  0
  0  0  0  1
[torch.FloatTensor of size 2x4x4]
```

- 带有mask的输入参数：

```python
query = key = value = pe_result

# 令mask为一个2x4x4的零张量
mask = Variable(torch.zeros(2, 4, 4))
```

------

- 调用:

```python
attn, p_attn = attention(query, key, value, mask=mask)
print("attn:", attn)
print("p_attn:", p_attn)
```

------

- 带有mask的输出效果:

```python
# query的注意力表示:
attn: Variable containing:
( 0 ,.,.) = 
   0.4284  -7.4741   8.8839  ...    1.5618   0.5063   0.5770
   0.4284  -7.4741   8.8839  ...    1.5618   0.5063   0.5770
   0.4284  -7.4741   8.8839  ...    1.5618   0.5063   0.5770
   0.4284  -7.4741   8.8839  ...    1.5618   0.5063   0.5770

( 1 ,.,.) = 
  -2.8890   9.9972 -12.9505  ...    9.1657  -4.6164  -0.5491
  -2.8890   9.9972 -12.9505  ...    9.1657  -4.6164  -0.5491
  -2.8890   9.9972 -12.9505  ...    9.1657  -4.6164  -0.5491
  -2.8890   9.9972 -12.9505  ...    9.1657  -4.6164  -0.5491
[torch.FloatTensor of size 2x4x512]

# 注意力张量:
p_attn: Variable containing:
(0 ,.,.) = 
  0.2500  0.2500  0.2500  0.2500
  0.2500  0.2500  0.2500  0.2500
  0.2500  0.2500  0.2500  0.2500
  0.2500  0.2500  0.2500  0.2500

(1 ,.,.) = 
  0.2500  0.2500  0.2500  0.2500
  0.2500  0.2500  0.2500  0.2500
  0.2500  0.2500  0.2500  0.2500
  0.2500  0.2500  0.2500  0.2500
[torch.FloatTensor of size 2x4x4]
```

`总结`：

- 学习了什么是注意力:
  - 我们观察事物时，之所以能够快速判断一种事物(当然允许判断是错误的), 是因为我们大脑能够很快把注意力放在事物最具有辨识度的部分从而作出判断，而并非是从头到尾的观察一遍事物后，才能有判断结果. 正是基于这样的理论，就产生了注意力机制.


------

- 什么是注意力计算规则:
  - 它需要三个指定的输入Q(query), K(key), V(value), 然后通过公式得到注意力的计算结果, 这个结果代表query在key和value作用下的表示. 而这个具体的计算规则有很多种, 我这里只介绍我们用到的这一种.


------

- 学习了`Q, K, V`的比喻解释:
  - Q是一段准备被概括的文本; K是给出的提示; V是大脑中的对提示K的延伸.
  - `当Q=K=V时`, 称作自注意力机制.


------

- 什么是注意力机制:
  - 注意力机制是注意力计算规则能够应用的深度学习网络的载体, 除了注意力计算规则外, 还包括一些必要的全连接层以及相关张量处理, 使其与应用网络融为一体. 使用自注意力计算规则的注意力机制称为自注意力机制.


------

- 学习并实现了注意力计算规则的函数: attention
  - 它的输入就是Q，K，V以及mask和dropout, mask用于掩码, dropout用于随机置0.
  - 它的输出有两个, query的注意力表示以及注意力张量.


### 2.3.3 多头注意力机制 P17 

- 学习目标:
  - 了解多头注意力机制的作用.
  - 掌握多头注意力机制的实现过程.


------

- 什么是多头注意力机制:
  - 从多头注意力的结构图中，貌似这个所谓的多个头就是指多组线性变换层，其实并不是，我只有使用了一组线性变化层，即`三个变换张量对Q，K，V分别进行线性变换`，这些变换`不会改变原有张量的尺寸`，因此每个变换矩阵都是`方阵`，得到输出结果后，多头的作用才开始显现，每个头开始从词义层面分割输出的张量，也就是每个头都想获得一组Q，K，V进行注意力机制的计算，但是句子中的每个词的表示只获得一部分，也就是只分割了最后一维的词嵌入向量. 这就是所谓的多头，将每个头的获得的输入送到注意力机制中, 就形成多头注意力机制.


------

- 多头注意力机制结构图:

  <img src="https://article.biliimg.com/bfs/article/af87236e673d1a082c9941b51678674b155712160.png" style="zoom:80%;" />



------

- 多头注意力机制的作用:
  - 这种结构设计能让每个注意力机制去优化每个词汇的不同特征部分，从而均衡同一种注意力机制可能产生的偏差，让词义拥有来自更多元的表达，实验表明可以从而提升模型效果.


------

- 多头注意力机制的代码实现:

```python
# 用于深度拷贝的copy工具包
import copy

# 首先需要定义克隆函数, 因为在多头注意力机制的实现中, 用到多个结构相同的线性层.
# 我们将使用clone函数将他们一同初始化在一个网络层列表对象中. 之后的结构中也会用到该函数.
def clones(module, N):
    """用于生成相同网络层的克隆函数, 它的参数module表示要克隆的目标网络层, N代表需要克隆的数量"""
    # 在函数中, 我们通过for循环对module进行N次深度拷贝, 使其每个module成为独立的层,
    # 然后将其放在nn.ModuleList类型的列表中存放.
    return nn.ModuleList([copy.deepcopy(module) for _ in range(N)])




# 我们使用一个类来实现多头注意力机制的处理
class MultiHeadedAttention(nn.Module):
    def __init__(self, head, embedding_dim, dropout=0.1):
        """在类的初始化时, 会传入三个参数，head代表头数，embedding_dim代表词嵌入的维度， 
           dropout代表进行dropout操作时置0比率，默认是0.1."""
        super(MultiHeadedAttention, self).__init__()

        # 在函数中，首先使用了一个测试中常用的assert语句，判断h是否能被d_model整除，
        # 这是因为我们之后要给每个头分配等量的词特征.也就是embedding_dim/head个.
        assert embedding_dim % head == 0

        # 得到每个头获得的分割词向量维度d_k
        self.d_k = embedding_dim // head

        # 传入头数h
        self.head = head

        # 然后获得线性层对象，通过nn的Linear实例化，它的内部变换矩阵是embedding_dim x embedding_dim，然后使用clones函数克隆四个，
        # 为什么是四个呢，这是因为在多头注意力中，Q，K，V各需要一个，最后拼接的矩阵还需要一个，因此一共是四个.
        self.linears = clones(nn.Linear(embedding_dim, embedding_dim), 4)

        # self.attn为None，它代表最后得到的注意力张量，现在还没有结果所以为None.
        self.attn = None

        # 最后就是一个self.dropout对象，它通过nn中的Dropout实例化而来，置0比率为传进来的参数dropout.
        self.dropout = nn.Dropout(p=dropout)

    def forward(self, query, key, value, mask=None):
        """前向逻辑函数, 它的输入参数有四个，前三个就是注意力机制需要的Q, K, V，
           最后一个是注意力机制中可能需要的mask掩码张量，默认是None. """

        # 如果存在掩码张量mask
        if mask is not None:
            # 使用unsqueeze拓展维度
            mask = mask.unsqueeze(0)

        # 接着，我们获得一个batch_size的变量，他是query尺寸的第1个数字，代表有多少条样本.
        batch_size = query.size(0)

        # 之后就进入多头处理环节
        # 首先利用zip将输入QKV与三个线性层组到一起，然后使用for循环，将输入QKV分别传到线性层中，
        # 做完线性变换后，开始为每个头分割输入，这里使用view方法对线性变换的结果进行维度重塑，多加了一个维度h，代表头数，
        # 这样就意味着每个头可以获得一部分词特征组成的句子，其中的-1代表自适应维度，
        # 计算机会根据这种变换自动计算这里的值.然后对第二维和第三维进行转置操作，
        # 为了让代表句子长度维度和词向量维度能够相邻，这样注意力机制才能找到词义与句子位置的关系，
        # 从attention函数中可以看到，利用的是原始输入的倒数第一和第二维.这样我们就得到了每个头的输入.
        query, key, value = \
           [model(x).view(batch_size, -1, self.head, self.d_k).transpose(1, 2)
            for model, x in zip(self.linears, (query, key, value))]

        # 得到每个头的输入后，接下来就是将他们传入到attention中，
        # 这里直接调用我们之前实现的attention函数.同时也将mask和dropout传入其中.
        x, self.attn = attention(query, key, value, mask=mask, dropout=self.dropout)

        # 通过多头注意力计算后，我们就得到了每个头计算结果组成的4维张量，我们需要将其转换为输入的形状以方便后续的计算，
        # 因此这里开始进行第一步处理环节的逆操作，先对第二和第三维进行转置，然后使用contiguous方法，
        # 这个方法的作用就是能够让转置后的张量应用view方法，否则将无法直接使用，
        # 所以，下一步就是使用view重塑形状，变成和输入形状相同.
        x = x.transpose(1, 2).contiguous().view(batch_size, -1, self.head * self.d_k)

        # 最后使用线性层列表中的最后一个线性层对输入进行线性变换得到最终的多头注意力结构的输出.
        return self.linears[-1](x)
```

- tensor.view演示:

```python
>>> x = torch.randn(4, 4)
>>> x.size()
torch.Size([4, 4])
>>> y = x.view(16)
>>> y.size()
torch.Size([16])
>>> z = x.view(-1, 8)  # the size -1 is inferred from other dimensions
>>> z.size()
torch.Size([2, 8])

>>> a = torch.randn(1, 2, 3, 4)
>>> a.size()
torch.Size([1, 2, 3, 4])
>>> b = a.transpose(1, 2)  # Swaps 2nd and 3rd dimension
>>> b.size()
torch.Size([1, 3, 2, 4])
>>> c = a.view(1, 3, 2, 4)  # Does not change tensor layout in memory
>>> c.size()
torch.Size([1, 3, 2, 4])
>>> torch.equal(b, c)
False
```

- torch.transpose演示:

```python
>>> x = torch.randn(2, 3)
>>> x
tensor([[ 1.0028, -0.9893,  0.5809],
        [-0.1669,  0.7299,  0.4942]])
>>> torch.transpose(x, 0, 1)
tensor([[ 1.0028, -0.1669],
        [-0.9893,  0.7299],
        [ 0.5809,  0.4942]])
```

------

- 实例化参数:

```python
# 头数head
head = 8

# 词嵌入维度embedding_dim
embedding_dim = 512

# 置零比率dropout
dropout = 0.2
```

------

- 输入参数:

```python
# 假设输入的Q，K，V仍然相等
query = value = key = pe_result

# 输入的掩码张量mask
mask = Variable(torch.zeros(8, 4, 4))
```

------

- 调用:

```python
mha = MultiHeadedAttention(head, embedding_dim, dropout)
mha_result = mha(query, key, value, mask)
print(mha_result)
```

- 输出效果:

```python
tensor([[[-0.3075,  1.5687, -2.5693,  ..., -1.1098,  0.0878, -3.3609],
         [ 3.8065, -2.4538, -0.3708,  ..., -1.5205, -1.1488, -1.3984],
         [ 2.4190,  0.5376, -2.8475,  ...,  1.4218, -0.4488, -0.2984],
         [ 2.9356,  0.3620, -3.8722,  ..., -0.7996,  0.1468,  1.0345]],

        [[ 1.1423,  0.6038,  0.0954,  ...,  2.2679, -5.7749,  1.4132],
         [ 2.4066, -0.2777,  2.8102,  ...,  0.1137, -3.9517, -2.9246],
         [ 5.8201,  1.1534, -1.9191,  ...,  0.1410, -7.6110,  1.0046],
         [ 3.1209,  1.0008, -0.5317,  ...,  2.8619, -6.3204, -1.3435]]],
       grad_fn=<AddBackward0>)
torch.Size([2, 4, 512])
```

------

`多头注意力机制总结`:P 20 -- 04:00

- 学习了什么是多头注意力机制:
  - 每个头开始从词义层面分割输出的张量，也就是每个头都想获得一组Q，K，V进行注意力机制的计算，但是句子中的每个词的表示只获得一部分，也就是只分割了最后一维的词嵌入向量. 这就是所谓的多头.将每个头的获得的输入送到注意力机制中, 就形成了多头注意力机制.


------

- 学习了多头注意力机制的作用:
  - 这种结构设计能让每个注意力机制去优化每个词汇的不同特征部分，从而均衡同一种注意力机制可能产生的偏差，让词义拥有来自更多元的表达，实验表明可以从而提升模型效果.


------

- 学习并实现了多头注意力机制的类: MultiHeadedAttention
  - 因为多头注意力机制中需要使用多个相同的线性层, 首先实现了克隆函数clones.
  - clones函数的输入是module，N，分别代表克隆的目标层，和克隆个数.
  - clones函数的输出是装有N个克隆层的Module列表.
  - 接着实现MultiHeadedAttention类, 它的初始化函数输入是h, d_model, dropout分别代表头数，词嵌入维度和置零比率.
  - 它的实例化对象输入是Q, K, V以及掩码张量mask.
  - 它的实例化对象输出是通过多头注意力机制处理的Q的注意力表示.

`P19`

```python
# 多头注意力机制的类
class MultiHeadedAttention(nn.Module):
    def __init__(self, head, embedding_dim, dropout=0.1):
        # head:代表几个头的参数
        # embedding_dim:代表词嵌入的维度
        # dropout:进行dropout操作时，置零的比率
        super(MultiHeadedAttention, self).__init__()

        # 要确认一个事实:多头的数量head需要整除嵌入词的维度embedding_dim
        assert embedding_dim % head == 0

        # 获得每个头获得的词向量的维度
        self.d_k = embedding_dim // head

        self.head = head
        self.embedding_dim = embedding_dim

        # 获得线形层，要获得4个，分别是Q,K,V以及最终的输出线形层
        self.linears = clones(nn.Linear(embedding_dim, embedding_dim), 4)

        # 初始化注意力张量
        self.attn = None

        # 初始化drouput对象
        self.dropout = nn.Dropout(p=dropout)

    def forward(self, query, key, value, mask=None):
        # query, key, value是注意力机制的三个输入张量，mask代表掩码张量
        # 首先判断是否使用掩码张量
        if mask is not None:
            # 使用unsqueeze将掩码张量进行维度扩充，代表多头中的第n个头
            mask = mask.unsqueeze(1)

        # 得到batch_size
        batch_size = query.size(0)
        # 首先使用zip将网络层和输入数据连接在一起，模型的输出利用view和transpose进行维度和形状的改变
        query, key, value = \
            [model(x).view(batch_size, -1, self.head, self.d_k).transpose(1, 2)
             for model, x in zip(self.linears, (query, key, value))]
        
        # 将每个头的输出传入到注意力层
        x, self.attn = attention(query, key, value, mask=mask, dropout=self.dropout)

        # 得到每个头的计算结果是4维张量，需要进行形状的转换
        # 前面已经将1，2两个维度进行过转置，在这里必须要重新转置回来，
        # 注意：经历了transpose()方法后，必须使用contiguous方法，否则无法使用view(）方法
        x = x.transpose(1, 2).contiguous().view(batch_size, -1, self.head * self.d_k)
        
        # 最后将x输入线形层列表中的最后一个线形层中进行处理，得到最终的多头注意力结构输出
        return self.linears[-1](x)
```

### 2.3.4 前馈全连接层

- 学习目标:
  - 了解什么是前馈全连接层及其它的作用.
  - 掌握前馈全连接层的实现过程.


------

- 什么是前馈全连接层:
  - 在Transformer中前馈全连接层就是具有两层线性层的全连接网络.


------

- 前馈全连接层的作用:
  - 考虑注意力机制可能对复杂过程的拟合程度不够, 通过增加两层网络来增强模型的能力.


------

- 前馈全连接层的代码分析:

```python
# 通过类PositionwiseFeedForward来实现前馈全连接层
class PositionwiseFeedForward(nn.Module):
    def __init__(self, d_model, d_ff, dropout=0.1):
        # d_model：代表词嵌入的维度，同时也是两个线性层的输入维度和输出维度
        # d_ff：代表第一个线性层的输出维度，和第二个线性层的输入维度
        # dropout：经过Dropout层处理时，随机置零的比率
        """初始化函数有三个输入参数分别是d_model, d_ff,和dropout=0.1，第一个是线性层的输入维度也是第二个线性层的输出维度，
           因为我们希望输入通过前馈全连接层后输入和输出的维度不变. 第二个参数d_ff就是第二个线性层的输入维度和第一个线性层的输出维度.
           最后一个是dropout置0比率."""
        super(PositionwiseFeedForward, self).__init__()

        # 首先按照我们预期使用nn实例化了两个线性层对象，self.w1和self.w2
        # 它们的参数分别是d_model, d_ff和d_ff, d_model
        self.w1 = nn.Linear(d_model, d_ff)
        self.w2 = nn.Linear(d_ff, d_model)
        # 然后使用nn的Dropout实例化了对象self.dropout
        self.dropout = nn.Dropout(dropout)

    def forward(self, x):
        """输入参数为x，代表来自上一层的输出"""
        # 首先经过第一个线性层，然后使用Funtional中relu函数进行激活,
        # 之后再使用dropout进行随机置0，最后通过第二个线性层w2，返回最终结果
        return self.w2(self.dropout(F.relu(self.w1(x))))

d_model = 512
d_ff = 64
dropout = 0.2

x = mha_result
ff = PositionwiseFeedForward(d_model, d_ff, dropout)
ff_result = ff(x)
print(ff_result)
print(ff_result.shape)
```

------

- ReLU函数公式: ReLU(x)=max(0, x)

------

- ReLU函数图像:

<img src="https://article.biliimg.com/bfs/article/7e3ca1eb7eb850ebfa19b2b4039ddd59155712160.png" style="zoom:80%;" />



- 实例化参数:

```python
d_model = 512

# 线性变化的维度
d_ff = 64

dropout = 0.2
```

------

- 输入参数:

```python
# 输入参数x可以是多头注意力机制的输出
x = mha_result
tensor([[[-0.3075,  1.5687, -2.5693,  ..., -1.1098,  0.0878, -3.3609],
         [ 3.8065, -2.4538, -0.3708,  ..., -1.5205, -1.1488, -1.3984],
         [ 2.4190,  0.5376, -2.8475,  ...,  1.4218, -0.4488, -0.2984],
         [ 2.9356,  0.3620, -3.8722,  ..., -0.7996,  0.1468,  1.0345]],

        [[ 1.1423,  0.6038,  0.0954,  ...,  2.2679, -5.7749,  1.4132],
         [ 2.4066, -0.2777,  2.8102,  ...,  0.1137, -3.9517, -2.9246],
         [ 5.8201,  1.1534, -1.9191,  ...,  0.1410, -7.6110,  1.0046],
         [ 3.1209,  1.0008, -0.5317,  ...,  2.8619, -6.3204, -1.3435]]],
       grad_fn=<AddBackward0>)
torch.Size([2, 4, 512])
```

------

- 调用:

```python
ff = PositionwiseFeedForward(d_model, d_ff, dropout)
ff_result = ff(x)
print(ff_result)
```

------

- 输出效果:

```python
tensor([[[-1.9488e+00, -3.4060e-01, -1.1216e+00,  ...,  1.8203e-01,
          -2.6336e+00,  2.0917e-03],
         [-2.5875e-02,  1.1523e-01, -9.5437e-01,  ..., -2.6257e-01,
          -5.7620e-01, -1.9225e-01],
         [-8.7508e-01,  1.0092e+00, -1.6515e+00,  ...,  3.4446e-02,
          -1.5933e+00, -3.1760e-01],
         [-2.7507e-01,  4.7225e-01, -2.0318e-01,  ...,  1.0530e+00,
          -3.7910e-01, -9.7730e-01]],

        [[-2.2575e+00, -2.0904e+00,  2.9427e+00,  ...,  9.6574e-01,
          -1.9754e+00,  1.2797e+00],
         [-1.5114e+00, -4.7963e-01,  1.2881e+00,  ..., -2.4882e-02,
          -1.5896e+00, -1.0350e+00],
         [ 1.7416e-01, -4.0688e-01,  1.9289e+00,  ..., -4.9754e-01,
          -1.6320e+00, -1.5217e+00],
         [-1.0874e-01, -3.3842e-01,  2.9379e-01,  ..., -5.1276e-01,
          -1.6150e+00, -1.1295e+00]]], grad_fn=<AddBackward0>)
torch.Size([2, 4, 512])
```

------

`前馈全连接层总结`:

- 学习了什么是前馈全连接层:
  - 在Transformer中前馈全连接层就是具有两层线性层的全连接网络.


------

- 学习了前馈全连接层的作用:
  - 考虑注意力机制可能对复杂过程的拟合程度不够, 通过增加两层网络来增强模型的能力.

------

- 学习并实现了前馈全连接层的类: PositionwiseFeedForward
  - 它的实例化参数为d_model, d_ff, dropout, 分别代表词嵌入维度, 线性变换维度, 和置零比率.
  - 它的输入参数x, 表示上层的输出.
  - 它的输出是经过2层线性网络变换的特征表示.

### 2.3.5 规范化层

- 学习目标:
  - 了解规范化层的作用.
  - 掌握规范化层的实现过程.


------

- 规范化层的作用:
  - 它是所有深层网络模型都需要的标准网络层，因为随着网络层数的增加，通过多层的计算后参数可能开始出现过大或过小的情况，这样可能会导致学习过程出现异常，模型可能收敛非常的慢. 因此都会在一定层数后接规范化层进行数值的规范化，使其特征数值在合理范围内.


------

- 规范化层的代码实现:

```python
 通过LayerNorm实现规范化层的类
class LayerNorm(nn.Module):
    def __init__(self, features, eps=1e-6):
        # features: 词嵌入的维度
        # eps： 一个足够小的正数，用来在规范化计算公式的分母中，放置除零操作
        """初始化函数有两个参数, 一个是features, 表示词嵌入的维度,
           另一个是eps它是一个足够小的数, 在规范化公式的分母中出现,
           防止分母为0.默认是1e-6."""
        super(LayerNorm, self).__init__()

        # 根据features的形状初始化两个参数张量a2，和b2，第一个初始化为1张量，
        # 也就是里面的元素都是1，第二个初始化为0张量，也就是里面的元素都是0，这两个张量就是规范化层的参数，
        # 因为直接对上一层得到的结果做规范化公式计算，将改变结果的正常表征，因此就需要有参数作为调节因子，
        # 使其即能满足规范化要求，又能不改变针对目标的表征.最后使用nn.parameter封装，代表他们是模型的参数。
        self.a2 = nn.Parameter(torch.ones(features))
        self.b2 = nn.Parameter(torch.zeros(features))

        # 把eps传到类中
        self.eps = eps

    def forward(self, x):
        # x：上一层网络的输出
        # 首先对x进行最后一个维度上的求均值操作，同时保持输出维度和输入维度一直
        """输入参数x代表来自上一层的输出"""
        # 在函数中，首先对输入变量x求其最后一个维度的均值，并保持输出维度与输入维度一致.
        # 接着再求最后一个维度的标准差，然后就是根据规范化公式，用x减去均值除以标准差获得规范化的结果，
        # 最后对结果乘以我们的缩放参数，即a2，*号代表同型点乘，即对应位置进行乘法操作，加上位移参数b2.返回即可.
        mean = x.mean(-1, keepdim=True)	# -1:在最后一个维度上
        # 按照规范化公式进行计算并返回
        std = x.std(-1, keepdim=True)
        return self.a2 * (x - mean) / (std + self.eps) + self.b2


features = d_model = 512
eps = 1e-6

x = ff_result
ln = LayerNorm(features, eps)
ln_result = ln(x)
print(ln_result)
print(ln_result.shape)
```

------

- 实例化参数:

```python
features = d_model = 512
eps = 1e-6
```

------

- 输入参数:

```python
# 输入x来自前馈全连接层的输出
x = ff_result
tensor([[[-1.9488e+00, -3.4060e-01, -1.1216e+00,  ...,  1.8203e-01,
          -2.6336e+00,  2.0917e-03],
         [-2.5875e-02,  1.1523e-01, -9.5437e-01,  ..., -2.6257e-01,
          -5.7620e-01, -1.9225e-01],
         [-8.7508e-01,  1.0092e+00, -1.6515e+00,  ...,  3.4446e-02,
          -1.5933e+00, -3.1760e-01],
         [-2.7507e-01,  4.7225e-01, -2.0318e-01,  ...,  1.0530e+00,
          -3.7910e-01, -9.7730e-01]],

        [[-2.2575e+00, -2.0904e+00,  2.9427e+00,  ...,  9.6574e-01,
          -1.9754e+00,  1.2797e+00],
         [-1.5114e+00, -4.7963e-01,  1.2881e+00,  ..., -2.4882e-02,
          -1.5896e+00, -1.0350e+00],
         [ 1.7416e-01, -4.0688e-01,  1.9289e+00,  ..., -4.9754e-01,
          -1.6320e+00, -1.5217e+00],
         [-1.0874e-01, -3.3842e-01,  2.9379e-01,  ..., -5.1276e-01,
          -1.6150e+00, -1.1295e+00]]], grad_fn=<AddBackward0>)
torch.Size([2, 4, 512])
```

------

- 调用:

```python
ln = LayerNorm(feature, eps)
ln_result = ln(x)
print(ln_result)
```

------

- 输出效果:

```python
tensor([[[ 2.2697,  1.3911, -0.4417,  ...,  0.9937,  0.6589, -1.1902],
         [ 1.5876,  0.5182,  0.6220,  ...,  0.9836,  0.0338, -1.3393],
         [ 1.8261,  2.0161,  0.2272,  ...,  0.3004,  0.5660, -0.9044],
         [ 1.5429,  1.3221, -0.2933,  ...,  0.0406,  1.0603,  1.4666]],

        [[ 0.2378,  0.9952,  1.2621,  ..., -0.4334, -1.1644,  1.2082],
         [-1.0209,  0.6435,  0.4235,  ..., -0.3448, -1.0560,  1.2347],
         [-0.8158,  0.7118,  0.4110,  ...,  0.0990, -1.4833,  1.9434],
         [ 0.9857,  2.3924,  0.3819,  ...,  0.0157, -1.6300,  1.2251]]],
       grad_fn=<AddBackward0>)
torch.Size([2, 4, 512])
```

------

`规范化层总结`:

- 学习了规范化层的作用:
  - 它是所有深层网络模型都需要的标准网络层，因为随着网络层数的增加，通过多层的计算后参数可能开始出现过大或过小的情况，这样可能会导致学习过程出现异常，模型可能收敛非常的慢. 因此都会在一定层数后接规范化层进行数值的规范化，使其特征数值在合理范围内.

------

- 学习并实现了规范化层的类: LayerNorm
  - 它的实例化参数有两个, features和eps，分别表示词嵌入特征大小，和一个足够小的数.
  - 它的输入参数x代表来自上一层的输出.
  - 它的输出就是经过规范化的特征表示.

### 2.3.6 子层连接结构

- 学习目标:
  - 了解什么是子层连接结构.
  - 掌握子层连接结构的实现过程.


------

- 什么是子层连接结构:
  - 如图所示，输入到每个子层以及规范化层的过程中，还使用了残差链接（跳跃连接），因此我们把这一部分结构整体叫做子层连接（代表子层及其链接结构），在每个编码器层中，都有两个子层，这两个子层加上周围的链接结构就形成了两个子层连接结构.


------

- 子层连接结构图:

  ![](https://article.biliimg.com/bfs/article/122092d91f732d6ea7ef61d100d3f1fc155712160.png)





------



![](https://article.biliimg.com/bfs/article/442c5ecb840fdeae191a0184e836f395155712160.png)

- 子层连接结构的代码分析:

```python
# 使用SublayerConnection来实现子层连接结构的类
class SublayerConnection(nn.Module):
    def __init__(self, size, dropout=0.1):
        """它输入参数有两个, size以及dropout， size一般是都是词嵌入维度的大小， 
           dropout本身是对模型结构中的节点数进行随机抑制的比率， 
           又因为节点被抑制等效就是该节点的输出都是0，因此也可以把dropout看作是对输出矩阵的随机置0的比率.
        """
        super(SublayerConnection, self).__init__()
        # 实例化了规范化对象self.norm
        self.norm = LayerNorm(size)
        # 又使用nn中预定义的droupout实例化一个self.dropout对象.
        self.dropout = nn.Dropout(p=dropout)

    def forward(self, x, sublayer):
        """前向逻辑函数中, 接收上一个层或者子层的输入作为第一个参数，
           将该子层连接中的子层函数作为第二个参数"""

        # 我们首先对输出进行规范化，然后将结果传给子层处理，之后再对子层进行dropout操作，
        # 随机停止一些网络中神经元的作用，来防止过拟合. 最后还有一个add操作， 
        # 因为存在跳跃连接，所以是将输入x与dropout后的子层输出结果相加作为最终的子层连接输出.
        return x + self.dropout(sublayer(self.norm(x)))
```

------

- 实例化参数

```python
size = 512
dropout = 0.2
head = 8
d_model = 512
###################################################
size = 512
dropout = 0.2
head = 8
d_model = 512
x = pe_result
mask = Variable(torch.zeros(2, 4, 4))
self_attn = MultiHeadedAttention(head, d_model)

sublayer = lambda x: self_attn(x, x, x, mask)

sc = SublayerConnection(size, dropout)
sc_result = sc(x, sublayer)
print(sc_result)
print(sc_result.shape)
```

- 输入参数:

```python
# 令x为位置编码器的输出
x = pe_result
mask = Variable(torch.zeros(8, 4, 4))

# 假设子层中装的是多头注意力层, 实例化这个类
self_attn =  MultiHeadedAttention(head, d_model)

# 使用lambda获得一个函数类型的子层
sublayer = lambda x: self_attn(x, x, x, mask)
```

------

- 调用:

```python
sc = SublayerConnection(size, dropout)
sc_result = sc(x, sublayer)
print(sc_result)
print(sc_result.shape)
```

- 输出效果:

```python
tensor([[[ 14.8830,  22.4106, -31.4739,  ...,  21.0882, -10.0338,  -0.2588],
         [-25.1435,   2.9246, -16.1235,  ...,  10.5069,  -7.1007,  -3.7396],
         [  0.1374,  32.6438,  12.3680,  ..., -12.0251, -40.5829,   2.2297],
         [-13.3123,  55.4689,   9.5420,  ..., -12.6622,  23.4496,  21.1531]],

        [[ 13.3533,  17.5674, -13.3354,  ...,  29.1366,  -6.4898,  35.8614],
         [-35.2286,  18.7378, -31.4337,  ...,  11.1726,  20.6372,  29.8689],
         [-30.7627,   0.0000, -57.0587,  ...,  15.0724, -10.7196, -18.6290],
         [ -2.7757, -19.6408,   0.0000,  ...,  12.7660,  21.6843, -35.4784]]],
       grad_fn=<AddBackward0>)
torch.Size([2, 4, 512])
```

------

`子层连接结构总结`:

- 什么是子层连接结构:
  - 如图所示，输入到每个子层以及规范化层的过程中，还使用了残差链接（跳跃连接），因此我们把这一部分结构整体叫做子层连接（代表子层及其链接结构）, 在每个编码器层中，都有两个子层，这两个子层加上周围的链接结构就形成了两个子层连接结构.

------

- 学习并实现了子层连接结构的类: SublayerConnection
  - 类的初始化函数输入参数是size, dropout, 分别代表`词嵌入大小`和`置零比率`.
  - 它的实例化对象输入参数是x, sublayer, 分别代表上一层输出以及子层的函数表示.
  - 它的输出就是通过子层连接结构处理的输出.

### 2.3.7 编码器层

- 学习目标:

  - 了解编码器层的作用.

  - 掌握编码器层的实现过程.


------

- 编码器层的作用:
  - 作为编码器的组成单元, 每个编码器层完成一次对输入的特征提取过程, 即编码过程.


------

- 编码器层的构成图:

<img src="https://article.biliimg.com/bfs/article/f46db8ec8cc3f5cc82fe1a014104a212155712160.png" style="zoom: 67%;" />

- 编码器层的代码分析:

```python
 使用EncoderLayer类实现编码器层 构建编码器层的类
class EncoderLayer(nn.Module):
    def __init__(self, size, self_attn, feed_forward, dropout):
        # size：代表词嵌入的维度
        # self_at tn：代表传入的多头自注意力子层的实例化对象
        # feed_forward：代表前馈全连接层实例化对象
        # dropout：进行dropout操作时的置零比率

        """它的初始化函数参数有四个，分别是size，其实就是我们词嵌入维度的大小，它也将作为我们编码器层的大小,
           第二个self_attn，之后我们将传入多头自注意力子层实例化对象, 并且是自注意力机制,
           第三个是feed_froward, 之后我们将传入前馈全连接层实例化对象, 最后一个是置0比率dropout."""
        super(EncoderLayer, self).__init__()

        # 首先将self_attn和feed_forward传入其中.
        # 将两个实例化对象和参数传入类中

        self.self_attn = self_attn
        self.feed_forward = feed_forward

        # 如图所示, 编码器层中有两个子层连接结构, 所以使用clones函数进行克隆操作
        self.sublayer = clones(SublayerConnection(size, dropout), 2)
        # 把size传入其中
        self.size = size

    def forward(self, x, mask):
        # X：代表上一层的传入张量
        # mask：代表掩码张量
        # 首先让经过第一个子层连接结构，内部包含多头自注意力机制子层
        # 再让张量经过第二个子层连接结构，其中包含前馈全连接网络

        # forward函数中有两个输入参数，x和mask，分别代表上一层的输出，和掩码张量mask.
        # 里面就是按照结构图左侧的流程. 首先通过第一个子层连接结构，其中包含多头自注意力子层，
        # 然后通过第二个子层连接结构，其中包含前馈全连接子层. 最后返回结果.
        x = self.sublayer[0](x, lambda x: self.self_attn(x, x, x, mask))
        return self.sublayer[1](x, self.feed_forward)
```

------

- 实例化参数:

```python

size = 512
head = 8
d_model = 512
d_ff = 64
x = pe_result
dropout = 0.2
self_attn = MultiHeadedAttention(head, d_model)
ff = PositionwiseFeedForward(d_model, d_ff, dropout)
mask = Variable(torch.zeros(8, 4, 4))
```

- 调用:

```python
el = EncoderLayer(size, self_attn, ff, dropout)
el_result = el(x, mask)
print(el_result)
print(el_result.shape)
```

------

- 输出效果:

```python
tensor([[[ 33.6988, -30.7224,  20.9575,  ...,   5.2968, -48.5658,  20.0734],
         [-18.1999,  34.2358,  40.3094,  ...,  10.1102,  58.3381,  58.4962],
         [ 32.1243,  16.7921,  -6.8024,  ...,  23.0022, -18.1463, -17.1263],
         [ -9.3475,  -3.3605, -55.3494,  ...,  43.6333,  -0.1900,   0.1625]],

        [[ 32.8937, -46.2808,   8.5047,  ...,  29.1837,  22.5962, -14.4349],
         [ 21.3379,  20.0657, -31.7256,  ..., -13.4079, -44.0706,  -9.9504],
         [ 19.7478,  -1.0848,  11.8884,  ...,  -9.5794,   0.0675,  -4.7123],
         [ -6.8023, -16.1176,  20.9476,  ...,  -6.5469,  34.8391, -14.9798]]],
       grad_fn=<AddBackward0>)
torch.Size([2, 4, 512])
```

------

`编码器层总结`：

- 学习了编码器层的作用:
  - 作为编码器的组成单元, 每个编码器层完成一次对输入的特征提取过程, 即编码过程.

------

- 学习并实现了编码器层的类: EncoderLayer
  - 类的初始化函数共有4个, 别是size，其实就是我们词嵌入维度的大小. 第二个self_attn，之后我们将传入多头自注意力子层实例化对象, 并且是自注意力机制. 第三个是feed_froward, 之后我们将传入前馈全连接层实例化对象. 最后一个是置0比率dropout.
    - 实例化对象的输入参数有2个，x代表来自上一层的输出, mask代表掩码张量.
    - 它的输出代表经过整个编码层的特征表示.

### 2.3.8 编码器

- 学习目标:
  - 了解编码器的作用.
  - 掌握编码器的实现过程.


------

- 编码器的作用:
  - 编码器用于对输入进行指定的特征提取过程, 也称为编码, 由N个编码器层堆叠而成.


------

- 编码器的结构图:

![img](https://pic1.zhimg.com/80/v2-306c89830ea9efe5953ae4d8b76492a4_1440w.webp)

- 编码器的代码分析:

```python
# 使用Encoder类来实现编码器
class Encoder(nn.Module):
    def __init__(self, layer, N):
        """初始化函数的两个参数分别代表编码器层和编码器层的个数"""
        super(Encoder, self).__init__()
        # 首先使用clones函数克隆N个编码器层放在self.layers中
        self.layers = clones(layer, N)
        # 再初始化一个规范化层, 它将用在编码器的最后面.
        self.norm = LayerNorm(layer.size)

    def forward(self, x, mask):
        """forward函数的输入和编码器层相同, x代表上一层的输出, mask代表掩码张量"""
        # 首先就是对我们克隆的编码器层进行循环，每次都会得到一个新的x，
        # 这个循环的过程，就相当于输出的x经过了N个编码器层的处理. 
        # 最后再通过规范化层的对象self.norm进行处理，最后返回结果. 
        for layer in self.layers:
            x = layer(x, mask)
        return self.norm(x)
```

- 实例化参数:

```python
# 第一个实例化参数layer, 它是一个编码器层的实例化对象, 因此需要传入编码器层的参数
# 又因为编码器层中的子层是不共享的, 因此需要使用深度拷贝各个对象.
size = 512
head = 8
d_model = 512
d_ff = 64
c = copy.deepcopy
attn = MultiHeadedAttention(head, d_model)
ff = PositionwiseFeedForward(d_model, d_ff, dropout)
dropout = 0.2
layer = EncoderLayer(size, c(attn), c(ff), dropout)

# 编码器中编码器层的个数N
N = 8
mask = Variable(torch.zeros(8, 4, 4))
```

------

- 调用:

```python
en = Encoder(layer, N)
en_result = en(x, mask)
print(en_result)
print(en_result.shape)
```

------

- 输出效果:

```python
tensor([[[-0.2081, -0.3586, -0.2353,  ...,  2.5646, -0.2851,  0.0238],
         [ 0.7957, -0.5481,  1.2443,  ...,  0.7927,  0.6404, -0.0484],
         [-0.1212,  0.4320, -0.5644,  ...,  1.3287, -0.0935, -0.6861],
         [-0.3937, -0.6150,  2.2394,  ..., -1.5354,  0.7981,  1.7907]],

        [[-2.3005,  0.3757,  1.0360,  ...,  1.4019,  0.6493, -0.1467],
         [ 0.5653,  0.1569,  0.4075,  ..., -0.3205,  1.4774, -0.5856],
         [-1.0555,  0.0061, -1.8165,  ..., -0.4339, -1.8780,  0.2467],
         [-2.1617, -1.5532, -1.4330,  ..., -0.9433, -0.5304, -1.7022]]],
       grad_fn=<AddBackward0>)
torch.Size([2, 4, 512])
```

------

**编码器总结：**

- 学习了编码器的作用:
  - 编码器用于对输入进行指定的特征提取过程, 也称为编码, 由N个编码器层堆叠而成.

------

- 学习并实现了编码器的类: Encoder
  - 类的初始化函数参数有两个，分别是layer和N，代表编码器层和编码器层的个数.
  - forward函数的输入参数也有两个, 和编码器层的forward相同, x代表上一层的输出, mask代码掩码张量.
  - 编码器类的输出就是Transformer中编码器的特征提取表示, 它将成为解码器的输入的一部分.

## 2.4 解码器部分实现

- 学习目标

  - 了解解码器中各个组成部分的作用.

  - 掌握解码器中各个组成部分的实现过程.


------

- 解码器部分:

  - 由N个解码器层堆叠而成
  - 每个解码器层由三个子层连接结构组成
  - 第一个子层连接结构包括一个多头自注意力子层和`规范化层以及一个残差连接`
  - 第二个子层连接结构包括一个多头注意力子层和规范化层以及一个残差连接
  - 第三个子层连接结构包括一个前馈全连接子层和规范化层以及一个残差连接

![img](https://pic1.zhimg.com/80/v2-4e17a521400c92b41a5927e5c40aeef0_1440w.webp)

说明:

- 解码器层中的各个部分，如，多头注意力机制，规范化层，前馈全连接网络，子层连接结构都与编码器中的实现相同. 因此这里可以直接拿来构建解码器层.

------

### 2.4.1 解码器层

- 学习目标:
  - 了解解码器的作用.
  - 掌握解码器的实现过程.


------

- 解码器的作用:
  - 作为解码器的组成单元, 每个解码器层根据给定的输入向目标方向进行特征提取操作，即解码过程.


------

- 解码器层的代码实现

```python
# 使用DecoderLayer的类实现解码器层
class DecoderLayer(nn.Module):
    def __init__(self, size, self_attn, src_attn, feed_forward, dropout):
        """初始化函数的参数有5个, 分别是size，代表词嵌入的维度大小, 同时也代表解码器层的尺寸，
            第二个是self_attn，多头自注意力对象，也就是说这个注意力机制需要Q=K=V， 
            第三个是src_attn，多头注意力对象，这里Q!=K=V， 第四个是前馈全连接层对象，最后就是droupout置0比率.
        """
        super(DecoderLayer, self).__init__()
        # 在初始化函数中， 主要就是将这些输入传到类中
        self.size = size
        self.self_attn = self_attn
        self.src_attn = src_attn
        self.feed_forward = feed_forward
        # 按照结构图使用clones函数克隆三个子层连接对象.
        self.sublayer = clones(SublayerConnection(size, dropout), 3)

    def forward(self, x, memory, source_mask, target_mask):
        """forward函数中的参数有4个，分别是来自上一层的输入x，
           来自编码器层的语义存储变量mermory， 以及源数据掩码张量和目标数据掩码张量.
        """
        # 将memory表示成m方便之后使用
        m = memory

        # 将x传入第一个子层结构，第一个子层结构的输入分别是x和self-attn函数，因为是自注意力机制，所以Q,K,V都是x，
        # 最后一个参数是目标数据掩码张量，这时要对目标数据进行遮掩，因为此时模型可能还没有生成任何目标数据，
        # 比如在解码器准备生成第一个字符或词汇时，我们其实已经传入了第一个字符以便计算损失，
        # 但是我们不希望在生成第一个字符时模型能利用这个信息，因此我们会将其遮掩，同样生成第二个字符或词汇时，
        # 模型只能使用第一个字符或词汇信息，第二个字符以及之后的信息都不允许被模型使用.
        x = self.sublayer[0](x, lambda x: self.self_attn(x, x, x, target_mask))

        # 接着进入第二个子层，这个子层中常规的注意力机制，q是输入x; k，v是编码层输出memory， 
        # 同样也传入source_mask，但是进行源数据遮掩的原因并非是抑制信息泄漏，而是遮蔽掉对结果没有意义的字符而产生的注意力值，
        # 以此提升模型效果和训练速度. 这样就完成了第二个子层的处理.
        x = self.sublayer[1](x, lambda x: self.src_attn(x, m, m, source_mask))

        # 最后一个子层就是前馈全连接子层，经过它的处理后就可以返回结果.这就是我们的解码器层结构.
        return self.sublayer[2](x, self.feed_forward)
```

- 实例化参数:

```python
# 类的实例化参数与解码器层类似, 相比多出了src_attn, 但是和self_attn是同一个类.
head = 8
size = 512
d_model = 512
d_ff = 64
dropout = 0.2
self_attn = src_attn = MultiHeadedAttention(head, d_model, dropout)

# 前馈全连接层也和之前相同 
ff = PositionwiseFeedForward(d_model, d_ff, dropout)
```

------

- 输入参数:

```python
# x是来自目标数据的词嵌入表示, 但形式和源数据的词嵌入表示相同, 这里使用per充当.
x = pe_result

# memory是来自编码器的输出
memory = en_result

# 实际中source_mask和target_mask并不相同, 这里为了方便计算使他们都为mask
mask = Variable(torch.zeros(8, 4, 4))
source_mask = target_mask = mask
```

- 调用:

```python
dl = DecoderLayer(size, self_attn, src_attn, ff, dropout)
dl_result = dl(x, memory, source_mask, target_mask)
print(dl_result)
print(dl_result.shape)
```

------

- 输出效果:

```python
tensor([[[ 1.9604e+00,  3.9288e+01, -5.2422e+01,  ...,  2.1041e-01,
          -5.5063e+01,  1.5233e-01],
         [ 1.0135e-01, -3.7779e-01,  6.5491e+01,  ...,  2.8062e+01,
          -3.7780e+01, -3.9577e+01],
         [ 1.9526e+01, -2.5741e+01,  2.6926e-01,  ..., -1.5316e+01,
           1.4543e+00,  2.7714e+00],
         [-2.1528e+01,  2.0141e+01,  2.1999e+01,  ...,  2.2099e+00,
          -1.7267e+01, -1.6687e+01]],

        [[ 6.7259e+00, -2.6918e+01,  1.1807e+01,  ..., -3.6453e+01,
          -2.9231e+01,  1.1288e+01],
         [ 7.7484e+01, -5.0572e-01, -1.3096e+01,  ...,  3.6302e-01,
           1.9907e+01, -1.2160e+00],
         [ 2.6703e+01,  4.4737e+01, -3.1590e+01,  ...,  4.1540e-03,
           5.2587e+00,  5.2382e+00],
         [ 4.7435e+01, -3.7599e-01,  5.0898e+01,  ...,  5.6361e+00,
           3.5891e+01,  1.5697e+01]]], grad_fn=<AddBackward0>)
torch.Size([2, 4, 512])
```

------

`解码器层总结`：

- 学习了解码器层的作用:
  - 作为解码器的组成单元, 每个解码器层根据给定的输入向目标方向进行特征提取操作，即解码过程.

------

- 学习并实现了解码器层的类: DecoderLayer
  - 类的初始化函数的参数有5个, 分别是size，代表词嵌入的维度大小, 同时也代表解码器层的尺寸，第二个是self_attn，多头自注意力对象，也就是说这个注意力机制需要Q=K=V，第三个是src_attn，多头注意力对象，这里Q!=K=V， 第四个是前馈全连接层对象，最后就是droupout置0比率.
  - forward函数的参数有4个，分别是来自上一层的输入x，来自编码器层的语义存储变量mermory， 以及源数据掩码张量和目标数据掩码张量.
  - 最终输出了由编码器输入和目标数据一同作用的特征提取结果.

### 2.4.2 解码器

- 学习目标:
  - 了解解码器的作用.
  - 掌握解码器的实现过程.


------

- 解码器的作用:
  - 根据编码器的结果以及上一次预测的结果, 对下一次可能出现的'值'进行特征表示.


------

- 解码器的代码分析:

```python
# 使用类Decoder来实现解码器
class Decoder(nn.Module):
    def __init__(self, layer, N):
        """初始化函数的参数有两个，第一个就是解码器层layer，第二个是解码器层的个数N."""
        super(Decoder, self).__init__()
        # 首先使用clones方法克隆了N个layer，然后实例化了一个规范化层. 
        # 因为数据走过了所有的解码器层后最后要做规范化处理. 
        self.layers = clones(layer, N)
        self.norm = LayerNorm(layer.size)

    def forward(self, x, memory, source_mask, target_mask):
        """forward函数中的参数有4个，x代表目标数据的嵌入表示，memory是编码器层的输出，
           source_mask, target_mask代表源数据和目标数据的掩码张量"""

        # 然后就是对每个层进行循环，当然这个循环就是变量x通过每一个层的处理，
        # 得出最后的结果，再进行一次规范化返回即可. 
        for layer in self.layers:
            x = layer(x, memory, source_mask, target_mask)
        return self.norm(x)
```

- 实例化参数:

```python
# 分别是解码器层layer和解码器层的个数N
size = 512
d_model = 512
head = 8
d_ff = 64
dropout = 0.2
c = copy.deepcopy
attn = MultiHeadedAttention(head, d_model)
ff = PositionwiseFeedForward(d_model, d_ff, dropout)
layer = DecoderLayer(d_model, c(attn), c(attn), c(ff), dropout)
N = 8
```

------

- 输入参数:

```python
# 输入参数与解码器层的输入参数相同
x = pe_result
memory = en_result
mask = Variable(torch.zeros(8, 4, 4))
source_mask = target_mask = mask
```

------

- 调用:

```python
de = Decoder(layer, N)
de_result = de(x, memory, source_mask, target_mask)
print(de_result)
print(de_result.shape)
```

------

- 输出效果:

```python
tensor([[[ 0.9898, -0.3216, -1.2439,  ...,  0.7427, -0.0717, -0.0814],
         [-0.7432,  0.6985,  1.5551,  ...,  0.5232, -0.5685,  1.3387],
         [ 0.2149,  0.5274, -1.6414,  ...,  0.7476,  0.5082, -3.0132],
         [ 0.4408,  0.9416,  0.4522,  ..., -0.1506,  1.5591, -0.6453]],

        [[-0.9027,  0.5874,  0.6981,  ...,  2.2899,  0.2933, -0.7508],
         [ 1.2246, -1.0856, -0.2497,  ..., -1.2377,  0.0847, -0.0221],
         [ 3.4012, -0.4181, -2.0968,  ..., -1.5427,  0.1090, -0.3882],
         [-0.1050, -0.5140, -0.6494,  ..., -0.4358, -1.2173,  0.4161]]],
       grad_fn=<AddBackward0>)
torch.Size([2, 4, 512])
```

------

**解码器总结：**

- 学习了解码器的作用:
  - 根据编码器的结果以及上一次预测的结果, 对下一次可能出现的'值'进行特征表示.

------

- 学习并实现了解码器的类: Decoder
  - 类的初始化函数的参数有两个，第一个就是解码器层layer，第二个是解码器层的个数N.
  - forward函数中的参数有4个，x代表目标数据的嵌入表示，memory是编码器层的输出，src_mask, tgt_mask代表源数据和目标数据的掩码张量.
  - 输出解码过程的最终特征表示.

## 2.5 输出部分实现

- 学习目标

  - 了解线性层和softmax的作用.

  - 掌握线性层和softmax的实现过程.


------

- 输出部分包含:
  - 线性层
  - softmax层


![img](https://pic3.zhimg.com/80/v2-4b2d21a7199c6f261c9caca82e213b96_1440w.webp)

- 线性层的作用
  - 通过对上一步的线性变化得到指定维度的输出, 也就是转换维度的作用.

------

-  softmax层的作用
  - 使最后一维的向量中的数字缩放到0-1的概率值域内, 并满足他们的和为1.

------

- 线性层和softmax层的代码分析:

```python
# nn.functional工具包装载了网络层中那些只进行计算, 而没有参数的层
import torch.nn.functional as F

# 将线性层和softmax计算层一起实现, 因为二者的共同目标是生成最后的结构
# 因此把类的名字叫做Generator, 生成器类
class Generator(nn.Module):
    def __init__(self, d_model, vocab_size):
        """初始化函数的输入参数有两个, d_model代表词嵌入维度, vocab_size代表词表大小."""
        super(Generator, self).__init__()
        # 首先就是使用nn中的预定义线性层进行实例化, 得到一个对象self.project等待使用, 
        # 这个线性层的参数有两个, 就是初始化函数传进来的两个参数: d_model, vocab_size
        self.project = nn.Linear(d_model, vocab_size)

    def forward(self, x):
        """前向逻辑函数中输入是上一层的输出张量x"""
        # 在函数中, 首先使用上一步得到的self.project对x进行线性变化, 
        # 然后使用F中已经实现的log_softmax进行的softmax处理.
        # 在这里之所以使用log_softmax是因为和我们这个pytorch版本的损失函数实现有关, 在其他版本中将修复.
        # log_softmax就是对softmax的结果又取了对数, 因为对数函数是单调递增函数, 
        # 因此对最终我们取最大的概率值没有影响. 最后返回结果即可.
        return F.log_softmax(self.project(x), dim=-1)
```

------

- nn.Linear演示:

```python
>>> m = nn.Linear(20, 30)
>>> input = torch.randn(128, 20)
>>> output = m(input)
>>> print(output.size())
torch.Size([128, 30])
```

------

- 实例化参数:

```python
# 词嵌入维度是512维
d_model = 512

# 词表大小是1000
vocab_size = 1000
```

------

- 输入参数:

```python
# 输入x是上一层网络的输出, 我们使用来自解码器层的输出
x = de_result
```

------

- 调用:

```python
gen = Generator(d_model, vocab_size)
gen_result = gen(x)
print(gen_result)
print(gen_result.shape)
```

------

- 输出效果:

```python
tensor([[[-7.8098, -7.5260, -6.9244,  ..., -7.6340, -6.9026, -7.5232],
         [-6.9093, -7.3295, -7.2972,  ..., -6.6221, -7.2268, -7.0772],
         [-7.0263, -7.2229, -7.8533,  ..., -6.7307, -6.9294, -7.3042],
         [-6.5045, -6.0504, -6.6241,  ..., -5.9063, -6.5361, -7.1484]],

        [[-7.1651, -6.0224, -7.4931,  ..., -7.9565, -8.0460, -6.6490],
         [-6.3779, -7.6133, -8.3572,  ..., -6.6565, -7.1867, -6.5112],
         [-6.4914, -6.9289, -6.2634,  ..., -6.2471, -7.5348, -6.8541],
         [-6.8651, -7.0460, -7.6239,  ..., -7.1411, -6.5496, -7.3749]]],
       grad_fn=<LogSoftmaxBackward>)
torch.Size([2, 4, 1000])
```

- 小节总结

  - 学习了输出部分包含:
    - 线性层
    - softmax层

  ------

  - 线性层的作用:
    - 通过对上一步的线性变化得到指定维度的输出, 也就是转换维度的作用.

  ------

  - softmax层的作用:

    - 使最后一维的向量中的数字缩放到0-1的概率值域内, 并满足他们的和为1.

  ------

  - 学习并实现了线性层和softmax层的类: Generator

    - 初始化函数的输入参数有两个, d_model代表词嵌入维度, vocab_size代表词表大小.
    - forward函数接受上一层的输出.
    - 最终获得经过线性层和softmax层处理的结果.

## 2.6 模型的构建

- 学习目标
  - 掌握编码器-解码器结构的实现过程.
  - 掌握Transformer模型的构建过程.

------

- 通过上面的小节, 我们已经完成了所有组成部分的实现, 接下来就来实现完整的编码器-解码器结构.

------

- Transformer总体架构图:

<img src="https://article.biliimg.com/bfs/article/e29cac3e97a731b009805f5fc7842ffa155712160.png" style="zoom:80%;" />

### 编码器-解码器结构的代码实现

```python
# 使用EncoderDecoder类来实现编码器-解码器结构
class EncoderDecoder(nn.Module):
    def __init__(self, encoder, decoder, source_embed, target_embed, generator):
        # encoder：代表编码器对象
        # decoder：代表解码器对象
        # source_embed：代表源数据的嵌入函数
        # target_embed：代表目标数据的嵌入函数
        # generator：代表输出部分类别生成器对象
        """初始化函数中有5个参数, 分别是编码器对象, 解码器对象, 
           源数据嵌入函数, 目标数据嵌入函数,  以及输出部分的类别生成器对象
        """
        super(EncoderDecoder, self).__init__()
        # 将参数传入到类中
        self.encoder = encoder
        self.decoder = decoder
        self.src_embed = source_embed
        self.tgt_embed = target_embed
        self.generator = generator

    def forward(self, source, target, source_mask, target_mask):
        # source：代表源数据
        # target：代表目标数据
        # source_mask：代表源数据的掩码张量
        # target_mask：代表目标数据的掩码张量
        """在forward函数中，有四个参数, source代表源数据, target代表目标数据, 
           source_mask和target_mask代表对应的掩码张量"""

        # 在函数中, 将source, source_mask传入编码函数, 得到结果后,
        # 与source_mask，target，和target_mask一同传给解码函数.
        return self.generator(self.decode(self.encode(source, source_mask), source_mask,
                            target, target_mask))

    def encode(self, source, source_mask):
        """编码函数, 以source和source_mask为参数"""
        # 使用src_embed对source做处理, 然后和source_mask一起传给self.encoder
        return self.encoder(self.src_embed(source), source_mask)

    def decode(self, memory, source_mask, target, target_mask):
        # memory：代表经历编码器编码后的输出张量
        """解码函数, 以memory即编码器的输出, source_mask, target, target_mask为参数"""
        # 使用tgt_embed对target做处理, 然后和source_mask, target_mask, memory一起传给self.decoder
        return self.decoder(self.tgt_embed(target), memory, source_mask, target_mask)
```

------

- 实例化参数

```python
vocab_size = 1000
d_model = 512
encoder = en
decoder = de
source_embed = nn.Embedding(vocab_size, d_model)
target_embed = nn.Embedding(vocab_size, d_model)
generator = gen
```

------

- 输入参数:

```python
# 假设源数据与目标数据相同, 实际中并不相同
source = target = Variable(torch.LongTensor([[100, 2, 421, 508], [491, 998, 1, 221]]))

# 假设src_mask与tgt_mask相同，实际中并不相同
source_mask = target_mask = Variable(torch.zeros(8, 4, 4))
```

------

- 调用:

```python
ed = EncoderDecoder(encoder, decoder, source_embed, target_embed, generator)
ed_result = ed(source, target, source_mask, target_mask)
print(ed_result)
print(ed_result.shape)
```

- 输出效果:

```python
tensor([[[ 0.2102, -0.0826, -0.0550,  ...,  1.5555,  1.3025, -0.6296],
         [ 0.8270, -0.5372, -0.9559,  ...,  0.3665,  0.4338, -0.7505],
         [ 0.4956, -0.5133, -0.9323,  ...,  1.0773,  1.1913, -0.6240],
         [ 0.5770, -0.6258, -0.4833,  ...,  0.1171,  1.0069, -1.9030]],

        [[-0.4355, -1.7115, -1.5685,  ..., -0.6941, -0.1878, -0.1137],
         [-0.8867, -1.2207, -1.4151,  ..., -0.9618,  0.1722, -0.9562],
         [-0.0946, -0.9012, -1.6388,  ..., -0.2604, -0.3357, -0.6436],
         [-1.1204, -1.4481, -1.5888,  ..., -0.8816, -0.6497,  0.0606]]],
       grad_fn=<AddBackward0>)
torch.Size([2, 4, 512])
```

------

- 接着将基于以上结构构建用于训练的模型.

------

- Tansformer模型构建过程的代码分析

```python
def make_model(source_vocab, target_vocab, N=6, 
               d_model=512, d_ff=2048, head=8, dropout=0.1):
    #source_voc ab：代表源数据的词汇总数
    #target_voc ab：代表目标数据的词汇总数
    #N：代表编码器和解码器堆叠的层数
    #d_model：代表词嵌入的维度
    #d_ff：代表前馈全连接层中变换矩阵的维度
    #head：多头注意力机制中的头数
    #dropout：指置零的比率

    """该函数用来构建模型, 有7个参数，分别是源数据特征(词汇)总数，目标数据特征(词汇)总数，
       编码器和解码器堆叠数，词向量映射维度，前馈全连接网络中变换矩阵的维度，
       多头注意力结构中的多头数，以及置零比率dropout."""

    # 首先得到一个深度拷贝命令，接下来很多结构都需要进行深度拷贝，
    # 来保证他们彼此之间相互独立，不受干扰.
    c = copy.deepcopy

    # 实例化了多头注意力类，得到对象attn
    attn = MultiHeadedAttention(head, d_model)

    # 然后实例化前馈全连接类，得到对象ff 
    ff = PositionwiseFeedForward(d_model, d_ff, dropout)

    # 实例化位置编码类，得到对象position
    position = PositionalEncoding(d_model, dropout)

    # 根据结构图, 最外层是EncoderDecoder，在EncoderDecoder中，
    # 分别是编码器层，解码器层，源数据Embedding层和位置编码组成的有序结构，
    # 目标数据Embedding层和位置编码组成的有序结构，以及类别生成器层. 
    # 在编码器层中有attention子层以及前馈全连接子层，
    # 在解码器层中有两个attention子层以及前馈全连接层.
    
    #实例化模型model，利用的是Encoder Decoder类
	#编码器的结构里面有2个子层，attention层和前馈全连接层
	#解码器的结构中有3个子层，两个attention层和前馈全连接层

    model = EncoderDecoder(
        Encoder(EncoderLayer(d_model, c(attn), c(ff), dropout), N),
        Decoder(DecoderLayer(d_model, c(attn), c(attn), 
                             c(ff), dropout), N),
        nn.Sequential(Embeddings(d_model, source_vocab), c(position)),
        nn.Sequential(Embeddings(d_model, target_vocab), c(position)),
        Generator(d_model, target_vocab))

    # 模型结构完成后，接下来就是初始化模型中的参数，比如线性层中的变换矩阵
    # 这里一但判断参数的维度大于1，则会将其初始化成一个服从均匀分布的矩阵，
    #初始化整个模型中的参数，判断参数的维度大于1，将矩阵初始化成一个服从均匀分布的矩阵

    for p in model.parameters():
        if p.dim() > 1:
            nn.init.xavier_uniform(p)
    return model
```

- nn.init.xavier_uniform演示:

```python
# 结果服从均匀分布U(-a, a)
>>> w = torch.empty(3, 5)
>>> w = nn.init.xavier_uniform_(w, gain=nn.init.calculate_gain('relu'))
>>> w
tensor([[-0.7742,  0.5413,  0.5478, -0.4806, -0.2555],
        [-0.8358,  0.4673,  0.3012,  0.3882, -0.6375],
        [ 0.4622, -0.0794,  0.1851,  0.8462, -0.3591]])
```

------

- 输入参数:

```python
source_vocab = 11
target_vocab = 11 
N = 6
# 其他参数都使用默认值 
```

------

- 调用:

```python
if __name__ == '__main__':
    res = make_model(source_vocab, target_vocab, N)
    print(res)
```

------

- 输出效果:

```python
# 根据Transformer结构图构建的最终模型结构
EncoderDecoder(
  (encoder): Encoder(
    (layers): ModuleList(
      (0): EncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linears): ModuleList(
            (0): Linear(in_features=512, out_features=512)
            (1): Linear(in_features=512, out_features=512)
            (2): Linear(in_features=512, out_features=512)
            (3): Linear(in_features=512, out_features=512)
          )
          (dropout): Dropout(p=0.1)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048)
          (w_2): Linear(in_features=2048, out_features=512)
          (dropout): Dropout(p=0.1)
        )
        (sublayer): ModuleList(
          (0): SublayerConnection(
            (norm): LayerNorm(
            )
            (dropout): Dropout(p=0.1)
          )
          (1): SublayerConnection(
            (norm): LayerNorm(
            )
            (dropout): Dropout(p=0.1)
          )
        )
      )
      (1): EncoderLayer(
        (self_attn): MultiHeadedAttention(
          (linears): ModuleList(
            (0): Linear(in_features=512, out_features=512)
            (1): Linear(in_features=512, out_features=512)
            (2): Linear(in_features=512, out_features=512)
            (3): Linear(in_features=512, out_features=512)
          )
          (dropout): Dropout(p=0.1)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048)
          (w_2): Linear(in_features=2048, out_features=512)
          (dropout): Dropout(p=0.1)
        )
        (sublayer): ModuleList(
          (0): SublayerConnection(
            (norm): LayerNorm(
            )
            (dropout): Dropout(p=0.1)
          )
          (1): SublayerConnection(
            (norm): LayerNorm(
            )
            (dropout): Dropout(p=0.1)
          )
        )
      )
    )
    (norm): LayerNorm(
    )
  )
  (decoder): Decoder(
    (layers): ModuleList(
      (0): DecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linears): ModuleList(
            (0): Linear(in_features=512, out_features=512)
            (1): Linear(in_features=512, out_features=512)
            (2): Linear(in_features=512, out_features=512)
            (3): Linear(in_features=512, out_features=512)
          )
          (dropout): Dropout(p=0.1)
        )
        (src_attn): MultiHeadedAttention(
          (linears): ModuleList(
            (0): Linear(in_features=512, out_features=512)
            (1): Linear(in_features=512, out_features=512)
            (2): Linear(in_features=512, out_features=512)
            (3): Linear(in_features=512, out_features=512)
          )
          (dropout): Dropout(p=0.1)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048)
          (w_2): Linear(in_features=2048, out_features=512)
          (dropout): Dropout(p=0.1)
        )
        (sublayer): ModuleList(
          (0): SublayerConnection(
            (norm): LayerNorm(
            )
            (dropout): Dropout(p=0.1)
          )
          (1): SublayerConnection(
            (norm): LayerNorm(
            )
            (dropout): Dropout(p=0.1)
          )
          (2): SublayerConnection(
            (norm): LayerNorm(
            )
            (dropout): Dropout(p=0.1)
          )
        )
      )
      (1): DecoderLayer(
        (self_attn): MultiHeadedAttention(
          (linears): ModuleList(
            (0): Linear(in_features=512, out_features=512)
            (1): Linear(in_features=512, out_features=512)
            (2): Linear(in_features=512, out_features=512)
            (3): Linear(in_features=512, out_features=512)
          )
          (dropout): Dropout(p=0.1)
        )
        (src_attn): MultiHeadedAttention(
          (linears): ModuleList(
            (0): Linear(in_features=512, out_features=512)
            (1): Linear(in_features=512, out_features=512)
            (2): Linear(in_features=512, out_features=512)
            (3): Linear(in_features=512, out_features=512)
          )
          (dropout): Dropout(p=0.1)
        )
        (feed_forward): PositionwiseFeedForward(
          (w_1): Linear(in_features=512, out_features=2048)
          (w_2): Linear(in_features=2048, out_features=512)
          (dropout): Dropout(p=0.1)
        )
        (sublayer): ModuleList(
          (0): SublayerConnection(
            (norm): LayerNorm(
            )
            (dropout): Dropout(p=0.1)
          )
          (1): SublayerConnection(
            (norm): LayerNorm(
            )
            (dropout): Dropout(p=0.1)
          )
          (2): SublayerConnection(
            (norm): LayerNorm(
            )
            (dropout): Dropout(p=0.1)
          )
        )
      )
    )
    (norm): LayerNorm(
    )
  )
  (src_embed): Sequential(
    (0): Embeddings(
      (lut): Embedding(11, 512)
    )
    (1): PositionalEncoding(
      (dropout): Dropout(p=0.1)
    )
  )
  (tgt_embed): Sequential(
    (0): Embeddings(
      (lut): Embedding(11, 512)
    )
    (1): PositionalEncoding(
      (dropout): Dropout(p=0.1)
    )
  )
  (generator): Generator(
    (proj): Linear(in_features=512, out_features=11)
  )
)
```

**小节总结**

- 学习并实现了编码器-解码器结构的类: EncoderDecoder
  - 类的初始化函数传入5个参数, 分别是编码器对象, 解码器对象, 源数据嵌入函数, 目标数据嵌入函数, 以及输出部分的类别生成器对象.
  - 类中共实现三个函数, forward, encode, decode
  - forward是主要逻辑函数, 有四个参数, source代表源数据, target代表目标数据, source_mask和target_mask代表对应的掩码张量.
  - encode是编码函数, 以source和source_mask为参数.
  - decode是解码函数, 以memory即编码器的输出, source_mask, target, target_mask为参数


------

- 学习并实现了模型构建函数: make_model
  - 有7个参数，分别是源数据特征(词汇)总数，目标数据特征(词汇)总数，编码器和解码器堆叠数，词向量映射维度，前馈全连接网络中变换矩阵的维度，多头注意力结构中的多头数，以及置零比率dropout.


## 2.7 模型基本测试运行 P44

- 学习目标

  - 了解Transformer模型基本测试的copy任务.

  - 掌握实现copy任务的四步曲.


------

- copy任务介绍:

  - 任务描述: 针对数字序列进行学习, 学习的最终目标是使输出与输入的序列相同. 如输入[1, 5, 8, 9, 3], 输出也是[1, 5, 8, 9, 3].
  - 任务意义: copy任务在模型基础测试中具有重要意义，因为copy操作对于模型来讲是一条明显规律, 因此模型能否在短时间内，小数据集中学会它，可以帮助我们断定模型所有过程是否正常，是否已具备基本学习能力.

------

- 使用copy任务进行模型基本测试的四步曲
  - 第一步: 构建数据集生成器
  - 第二步: 获得Transformer模型及其优化器和损失函数
  - 第三步: 运行模型进行训练和评估
  - 第四步: 使用模型进行贪婪解码

------

- 第一步: 构建数据集生成器

```python
# 导入工具包Batch, 它能够对原始样本数据生成对应批次的掩码张量
from pyitcast.transformer_utils import Batch  
from pyitcast.transformer_utils import get_std_opt
from pyitcast.transformer_utils import LabelSmoothing
from pyitcast.transformer_utils import SimpleLossCompute
from pyitcast.transformer_utils import run_epoch
from pyitcast.transformer_utils import greedy_decode


def data_generator(V, batch, num_batch):
    # V：随机生成数据的最大值+1
	# batch_size：每次输送给模型的样本数量，经历这些样本训练后进行一次参数的更新
	# num_batch：一共输送模型多少轮数据

    """该函数用于随机生成copy任务的数据, 它的三个输入参数是V: 随机生成数字的最大值+1, 
       batch: 每次输送给模型更新一次参数的数据量, num_batch: 一共输送num_batch次完成一轮
    """
    # 使用for循环遍历nbatches
    for i in range(num_batch):
        # 使用num py中的random.rand in t（）来随机生成[1，V)
		# 分布的形状(batch，10）

        # 在循环中使用np的random.randint方法随机生成[1, V)的整数, 
        # 分布在(batch, 10)形状的矩阵中, 然后再把numpy形式转换称torch中的tensor.
        data = torch.from_numpy(np.random.randint(1, V, size=(batch, 10)))

        # 接着使数据矩阵中的第一列数字都为1, 这一列也就成为了起始标志列, 
        # 当解码器进行第一次解码的时候, 会使用起始标志列作为输入.
        data[:, 0] = 1

        # 因为是copy任务, 所有source与target是完全相同的, 且数据样本作用变量不需要求梯度
        # 因此requires_grad设置为False
        source = Variable(data, requires_grad=False)
        target = Variable(data, requires_grad=False)

        # 使用Batch对source和target进行对应批次的掩码张量生成, 最后使用yield返回
        yield Batch(source, target)
```

- 输入参数:

```python
# 将生成0-10的整数
V = 11

# 每次喂给模型20个数据进行参数更新
batch = 20 

# 连续喂30次完成全部数据的遍历, 也就是1轮
num_batch = 30
```

------

- 调用:

```python
if __name__ == '__main__':
    res = data_generator(V, batch, num_batch)
    print(res)
```

------

- 输出效果:

```python
# 会得到一个数据生成器(生成器对象)
<generator object data_gen at 0x10c053e08>
```

------

- 第二步: 获得Transformer模型及其优化器和损失函数

```python
# 导入优化器工具包get_std_opt, 该工具用于获得标准的针对Transformer模型的优化器 
# 该标准优化器基于Adam优化器, 使其对序列到序列的任务更有效.
from pyitcast.transformer_utils import get_std_opt

# 导入标签平滑工具包, 该工具用于标签平滑, 标签平滑的作用就是小幅度的改变原有标签值的值域
# 因为在理论上即使是人工的标注数据也可能并非完全正确, 会受到一些外界因素的影响而产生一些微小的偏差
# 因此使用标签平滑来弥补这种偏差, 减少模型对某一条规律的绝对认知, 以防止过拟合. 通过下面示例了解更多.
from pyitcast.transformer_utils import LabelSmoothing

# 导入损失计算工具包, 该工具能够使用标签平滑后的结果进行损失的计算, 
# 损失的计算方法可以认为是交叉熵损失函数.
from pyitcast.transformer_utils import SimpleLossCompute

# 使用make_model获得model
model = make_model(V, V, N=2)

# 使用get_std_opt获得模型优化器
model_optimizer = get_std_opt(model)

# 使用LabelSmoothing获得标签平滑对象
criterion = LabelSmoothing(size=V, padding_idx=0, smoothing=0.0)

# 使用SimpleLossCompute获得利用标签平滑结果的损失计算方法
loss = SimpleLossCompute(model.generator, criterion, model_optimizer)
```

------

- 标签平滑示例:

```python
from pyitcast.transformer_utils import LabelSmoothing

# 使用LabelSmoothing实例化一个crit对象.
# 第一个参数size代表目标数据的词汇总数, 也是模型最后一层得到张量的最后一维大小
# 这里是5说明目标词汇总数是5个. 第二个参数padding_idx表示要将那些tensor中的数字
# 替换成0, 一般padding_idx=0表示不进行替换. 第三个参数smoothing, 表示标签的平滑程度
# 如原来标签的表示值为1, 则平滑后它的值域变为[1-smoothing, 1+smoothing].
crit = LabelSmoothing(size=5, padding_idx=0, smoothing=0.5)

# 假定一个任意的模型最后输出预测结果和真实结果
predict = Variable(torch.FloatTensor([[0, 0.2, 0.7, 0.1, 0],
                             [0, 0.2, 0.7, 0.1, 0], 
                             [0, 0.2, 0.7, 0.1, 0]]))

# 标签的表示值是0，1，2
target = Variable(torch.LongTensor([2, 1, 0]))

# 将predict, target传入到对象中
crit(predict, target)

# 绘制标签平滑图像
plt.imshow(crit.true_dist)
```

------

- 标签平滑图像:

![image-20231105223915947](https://cdn.jsdelivr.net/gh/beiyoudaxue/pic2023@main/img/202311052258109.png)

- 标签平滑图像分析:

  - 我们目光集中在`黄色小方块`上, 它相对于横坐标横跨的值域就是标签平滑后的正向平滑值域, 我们可以看到大致是从0.5到2.5.
  - 它相对于纵坐标横跨的值域就是标签平滑后的负向平滑值域, 我们可以看到大致是从-0.5到1.5, 总的值域空间由原来的[0, 2]变成了[-0.5, 2.5].

------

- 第三步: 运行模型进行训练和评估

```python
# 导入模型单轮训练工具包run_epoch, 该工具将对模型使用给定的损失函数计算方法进行单轮参数更新.
# 并打印每轮参数更新的损失结果.
from pyitcast.transformer_utils import run_epoch

def run(model, loss, epochs=10):
    """模型训练函数, 共有三个参数, model代表将要进行训练的模型
       loss代表使用的损失计算方法, epochs代表模型训练的轮数"""

    # 遍历轮数
    for epoch in range(epochs):
        # 模型使用训练模式, 所有参数将被更新
        model.train()
        # 训练时, batch_size是20
        run_epoch(data_generator(V, 8, 20), model, loss)

        # 模型使用评估模式, 参数将不会变化 
        model.eval()
        # 评估时, batch_size是5
        run_epoch(data_generator(V, 8, 5), model, loss)
```

------

- 输入参数:

```python
# 进行10轮训练
epochs = 10

# model和loss都是来自上一步的结果
```

------

- 输出效果:

```python
Epoch Step: 1 Loss: 3.315704 Tokens per Sec: 309.740843
Epoch Step: 1 Loss: 2.602743 Tokens per Sec: 393.885743
Epoch Step: 1 Loss: 2.563469 Tokens per Sec: 347.746994
Epoch Step: 1 Loss: 2.065951 Tokens per Sec: 422.632783
Epoch Step: 1 Loss: 2.218468 Tokens per Sec: 346.982987
Epoch Step: 1 Loss: 1.771149 Tokens per Sec: 396.451901
Epoch Step: 1 Loss: 1.979203 Tokens per Sec: 350.384045
Epoch Step: 1 Loss: 1.648887 Tokens per Sec: 361.534817
Epoch Step: 1 Loss: 1.824539 Tokens per Sec: 349.660287
Epoch Step: 1 Loss: 1.550169 Tokens per Sec: 319.302558
Epoch Step: 1 Loss: 1.676636 Tokens per Sec: 369.678638
Epoch Step: 1 Loss: 1.394759 Tokens per Sec: 364.660371
Epoch Step: 1 Loss: 1.473153 Tokens per Sec: 324.016068
Epoch Step: 1 Loss: 1.142609 Tokens per Sec: 422.345444
Epoch Step: 1 Loss: 1.410883 Tokens per Sec: 365.395922
Epoch Step: 1 Loss: 0.828656 Tokens per Sec: 401.538655
Epoch Step: 1 Loss: 1.254409 Tokens per Sec: 346.133228
Epoch Step: 1 Loss: 0.745532 Tokens per Sec: 402.395937
Epoch Step: 1 Loss: 0.952969 Tokens per Sec: 324.858870
Epoch Step: 1 Loss: 0.373509 Tokens per Sec: 358.814760
```

------

- 第四步: 使用模型进行贪婪解码

```python
# 导入贪婪解码工具包greedy_decode, 该工具将对最终结进行贪婪解码
# 贪婪解码的方式是每次预测都选择概率最大的结果作为输出, 
# 它不一定能获得全局最优性, 但却拥有最高的执行效率.
from pyitcast.transformer_utils import greedy_decode 


def run(model, loss, epochs=10):
    for epoch in range(epochs):
        # 首先进入训练模式，所有的参数将会被更新
        model.train()

        run_epoch(data_generator(V, 8, 20), model, loss)
		
        # 训练结束后， 进入评估模式，所有的参数固定不变
        model.eval()

        run_epoch(data_generator(V, 8, 5), model, loss)

    # 跳出for循环后，掉膘模型训练结束，进入评估模式
    # 模型进入测试模式
    model.eval()

    # 假定的输入张量
    # 初始化一个输入张量
    source = Variable(torch.LongTensor([[1,3,2,5,4,6,7,8,9,10]]))

    # 定义源数据掩码张量, 因为元素都是1, 在我们这里1代表不遮掩
    # 因此相当于对源数据没有任何遮掩.
    # 初始化一个输入张量的掩码张量，全1代表没有任何的遮掩
    source_mask = Variable(torch.ones(1, 1, 10))

    # 最后将model, src, src_mask, 解码的最大长度限制max_len, 默认为10
    # 以及起始标志数字, 默认为1, 我们这里使用的也是1
    #设定解码的最大长度max_len等于10，起始数字的标志默认等于1

    result = greedy_decode(model, source, source_mask, max_len=10, start_symbol=1)
    print(result)


if __name__ == '__main__':
    run(model, loss) 
```

------

- 输出效果:

```python
    1     3     2     5     4     6     7     8     9    10
[torch.LongTensor of size 1x10]
```

------

**小节总结**

- 学习了copy任务的相关知识:

  - 任务描述: 针对数字序列进行学习, 学习的最终目标是使输出与输入的序列相同. 如输入[1, 5, 8, 9, 3], 输出也是[1, 5, 8, 9, 3].
  - 任务意义: `copy任务`在模型基础测试中具有重要意义，因为copy操作对于模型来讲是一条明显规律, 因此模型能否在短时间内，小数据集中学会它，可以帮助我们断定模型所有过程是否正常，是否已具备基本学习能力.

------

- 学习了使用copy任务进行模型基本测试的四步曲:

  - 第一步: 构建数据集生成器
  - 第二步: 获得Transformer模型及其优化器和损失函数
  - 第三步: 运行模型进行训练和评估
  - 第四步: 使用模型进行贪婪解码

------

- 学习并实现了构建数据集生成器函数: data_gen

  - 它有三个输入参数, 分别是V: 随机生成数字的最大值+1, batch: 每次输送给模型更新一次参数的数据量, nbatches: 一共输送nbatches次完成一轮.
  - 该函数最终得到一个生成器对象.

------

- 学习了获得Transformer模型及其优化器和损失函数:

  - 通过导入优化器工具包get_std_opt, 获得标准优化器.
  - 通过导入标签平滑工具包LabelSmoothing, 进行标签平滑.
  - 通过导入损失计算工具包SimpleLossCompute, 计算损失.

------

- 学习并实现了运行模型进行训练和评估函数: run

  - 在函数中导入模型单轮训练工具包run_epoch, 对模型进行单轮训练.
  - 函数共有三个参数, model代表将要进行训练的模型, slc代表使用的损失计算方法, epochs代表模型训练的轮数.
  - 函数最终打印了模型训练和评估两个过程的损失.

------

- 学习并实现了使用模型进行贪婪解码:

  - 通过导入贪婪解码工具包greedy_decode, 根据输入得到最后输出, 完成了copy任务.

