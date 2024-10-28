# Definitions

## AC DC
**AC 般是指交流电220~250V之间的电源的进入电压，一般只用做家用电器的进入线，还有工业生产常用的380V（伏特）DC是指直流电源**，一般常用的有3 0V，6 . 0V，9 0V，12V等几个常见电压

HVDC (High Voltage Direct Current), 高压直流输电

cross linked polyethylene (XLPE) cable, _交联聚乙烯绝缘耐火电力电缆_


## partial discharge (Teilentladung)
The standard definition of *partial discharge* (PD) is an electrical discharge that does not completely bridge the space between two conducting electrodes. 

Partial discharge occurs in a variety of locations and mediums in high voltage electrical equipment.

在电气工程中，*局部放电*是在高压应力下固体或流体电绝缘系统的一小部分的局部介电击穿。虽然电晕放电通常是通过空气中相对稳定的辉光放电或刷子放电来显示的，但固体绝缘系统中的局部放电是不可见的。PD可能发生在气态，液态或固态绝缘介质中。它通常始于气体空隙，例如固体环氧绝缘材料中的空隙或变压器油中的气泡

The accumulation of **space charge** inside the *polymer* leads to local electric field *distortion*, which may result in partial discharge (PD), especially in insulation defects.
*聚合物*内部**空间电**荷的积累会导致局部电场*畸变*，从而可能导致局部放电（PD），尤其是在绝缘缺陷处。


#  #paper Pattern Recognition of DC Partial Discharge on XLPE Cable Based on ADAM-DBN
PD analysis methods can be divided into *phase resolved partial discharge (PRPD)* mode and *time resolved partial discharge (TRPD)* mode
局部放电（PD）分析方法可以分为相位分辨局部放电（PRPD）模式和时间分辨局部放电（TRPD）模式。
--> 这是高压输电行业中常见的局部放电检测技术，帮助识别电气设备中的绝缘故障。

Because the PD signal under DC has no *[[phase information]]*, the time interval between two *adjacent* discharge ∆t is usually used as an important characteristic parameter.
由于直流下的局部放电（PD）信号没有相位信息，通常使用两个*相邻*放电之间的时间间隔 ∆t 作为一个重要的特征参数。
--> 这解释了在**直流**条件下如何处理局部放电信号，由于缺乏相位信息，时间间隔成为一个关键的分析参数。




## adaptive moment estimation (ADAM) algorithm
**Adaptive Moment Estimation (ADAM) 算法** 的中文翻译为 **自适应矩估计算法**。

ADAM 是一种常用于训练深度学习模型的优化算法，结合了 **动量法** 和 **RMSProp** 两者的优点。它通过自适应地调整每个参数的学习率，并使用梯度的一阶和二阶矩估计来更新参数，从而使得训练过程更加稳定且收敛速度较快。

这个算法在处理稀疏梯度问题时表现优异，尤其适合大型数据集或高维度问题中的神经网络训练。


## deep belief network (DBN)
### 组成, 结构
The deep belief network is a non-convolution generation model proposed by Hinton et al. in 2006 which solves the problem that the depth model was difficult to optimize.

#### RBM
The deep belief network consists of a multi-layered *restricted Boltzmann machine (RBM).* It uses the contrastive divergence (CD) algorithm for *unsupervised* training of RBM and then uses *supervised* training for tuning of the entire DBN network.
深度信念网络（DBN）由多层受限玻尔兹曼机（RBM）组成。它使用对比散度（CD）算法对 RBM 进行无监督训练，然后使用有监督训练对整个 DBN 网络进行调优。
--> 这里提到的 **受限玻尔兹曼机（RBM）** 是 DBN 的构建单元，**对比散度（CD）算法** 是用于加速 RBM 训练的无监督学习方法。而之后的有监督训练阶段则用于对整个网络进行细调，以提高模型的最终性能。

> 正如名字所提示的那样，受限玻兹曼机是一种[玻兹曼机](https://zh.wikipedia.org/wiki/%E7%8E%BB%E5%B0%94%E5%85%B9%E6%9B%BC%E6%9C%BA "玻尔兹曼机")的变体，但限定模型必须为[二分图](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E5%9B%BE "二分图")。模型中包含对应输入参数的输入（可见）单元和对应训练结果的隐单元，图中的每条边必须连接一个可见单元和一个隐单元。（与此相对，“无限制”玻兹曼机包含隐单元间的边，使之成为[循环神经网络](https://zh.wikipedia.org/wiki/%E5%BE%AA%E7%8E%AF%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C "循环神经网络")。）这一限定使得相比一般玻兹曼机更高效的训练算法成为可能，特别是基于[梯度](https://zh.wikipedia.org/wiki/%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D%E6%B3%95 "梯度下降法")的对比分歧（contrastive divergence）算法[[


注意该模型可用于推荐系统和模式识别(例如手写数字)
![[Pasted image 20241021150823.png]]
Edges 上有权重
Phase 1.:
visiable能够看到训练数据, 并将input乘以权重再加上偏置, 然后传给隐藏单元 --> Feed forward pass

Phase 2.:
反向传播, 决定权重如何被调整



![[Pasted image 20241021151702.png]]

The state of the hidden elements in RBM is *independent* of each other, and when given the visible unit v, the ***probability that the hidden unit h is activated*** (set to 1) is:
![[Pasted image 20241021153712.png]]

Similarly, when the state of *hidden unit h is determined*, the probability that the visible unit v is activated is: 
![[Pasted image 20241021153801.png]]
**注意**: 这里使用 sigmoid 函数作为激活函数, 将自变量 x 映射到 (0, 1)

For the RBM model given the number of explicit elements and hidden elements, it is necessary to determine the parameter θ through training, where the training goal is to make the data reconstructed from the RBM model under the control of the parameter θ as consistent as possible with the given training sample data.
--> θ 包含了权重和两个偏置项

Because the fractionation function of RBM, Zθ, is difficult to calculate by simple method, this paper uses the comparative dispersion (CD) algorithm proposed by Hinton in 2002 to carry out rapid unsupervised training of RBM to solve the optimal value of the θ

![[Pasted image 20241021154541.png]]


### 整体网络
The *classification model* based on the DBN is stacked with *several RBMs* and consists of an input layer, several hidden layers and an output layer consisting of the Softmax classifier.
![[Pasted image 20241021154816.png]]

#### Pre-training --> unsupervised
![[Pasted image 20241021155255.png]]

#### Supervised Fine-Tuning Based on ADAM
预训练的最后阶段, 模型的参数需要被微调。
![[Pasted image 20241021155634.png]]

![[Pasted image 20241021155837.png]]

### 应用 - Cable PD Pattern Recognition Based on ADAM-DBN
Compared with naive Bayes (NB), K-nearest neighbor (KNN), support vector machine (SVM), and back propagation neural networks (BPNN), the ADAM-DBN method has higher accuracy on four different defect types due to the excellent ability in terms of the feature extraction of PD pulse waveforms.

The deep belief network (*DBN*) is a deep learning model with excellent feature learning ability, outstanding performance in data degradation and feature recognition, which is widely used in image processing, speech recognition. 
--> 用于特征提取
--> the deep learning method has strong characteristic learning ability based on the original data


a modified DBN algorithm based on DC PD pulse waveforms is proposed to achieve the pattern recognition of *DC cable insulation defects*.
基于直流局部放电脉冲波形的改进型深度信念网络（DBN）算法被提出，用于实现*直流电缆绝缘缺陷*的模式识别。
--> 此处的 **DBN（深度信念网络）** 是一种深度学习算法，而模式识别是用于检测和分类绝缘缺陷的过程。
 
- First, the *PD signals* of typical insulation defect cables are collected through the DC experimental platform. 
- Second, the PD pulse waveform is pre-processed using the *Canny* algorithm and used as an input sample for the classification model. 
- Third, a DBN recognition model optimized by the adaptive moment estimation (ADAM) algorithm is built to achieve the pattern recognition of different defect types. 
- Finally, compared with the artificial feature recognition methods, the effect of classification methods on various defects and the effect of training sample capacity on the classification models are analyzed.



论文设计了四种常见的XLPE电缆绝缘故障模型：

1. **导体毛刺(Conductor burrs) (缺陷C1)**：一个长度为1.5毫米的金属针附着在XLPE绝缘外表面，一端接触电缆铜芯，另一端悬挂在XLPE绝缘内部。
2. **外部半导电层残留物(external semi- conductive layer residue) (缺陷C2)**：在剥离半导电层的过程中，主绝缘表面上残留宽3毫米、长30毫米的半导电层。
3. **内部空气隙(internal air gap) (缺陷C3)**：在XLPE电缆绝缘界面上制造一些微孔，使*少量空气进入绝缘层内部*，然后用环氧树脂密封孔及其周围。
4. **绝缘表面的划痕(scratch on the insulation surface) (缺陷C4)**：沿着XLPE电缆绝缘表面的轴向做出宽1毫米、深1毫米的划痕。
![[Pasted image 20241021160741.png]]
#### Canny edge detection
Canny边缘检测具有强抗噪干扰和易于检测弱边缘的优点。使用Canny算法提取波形的有效信息的步骤如下：
1. 使用高斯滤波器对波形进行平滑处理。
2. 对波形求导，进行非最大值抑制，并仅保留导数的最大值点。
3. 对于双阈值检测，如果导数值低于低阈值，则抑制该点；如果导数值高于高阈值，则标记为强边缘点，否则标记为弱边缘点。
4. 抑制孤立的弱边缘点以及没有强边缘点邻近的弱边缘点


After determining the starting point of the *discharge waveform*, the discharge waveform is intercepted according to the length of the waveform and the sample rate, which is set to 600 in this article. Due to the different stable discharge voltages of different defects, the amplitude is normalized after intercepting the waveform.

![[Pasted image 20241021161719.png]]


### Steps
The PD pattern recognition step of DC cable based on the ADAM-DBN are shown as follows:

1. (1)  The original data are pre-processed and divided proportionally into training sets and sample sets.
    
2. (2)  Construct the DBN recognition model, pre-train it with CD algorithm, and get the pre-trained network parameters of the identification model.
    
3. (3)  Using the ADAM algorithm, the DBN model is supervised trained by training sample label, fine-tuning the network parameters to make the model optimized.
    
4. (4)  Use the test data set as input to inspect the trained DBN model.

## Evaluation
### 实验评估指标

准确率和召回率用于衡量各种诊断绝缘缺陷方法的有效性。

在多类别问题中，准确率表示***所有样本***中正确预测的样本所占的比例：

$$
a = \frac{{card\left( \sum X_i \right)}}{{card\left( \sum C_i \right)}}
$$
(公式13)

召回率表示*某种实际类型*的样本中被正确识别出的比例：

$$
r = \frac{{card(X_i)}}{{card(C_i)}}
$$
(公式14)

其中，$X_i$ 代表实际类型和识别类型都为 $i$ 的集合，$C_i$ 是实际类型为 $i$ 的集合。

Through the analysis of accuracy and recall rate, we can not only evaluate the overall effectiveness of the pattern recognition method, but also examine the specific identification effect of the pattern recognition method for each defect, and analyze the application of the algorithm to different defects.

### Structure and Parameter Settings
The initial bias of parameters in the DBN model are set to 0, and the initial weight uses the random number generated by the Gaussian distribution, where the expectation of Gaussian distribution is set to 0, the standard deviation is set to the inverse of the mean square root value of the number of cells in the visual layer, the batch size of the pre-training stage is 100, the RBM learning rate is 0.1, and the learning cycle of the fine-tuning stage is preset 200. Because the hidden layer structure and learning cycle have a great influence on the recognition accuracy, this paper determines the specific value through experiments.
在DBN模型中，参数的初始偏置设为0，初始权重使用由高斯分布生成的随机数，高斯分布的期望设为0，标准差设为可视层单元数均方根值的倒数。预训练阶段的批次大小为100，RBM的学习率为0.1，微调阶段的学习周期预设为200。由于隐藏层结构和学习周期对识别精度有很大影响，本文通过实验确定了具体数值。

这段描述了DBN模型训练的初始化设置及其对识别性能的影响，尤其是隐藏层结构和学习周期的实验优化过程。

The number of hidden layers of the model and the number of hidden units per hidden layer are obtained by the enumeration method. Thereby, first, a hidden layer is set for the model, the number of hidden units is gradually increased, the average accuracy of 10 experiments is recorded as a performance indicator, then the optimal value of the number of hidden units is determined. Moreover, add one more hidden layer and choose the optimal number of hidden units of second hidden layer, until the validation score is no longer improved.
--> 如此设置模型结构参数

![[Pasted image 20241021164024.png]]

![[Pasted image 20241021164130.png]]





