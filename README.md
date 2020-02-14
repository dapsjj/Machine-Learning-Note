
# Machine-Learning-Note(机器学习笔记)

## 机器学习“判定模型”和“生成模型”有什么区别？
假设我们有两类动物，大象（y = 1）和狗（y = 0）。而X是动物的特征向量。

给定训练集，诸如逻辑回归或支持向量机算法之类的算法会尝试找到一条将大象和狗分开的直线（即决策边界）。然后，要将新动物归类为大象或狗，它会检查它落在决策边界的哪一侧，并据此做出预测。我们称这些判别学习算法。p(y|x)条件概率。

另一种方法，首先，看看大象，我们可以建立一个大象长什么样的模型。然后，查看狗，我们可以为狗的外观建立一个单独的模型。最后，要对新动物进行分类，我们可以将新动物与大象模型进行匹配，并与狗模型进行匹配，以查看新动物看起来更像大象还是更像我们在训练集中看到的狗。我们称这些生成学习算法。p(x,y)联合概率。


## 理解支持向量机
形式上，支持向量机在高维或无限维空间中构建一个超平面或一组超平面，可用于分类，回归或其他任务。
直观地，通过超平面可以实现良好的分离，该超平面与任何类别的最近训练数据点之间的距离最大（所谓的功能裕量），因为通常裕量越大，分类器分类器的泛化误差就越小。

通常与“内核函数”一起使用，本质上是对有效地使空间非线性化的标准内部产品的替代。这大致相当于从你的空间到应用线性分类器的某个“工作空间”中进行非线性变换，然后将结果拉回到您的原始空间，在该原始空间中，分类器使用的线性子空间不再是线性的。

支持向量机使用内核函数将数据隐式映射到可以线性分离的特征空间中：
![支持向量机_1.jpg](./image/支持向量机_1.jpg)


## 理解随机森林
在机器学习中，随机森林是一个包含多个决策树的分类器， 并且其输出的类别是由个别树输出的类别的众数而定。(少数服从多数)

随机森林的构建过程：
1. 假如有N个样本，则有放回的随机选择N个样本(每次随机选择一个样本，然后返回继续选择)。这选择好了的N个样本用来训练一个决策树，作为决策树根节点处的样本。
2. 当每个样本有M个属性时，在决策树的每个节点需要分裂时，随机从这M个属性中选取出m个属性，满足条件m < M。然后从这m个属性中采用某种策略（比如说信息增益）来选择1个属性作为该节点的分裂属性。
3. 决策树形成过程中每个节点都要按照步骤2来分裂（很容易理解，如果下一次该节点选出来的那一个属性是刚刚其父节点分裂时用过的属性，则该节点已经达到了叶子节点，无须继续分裂了）。一直到不能够再分裂为止。注意整个决策树形成过程中没有进行剪枝。
4. 按照步骤1~3建立大量的决策树，这样就构成了随机森林了。

例子：
我要到杭州旅游，刚好我有3个杭州的朋友，我让他们推荐景点，A推荐西湖、灵隐寺，B推荐西湖、南宋御街，C推荐西湖、雷峰塔。
大家都推荐西湖，那我一定得去西湖溜达溜达。这就是典型的随机森林的例子。

优点：

1）对于很多种资料，它可以产生高准确度的分类器；

2）它可以处理大量的输入变数；

3）它可以在决定类别时，评估变数的重要性；

4）在建造森林时，它可以在内部对于一般化后的误差产生不偏差的估计；

5）它包含一个好方法可以估计遗失的资料，并且，如果有很大一部分的资料遗失，仍可以维持准确度；

6）它提供一个实验方法，可以去侦测variable interactions；

7）对于不平衡的分类资料集来说，它可以平衡误差；

8）它计算各例中的亲近度，对于数据挖掘、侦测离群点（outlier）和将资料视觉化非常有用；

9）使用上述。它可被延伸应用在未标记的资料上，这类资料通常是使用非监督式聚类。也可侦测偏离者和观看资料；

10）学习过程是很快速的。


## 理解KNN
一、KNN算法概述

　　邻近算法，或者说K最近邻(KNN，K-NearestNeighbor)分类算法是数据挖掘分类技术中最简单的方法之一。所谓K最近邻，就是K个最近的邻居的意思，说的是每个样本都可以用它最接近的K个邻居来代表。Cover和Hart在1968年提出了最初的邻近算法。KNN是一种分类(classification)算法，它输入基于实例的学习（instance-based learning），属于懒惰学习（lazy learning）即KNN没有显式的学习过程，也就是说没有训练阶段，数据集事先已有了分类和特征值，待收到新样本后直接进行处理。与急切学习（eager learning）相对应。
  
　　KNN是通过测量不同特征值之间的距离进行分类。 
  
　　思路是：如果一个样本在特征空间中的k个最邻近的样本中的大多数属于某一个类别，则该样本也划分为这个类别。KNN算法中，所选择的邻居都是已经正确分类的对象。该方法在定类决策上只依据最邻近的一个或者几个样本的类别来决定待分样本所属的类别。
  
　　提到KNN，网上最常见的就是下面这个图，可以帮助大家理解。
  
　　我们要确定绿点属于哪个颜色（红色或者蓝色），要做的就是选出距离目标点距离最近的k个点，看这k个点的大多数颜色是什么颜色。当k取3的时候，我们可以看出距离最近的三个，分别是红色、红色、蓝色，因此得到目标点为红色。
  
![KNN_1.png](./image/KNN_1.png)

算法的描述：

　　1）计算测试数据与各个训练数据之间的距离
  
　　2）按照距离的递增关系进行排序
  
　　3）选取距离最小的K个点
  
　　4）确定前K个点所在类别的出现频率
  
　　5）返回前K个点中出现频率最高的类别作为测试数据的预测分类

二、关于K的取值

　　K：临近数，即在预测目标点时取几个临近的点来预测。
  
　　K值得选取非常重要，因为：
  
　　如果当K的取值过小时，一旦有噪声得成分存在们将会对预测产生比较大影响，例如取K值为1时，一旦最近的一个点是噪声，那么就会出现偏差，K值的减小就意味着整体模型变得复杂，容易发生过拟合。
  
　　如果K的值取的过大时，就相当于用较大邻域中的训练实例进行预测，学习的近似误差会增大。这时与输入目标点较远实例也会对预测起作用，使预测发生错误。K值的增大就意味着整体的模型变得简单。
  
　　如果K==N的时候，那么就是取全部的实例，即为取实例中某分类下最多的点，就对预测没有什么实际的意义了。
  
　　K的取值尽量要取奇数，以保证在计算结果最后会产生一个较多的类别，如果取偶数可能会产生相等的情况，不利于预测。

K的取法：

 　　常用的方法是从k=1开始，使用检验集估计分类器的误差率。重复该过程，每次K增值1，允许增加一个近邻。选取产生最小误差率的K。
   
　　一般k的取值不超过20，上限是n的开方，随着数据集的增大，K的值也要增大。

三、关于距离的选取

　　距离就是平面上两个点的直线距离
  
　　关于距离的度量方法，常用的有：欧几里得距离、余弦值（cos）, 相关度 （correlation）, 曼哈顿距离 （Manhattan distance）或其他。
  
　　Euclidean Distance 定义：
  
　　两个点或元组P1=（x1，y1）和P2=（x2，y2）的欧几里得距离是:
  
  ![欧几里得距离_1.png](./image/欧几里得距离_1.png)
  
   距离公式为：（多个维度的时候是多个维度各自求差）
   
   ![距离公式_1.png](./image/距离公式_1.png)
    
四、特点

  优点：
  
  1）思想简单，理论成熟，既可以用来做分类也可以用来做回归
  
  2）可用于非线性分类
  
  3）训练时间复杂度为O(n)
  
  4）准确度高，对数据没有假设，对outlier不敏感

  缺点：
  
  1）计算量太大
  
  2）对于样本分类不均衡的问题，会产生误判
  
  3）需要大量的内存
  
  4）输出的可解释性不强
  
  
  ## 有监督学习、无监督学习、半监督学习的区别
  监督学习：给小朋友一本有课后答案的习题册，让小朋友自己做题，并自己校对答案。
  无监督学习：比如参加一些开放性的竞赛（比如：数学建模竞赛），出题人只给出题目。参赛者，需要根据题目找出结构和规则，才能解题。（在没有老师的情况下，学生自学的过程。学生在学习的过程中，自己对知识进行归纳、总结。无监督学习中，类似分类和回归中的目标变量事先并不存在。要回答的问题是“从数据X中能发现什么”。）
  半监督学习：家教，家教老师给学生讲一两道例题思路，然后给学生布置没有答案的课后习题，让学生课后自己完成。

  监督学习是最常见的一种机器学习，它的训练数据是有标签的，训练目标是能够给新数据（测试数据）以正确的标签。
  例如，想让AI知道什么是猫什么是狗，一开始我们先将一些猫的图片和狗的图片（带标签）一起进行训练，学习模型不断捕捉这些图片与标签间的联系进行自我调整和完善，然后我们给一些不带标签的新图片，让该AI来猜猜这些图片是猫还是狗。
  经典的算法：支持向量机、回归、决策树、朴素贝叶斯

  无监督学习常常被用于数据挖掘，用于在大量无标签数据中发现些什么。它的训练数据是无标签的，训练目标是能对观察值进行分类或者区分等。相对于监督学习，无监督学习使用的是没有标签的数据。机器会主动学习数据的特征，并将它们分为若干类别，相当于形成「未知的标签」。
  非监督性学习是只给特征，没有给标签，就是高考前的一些模拟试卷，是没有标准答案的，也就是没有参照是对还是错，但是我们还是可以根据这些问题之间的联系将语文、数学、英语分开。
  通常无监督学习是指不需要人为注释的样本中抽取信息。例如word2vec。
  经典的算法：k-means、PCA等；

  半监督学习介于两者之间。算法上，包括一些对常用监督式学习算法的延伸，这些算法首先试图对未标识数据进行建模，在此基础上再对标识的数据进行预测。隐藏在半监督学习下的基本规律在于：数据的分布必然不是完全随机的，通过一些有标签数据的局部特征，以及更多没标签数据的整体分布，就可以得到可以接受甚至是非常好的分类结果。（此处大量忽略细节）
  例如：很多实际问题中，只有少量的带有标记的数据，因为对数据进行标记的代价有时很高。比如找到照片并给照片上的猫标上标签（lable）很麻烦，但是猫的各种姿势的猫片网上一搜一大堆。那我们能不能手动标记一部分猫片，然后让AI学习训练，然后再剩下没标记的猫片上做实验呢？
  经典算法：S3VM半监督支持向量机


## 有监督学习建模步骤
  监督学习是使用已知正确答案的示例来训练网络，每组训练数据有一个明确的标识或结果。想象一下，我们可以训练一个网络，让其从照片库中（其中包含气球的照片）识别出气球的照片。以下就是我们在这个假设场景中所要采取的步骤。

  步骤1：数据集的创建和分类 ​   
  首先，浏览你的照片（数据集），确定所有包含气球的照片，并对其进行标注。然后，将所有照片分为训练集和验证集。目标就是在深度网络中找一函数，这个函数输入是任意一张照片，当照片中包含气球时，输出1，否则输出0。

  步骤2：数据增强（Data Augmentation） ​   
  当原始数据搜集和标注完毕，一般搜集的数据并不一定包含目标在各种扰动下的信息。数据的好坏对于机器学习模型的预测能力至关重要，因此一般会进行数据增强。对于图像数据来说，数据增强一般包括，图像旋转，平移，颜色变换，裁剪，仿射变换等。

  步骤3：特征工程（Feature Engineering） ​   
  一般来讲，特征工程包含特征提取和特征选择。常见的手工特征(Hand-Crafted Feature)有尺度不变特征变换(Scale-Invariant Feature Transform, SIFT)，方向梯度直方图(Histogram of Oriented Gradient, HOG)等。由于手工特征是启发式的，其算法设计背后的出发点不同，将这些特征组合在一起的时候有可能会产生冲突，如何将组合特征的效能发挥出来，使原始数据在特征空间中的判别性最大化，就需要用到特征选择的方法。在深度学习方法大获成功之后，人们很大一部分不再关注特征工程本身。因为，最常用到的卷积神经网络(Convolutional Neural Networks, CNN)本身就是一种特征提取和选择的引擎。研究者提出的不同的网络结构、正则化、归一化方法实际上就是深度学习背景下的特征工程。

  步骤4：构建预测模型和损失 ​   
  将原始数据映射到特征空间之后，也就意味着我们得到了比较合理的输入。下一步就是构建合适的预测模型得到对应输入的输出。而如何保证模型的输出和输入标签的一致性，就需要构建模型预测和标签之间的损失函数，常见的损失函数(Loss Function)有交叉熵、均方差等。通过优化方法不断迭代，使模型从最初的初始化状态一步步变化为有预测能力的模型的过程，实际上就是学习的过程。

  步骤5：训练 ​     
  选择合适的模型和超参数进行初始化，其中超参数比如支持向量机中核函数、误差项惩罚权重等。当模型初始化参数设定好后，将制作好的特征数据输入到模型，通过合适的优化方法不断缩小输出与标签之间的差距，当迭代过程到了截止条件，就可以得到训练好的模型。优化方法最常见的就是梯度下降法及其变种，使用梯度下降法的前提是优化目标函数对于模型是可导的。

  步骤6：验证和模型选择 ​   
  训练完训练集图片后，需要进行模型测试。利用验证集来验证模型是否可以准确地挑选出含有气球在内的照片。在此过程中，通常会通过调整和模型相关的各种事物（超参数）来重复步骤2和3，诸如里面有多少个节点，有多少层，使用怎样的激活函数和损失函数，如何在反向传播阶段积极有效地训练权值等等。

  步骤7：测试及应用 ​   
  当有了一个准确的模型，就可以将该模型部署到你的应用程序中。你可以将预测功能发布为API（Application Programming Interface, 应用程序编程接口）调用，并且你可以从软件中调用该API，从而进行推理并给出相应的结果。

## 常用分类算法优缺点对比
|算法|优点|缺点|
|:-|:-|:-|
|Bayes 贝叶斯分类法|1）所需估计的参数少，对于缺失数据不敏感。<br />2）有着坚实的数学基础，以及稳定的分类效率。|1）需要假设属性之间相互独立，这往往并不成立。（喜欢吃番茄、鸡蛋，却不喜欢吃番茄炒蛋）。<br />2）需要知道先验概率。<br />3）分类决策存在错误率。|
|Decision Tree决策树|1）不需要任何领域知识或参数假设。<br />2）适合高维数据。<br />3）简单易于理解。<br />4）短时间内处理大量数据，得到可行且效果较好的结果。<br />5）能够同时处理数据型和常规性属性。|1）对于各类别样本数量不一致数据，信息增益偏向于那些具有更多数值的特征。<br />2）易于过拟合。<br />3）忽略属性之间的相关性。<br />4）不支持在线学习。|
|SVM支持向量机|1）可以解决小样本下机器学习的问题。<br />2）提高泛化性能。<br />3）可以解决高维、非线性问题。超高维文本分类仍受欢迎。<br />4）避免神经网络结构选择和局部极小的问题。|1）对缺失数据敏感。<br />2）内存消耗大，难以解释。<br />3）运行和调参略烦人。|
|KNN K近邻|1）思想简单，理论成熟，既可以用来做分类也可以用来做回归； <br />2）可用于非线性分类；<br /> 3）训练时间复杂度为O(n)； <br />4）准确度高，对数据没有假设，对outlier不敏感；|1）计算量太大。<br />2）对于样本分类不均衡的问题，会产生误判。<br />3）需要大量的内存。<br />4）输出的可解释性不强。|
|Logistic Regression逻辑回归|1）速度快。<br />2）简单易于理解，直接看到各个特征的权重。<br />3）能容易地更新模型吸收新的数据。<br />4）如果想要一个概率框架，动态调整分类阀值。|特征处理复杂。需要归一化和较多的特征工程。|
|Neural Network 神经网络|1）分类准确率高。<br />2）并行处理能力强。<br />3）分布式存储和学习能力强。<br />4）鲁棒性较强，不易受噪声影响。|1）需要大量参数（网络拓扑、阀值、阈值）。<br />2）结果难以解释。<br />3）训练时间过长。|
|Adaboosting|1）adaboost是一种有很高精度的分类器。<br />2）可以使用各种方法构建子分类器，Adaboost算法提供的是框架。<br />3）当使用简单分类器时，计算出的结果是可以理解的。而且弱分类器构造极其简单。<br />4）简单，不用做特征筛选。<br />5）不用担心overfitting。|对outlier比较敏感|


## 分类算法的评估方法

评价指标列表
![评价指标列表](./image/分类算法评价指标_1.png)


