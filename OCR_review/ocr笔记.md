# 研究主题：OCR技术

​		==OCR==：光学字符识别（Optical Character Recognition）,指对文本资料的图像文件进行分析识别处理，获取文字及版面信息的过程。亦即将图像中的文字进行识别，并以文本的形式返回。

​		应用场景：证件识别、车牌识别

## 传统方法：

​		使用opencv算法库，通过图像处理和统计机器学习方法从图像中提取文本信息，包括二值化、噪声滤波、相关域分析、AdaBoost等。三个阶段：图像准备、文本识别、后处理。

​		针对简单场景下的图片，传统OCR已经取得了很好的效果。传统方法是针对特定场景下的图像进行建模，一旦跳出当前场景，模型就会失效。（近些年：基于深度学习的OCR技术）

一、图像准备预处理

- 文字区域定位：连通区域分析、MSER
- 文字矫正：旋转、仿射变换
- 文字分割：二值化、过滤噪声

传统方法采用==HoG==对图像进行特征提取；==缺点==：对于图像模糊、扭曲等问题鲁棒性很差，对于复杂场景泛化能力不佳。

基于==CNN的神经网络==进行特征提取；==优点==：基于CNN强大的学习能力，配合大量的数据可以增强特征提取的鲁棒性，面临模糊、扭曲、畸变、复杂背景和光线不清等图像问题均可以表现良好的鲁棒性。

预处理阶段的质量直接决定了最终的识别效果

首先文本定位，接着进行倾斜文本矫正，分割出单字后，使用人工特征HOG或者CNN特征，结合分类模型对单字进行识别，最后基于统计语言模型（如隐马尔科夫链，HMM）或者规则进行语义纠错

二、文字识别

- 分类器识别：逻辑回归、SVM、Adaboost

三、后处理

- 规则、语言模型（HMM等）

## 基于深度学习的OCR技术：

一、文字检测

​		检测图片中的文本区域，定位精度直接影响后续Recognition结果。==定位：6.FOTS基于统一网络的快速文本定位==

CTPN

Deeptext

​		目前文字检测方法：EAST/CTPN/SegLink/TextBoxes/TextBoxes++/TextSnake/MSR/Faster R-CNN/RRPN

**[EAST: An Efficient and Accurate Scene Text Detector](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1704.03155.pdf)**

TextBoxes:基于SSD改进的一个算法，调整了锚定框的长宽比，以适应文字的长宽比。==9==

TextBoxes++:==8==

EAST:==5==

CTPN：目前应用最广的文本检测模型之一。其基本假设是单个字符相较于异质化程度更高的文本行更容易被检测，因此先对单个字符进行类似R-CNN的检测。之后又在检测网络中加入了双向LSTM，使检测结果形成序列提供了文本的上下文特征，便可以将多个字符进行合并得到文本行。==10==

SegLink:是在SSD的启发下得出的，采用临近连接的方法对上下文进行连接。并且通过将连接参数的学习整合进了神经网络的学习过程，使得模型更容易训练。==文本检测7==

二、文字识别==1==

​		通过文字检测对图片中的文字进行定位后，再对该区域内的文字进行识别。

​		传统方法通过对单字符识别以实现对全文的识别：

1. 将文字行进行字符切分，得到单个字符；需要对候选字符进行过分割，使其足够破碎，之后再通过动态规划合并分割碎片，得到最优组合。

2. 通过滑动窗口对每一个可能的字符进行匹配，这种方法的准确率依赖于滑动窗口的滑动窗尺寸，尺寸过大会造成信息丢失，过小则会使计算力需求大幅增加。

深度学习的角度：引入上下文这样的序列信息，eg:RNN、LSTM等依赖于时序关系的神经网络。





关键词：OCR、

1、Accurate, data-efficient, unconstrained text recognition with convolutional neural networks

2、Geometric rectification of document images using adversarial gated unwarping network

3、[Optical character recognition by open source OCR tool tesseract: A case study](https://www.researchgate.net/profile/Chirag_Patel27/publication/235956427_Optical_Character_Recognition_by_Open_source_OCR_Tool_Tesseract_A_Case_Study/links/00463516fa43a64739000000.pdf)



## 笔记：

==**1、Gradient-based learning applied to document recognition**==(基于梯度的学习用于文本识别)

在合适的网络结构下，基于梯度的学习算法可以用来合成一个复杂的决策面，该决策面可以用最少的预处理对手写字符等高维模式进行分类。

**内容提要：**

1. 各种用于手写体字符识别的方法

2. 在一个标准的手写体数字识别任务中进行比较：卷积神经网络是专门设计用来处理二维形状变化的网络，其性能优于其他任何网络技术。

3. GTN：graphtransformer network

4. 两个在线手写识别系统
5. 实验读取银行支票，使用卷积神经网络字符识别器与全局训练技术结合

==**2、Faster R-CNN: Towards Real-Time ObjectDetection with Region Proposal Networks**==（面向区域方案网络的实时目标监测）

**内容提要：**

1. 最新的目标检测网络依赖于区域建议算法来假设目标位置，

2. 引入了一个区域建议网络（RPN），与检测网络共享完整的图像卷积特征，从而实现几乎无成本的区域建议；RPN是一个完全卷积的网络，它同时预测每个位置的目标边界和目标得分；RPN经过端到端训练，能够生成高质量的区域建议，用于Faster R-CNN用于检测。

==**3、Feature Pyramid Networks for Object Detection**==（用于目标检测的特征金字塔网络）

**内容提要：**

1. 特征金字塔（FPN）是识别系统中用于检测不同尺度目标的基本组成部分；
2. 特征金字塔具有计算性和记忆性，因此最近的深度学习对象检测器避免了使用特征金字塔（部分原因）；
3. 此论文，利用深卷积网络固有的多尺度金字塔层级结构，提出了一种具有横向连接的自顶向下的体系结构，用于构建各种尺度的高层语义特征图；

==**4、 Arbitrary-Oriented Scene Text Detection via Rotation Proposals**==（基于旋转建议的任意方向场景文本检测）

==**5、EAST An Efficient and Accurate Scene Text Detector**==（EAST:一种高效准确的场景文本检测器）

内容提要：

1. 简单而强大的pipeline
2. 在自然场景中产生快速而准确的文本检测
3. 

==**6、FOTS: Fast Oriented Text Spotting with a Unified Network**==（FOTS：基于统一网络的快速文本定位）

内容提要：

1. 统一的端到端可训练的快速文本定位网络；
2. FOTS算法具有较小的计算开销，并且联合训练方法使我们的方法比这两个阶段的方法性能更好；

==**7、Detecting Oriented Text in Natural Images by Linking Segments**==（基于SegLink的自然图像有向文本检测）

内容提要：

1. 大多数文本检测方法是针对水平拉丁文本，对于实时应用来说速度不够快；
2. SegLink:一种面向文本的检测方法；主要思想是将文本分解成两个可在本地检测到的元素——segments and links;
3. Segment:覆盖一部分单词或文本行的定向框；
4. Link:连接两个相邻的Segment，表示它们属于同一个单词或文本行；
5. 与一些方法相比，SegLink在准确性、速度和易于训练等方面都有所提高。
6. 以超过20FPS的频率在512*512的图像上运行，不用修改，能够检测出非拉丁文字的长行，如中文。

==**8、TextBoxes++: A Single-Shot Oriented Scene Text Detector**==(一种面向单镜头的场景文本检测器)

内容提要：

1. 场景文本检测的主要挑战：自然图像中文本的任意方向、小尺寸和显著变化的纵横比；
2. TextBoxes:端到端的可训练的快速场景文本检测器；可以在单次网络转发中以高精度和高效率检测任意方向的场景文本；

==**9、A Fast Text Detector with a Single Deep Neural Network**==

内容提要：

1. 端到端可训练的快速场景文本检测器
2. 在单个网络前向通道中以高精度和高效率检测场景文本
3. 在单词识别和端到端文本识别任务中性能良好

==**10、Detecting Text in Natural Image withConnectionist Text Proposal Network**==

内容提要：

1. 探索丰富的图像上下文信息，能够检测极其模糊的文本













