# RNN-Attention
两层attention lstm评论情感分析
 
### 业务背景介绍:  
目的：通过 海量京东和天猫的用户商品评论对商品产生评分，帮组运营人员发现好的产品推送给用户  
在此之前尝试过Imdb类似的评分计算，以及kmeans聚类，但都未达到特别理想效果，转而考虑使用lstm的情感分析来评分


![计算流图](https://github.com/rebornfly/RNN-Attention/blob/master/img/graph.png)  
 
### 模型介绍  
#### first attention:  
* 输入 ：字或者词向量（本模型没有额外训练词向量），采用字向量，batch_size * vector_size * comment_size  
* 输出 ： 评论的向量batch_size*vector_size
#### second attention:  
* 输入 ：batch_size*vector_size的评论向量  
* 输出 ：机型的评分
 
### 代码结构  
* db.py 数据库读取数据  
* data.py 对数据预处理的文件随机抽样打印结果
* infer.py  对数据库的数据机型评分
* model.py  最关键部分，绘制tensorflow计算流图
* ops.py  最基本的神经网络操作
* test.py  测试用例（可以忽略）
* train.py  神经网络训练，超参数设置  
* data目录  数据预处理生成字id  
* plot目录  绘制attention图

### 参数设置
```
self.num_epochs=200            # num of epochs 
self.batch_size= 1000           # batch size
self.hidden_size= 100          # num hidden units for RNN
#self.embedding="glove"        # random|glove
self.embedding="random"        # random|glove
self.emb_size= 200             # num hidden units for embeddings
self.max_grad_norm=5           # max gradient norm
#self.keep_prob=0.9             # Keep prob for dropout layers
self.keep_prob=0.9             # Keep prob for dropout layers
self.num_layers=2              # number of layers for recurrsion
self.max_input_length=40       # max number of words per review
self.min_lr=1e-6               # minimum learning rate
self.decay_rate=0.96           # Decay rate for lr per global step (train batch)
self.save_every=10             # Save the model every <save_every> epochs
self.model_name="imdb_model"   # Name of the model
self.num_classes=5             # number of class for classify
 ```
        self.infer_dir = "data/ckpt"
