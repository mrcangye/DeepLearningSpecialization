# 第一周测验 Introduction to Deep Learning

## 1.What does the analogy “AI is the new electricity” refer to?

AI是新的电力指的是？
- [ ] AI runs on computers and is thus powered by electricity, but it is letting computers do things not possible before. 
  AI 在计算机上运行，由电力供电，但它让计算机以前不可能做事。
- [ ] Through the “smart grid”, AI is delivering a new wave of electricity. 
  通过"智能电网"，人工智能正在提供新一轮的电力。
- [ ] AI is powering personal devices in our homes and offices, similar to electricity.
  AI 正在为家庭和办公室的个人设备供电，类似于电力  
- [x] Similar to electricity starting about 100 years ago, AI is transforming multiple industries.
  与大约 100 年前开始的电力类似，人工智能正在改变多个行业。

## 2.Which of these are reasons for Deep Learning recently taking off? (Check the three options that apply.)
深度学习迅速发展的原因？
- [x] Deep learning has resulted in significant improvements in important applications such as online advertising, speech recognition, and image recognition. 
	深度学习是的在线广告，语言识别，图像识别等重要应用有了显著改进
- [x] We have access to a lot more computational power. 
	可以获得更多的算力
- [ ] Neural Networks are a brand new field. 
	神经网络是新的领域
	**神经网络90年代就出来理论了**
- [x] We have access to a lot more data.
	可以获得更多的数据
## 3.Recall this diagram of iterating over different ML ideas. Which of the statements below are true? (Check all that apply.)
回想这个图，以下哪个说法是对的？
![](./static/Idea-Code-Experiment.png)
- [ ] It is faster to train on a big dataset than a small dataset. 
	在大数据集中进行训练比在小数据集上训练更快。
	**数据规模越大训练越慢**
- [x] Faster computation can help speed up how long a team takes to iterate to a good idea. 
	更快的计算可以加快团队迭代到好方式所需的时间。
- [x] Being able to try out ideas quickly allows deep learning engineers to iterate more quickly. 
	能够快速尝试想法，使深度学习的工程师能够更快地迭代。
- [x] Recent progress in deep learning algorithms has allowed us to train good models faster (even without changing the CPU/GPU hardware). 
    最近在深度学习算法方面的进步使我们能够更快地训练好模型（即使无需更改 CPU/GPU 硬件
## 4.When an experienced deep learning engineer works on a new problem, they can usually use insight from previous problems to train a good model on the first try, without needing to iterate multiple times through different models. True/False?
当一个有经验的深度学习工程师在解决一个新问题时，他们通常可以使用以前的经验一次就训练一个好的模型，而无需通过不同的模型多次重复。真/假？
**还是需要对模型进行调整拟合，一招鲜吃遍天基本不管用**
- [x] False
- [ ] True
## 5.Which one of these plots represents a ReLU activation function?
其中哪一个图表示ReLU激活函数
- [x] ![](./static/question1.png)
**ReLU函数**
- [ ] ![](./static/question3.png)
**sigmoid函数**
- [ ] ![](./static/question2.png)
**leaky ReLU函数**
- [ ] ![](./static/question4.png)
**tanh**函数

## 6.Images for cat recognition is an example of “structured” data, because it is represented as a structured array in a computer. True/False?
猫的识别图像是"结构化"数据的示例，是因为它在计算机中表示为结构化数组。真/假？
**图像，语音，文本都不是结构化数据**
- [x] False
- [ ] True
## 7.A demographic dataset with statistics on different cities' population, GDP per capita, economic growth is an example of “unstructured” data because it contains data coming from different sources. True/False?
人口数据集包含不同城市的人口统计数据、人均 GDP、经济增长等。是"非结构化"数据的一个例子，因为它包含来自不同来源的数据。真/假？
**这些数据可以在数据库中表示出来，应该是结构化数据。是不是结构化数据跟来源无关**
- [x] False
- [ ] True
## 8.Why is an RNN (Recurrent Neural Network) used for machine translation, say translating English to French? (Check all that apply.)
为什么 RNN（卷积神经网络）用于机器翻译，比如将英语翻译成法语？
- [x] It is applicable when the input/output is a sequence (e.g., a sequence of words).  
	当输入/输出是一个序列（例如，单词序列）时，它适用
- [x] It can be trained as a supervised learning problem. 
	它可以被训练成一个有监督的学习问题。
- [ ] RNNs represent the recurrent process of Idea->Code->Experiment->Idea->.... 
	RNN 代表想法 - >代码 - >体验 - >意>的反复过程。
- [ ] It is strictly more powerful than a Convolutional Neural Network (CNN). 
	它比卷积神经网络 （CNN） 更强大。
## 9.In this diagram which we hand-drew in lecture, what do the horizontal axis (x-axis) and vertical axis (y-axis) represent? 
  在我们讲课时亲手绘制的这张图表中，水平轴（x轴）和垂直轴（y轴）代表什么？
 ![](.\static\x,y.png)



- [x] x-axis is the amount of data
        y-axis (vertical axis) is the performance of the algorithm.
		x轴是数据量
		y 轴（垂直轴）是算法的性能
- [ ] x-axis is the input to the algorithm

 	   y-axis is outputs.
 	   x轴是算法的输入
 	   y轴是输出。
- [ ] x-axis is the amount of data
       y-axis is the size of the model you train. 
      x轴是数据量
      y轴是您训练的模型的大小。
- [ ] x-axis is the performance of the algorithm
       y-axis (vertical axis) is the amount of data.
       x轴是算法的性能
       y 轴（垂直轴）是数据量。
## 10.Assuming the trends described in the previous question's figure are accurate (and hoping you got the axis labels right), which of the following are true? (Check all that apply.)
假设上一个问题的数字中描述的趋势是准确的（并希望您得到正确的轴标签），以下哪一个是正确的？
- [x] Increasing the training set size generally does not hurt an algorithm’s performance, and it may help significantly. 
       增加培训集大小通常不会损害算法的性能，并且可能会有显著帮助。
- [ ] Decreasing the size of a neural network generally does not hurt an algorithm’s performance, and it may help significantly.
       缩小神经网络的大小通常不会损害算法的性能，而且可能会有显著帮助。
- [x] Increasing the size of a neural network generally does not hurt an algorithm’s performance, and it may help significantly.
      增加神经网络的大小通常不会损害算法的性能，而且可能会有显著帮助
- [ ] Decreasing the training set size generally does not hurt an algorithm’s performance, and it may help significantly.
       降低培训集大小通常不会损害算法的性能，并且可能会有显著帮助。