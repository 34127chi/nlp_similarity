# nlp_similarity
对文本相似度的认识<br>

项目目前的瓶颈在文本相似度这块，因此自己这个月花了些时间在这块，也多亏了好朋友的一些指引，对这块有了基本的了解，以下是对这块的总结：<br>

1,http://nlp.town/blog/sentence-similarity/ 提到了四种方法<br>
  1）基于词向量加权平均来计算句子的向量，接着用距离来衡量相似度,根据加权的方式、是否考虑停用词等有不同的变种<br>
  2）word mover‘s distance，一个词对应的向量可以看作空间的一个点，一个词移到另一个词的距离是可以度量的，所以可以计算一个句子中移动到另一个句子的最小距离，进而来度量句子之间的相似度<br>
  3）smooth inverse frequncy。认为平均句子中的词向量会给类似停用词过多的权重，因此该方法先基于词频的词向量加权，得到句向量，接着用句向量减去句子的主成分，最终的句向量再来计算句子之间的相似度<br>
  4）基于预训练模型的方法。以上方法没有考虑句子中词出现的顺序，仅是利用了词袋，并且学得词向量都是比较通用的，没有针对特定具体任务或者目标的，因此提出基于预训练模型的方法，这个预训练模型是根据其他的特定具体任务学习得到的，但这个预训练模型的作用也是为了encode(编码)句子得到固定长度的向量，与word2vecto的作用类似。ps：nlp相关的通用预训练模型没有cv的多，中文的已知没有<br>
  
2，Learning to Rank Short Text Pairs with Convolutional Deep Neural Networks 将排序问题当作二分类问题来做，输入是question和answer以及0，1标签，0代表负样例，1代表正样例，损失函数是二分类的交叉熵，也称为point-wise类型。论文里面将question 和 answer分别用了一个模型来encode（编码），相比于现在更多的是用同一个模型来encode（编码），模型在分类之前也考虑了计算questio和answer的相似度作为特征（我理解为是一种attention机制），最终question和answer的encode以及相似度特征一起作为特征进行分类。ps：实验部分提到加入question 和 answer中词的共现特征（word-count），这个特征对模型的提升效果较大，我做的实验也是这个情况。<br>

3，LSTM-BASED DEEP LEARNING MODELS FOR NON-FACTOID ANSWER SELECTION 输入是question、ground trueth answer、incorrect answer，损失函数是hinge loss —— L = max{0, M − cosine(q, a+) + cosine(q, a−)}，也称为pair-wise类型。论文里面先提了一个基本模型，是利用lstm来 encode（编码） question和 answer，在基本模型的基础上考虑了加入更多的特征（集成cnn）和基于问题的attention（注意力）机制。ps：这里的incorrect answer 是随机挑选出来的，如果训练时随机的负样本太弱太简单（和正确答案差异性很大），而在预测时候选答案又太难太挑战（和正确答案很相似），效果就不好了，可以考虑Semi-hard Negative Samples，具体论文：FaceNet: A Unified Embedding for Face Recognition and Clustering<br>

4，Attentive Pooling Networks <br>

5，Learning to Rank: From Pairwise Approach to Listwise Approach<br>

6，Deep Learning for Answer Sentence Selection<br>


总结：快速入门某个领域，读综述或者文章介绍部分，注意实验部分<br>
