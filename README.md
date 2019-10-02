# ML-Base-Knowledge-Summarise





### Methods Dealing With Overfitting           
1）增大数据集         
2）减少features数量           
3）正则         
4）dropout(神经网络）     
5）early stopping          
6）用adaptive learning rate（比如adam,神经网络)
7）减少网络层数             
8）Bagging (参考随机森林，每次放回采样做预测，训练一堆互不关联的决策树，以平均投票结果作为输出）       
9）贝叶斯优化器（bayes optimizer，python可直接调api），随着采样参数训练次数的增多，通过先验分布求出后验分布，从而得到估计的最佳参数）     


### Methods Dealing With Underfitting
1) 增加参数，比如由于模型非线性太强，可以增加多项式特征提升模型复杂度，或使用kernel函数升纬使得模型在高纬度线性可分（参考svm）     
2）增加神经网络层数（也是增加参数的一种手段）     
3）减少正则化参数          


### 树模型王者（gbdt）                
#### gbdt之基本原理             
1）每次用一个弱分类器去拟合残差，每个弱分类器的本质是一个回归树，假如要生成M个弱分类器和有k个类的label。           
2）每次生成弱分类器时，需要生成k个回归树，每个回归树拟合对应一个类的残差，预测的概率可以用softmax计算，残差为标签减去之前已生成的模型的预测概率。   
3）生成新树的原则是拟合该残差，贪婪算法，每次选择收益最大的特征在收益最佳的节点进行分裂（此时还可以顺便记录收益用于计算impoartance)。      
4）最后将新的弱分类器并入模型。          
5）理论上gbdt对异常值比较敏感，需要特征归一化（由于每个树是回归树）。但是，不知道为什么在实践中（kaggle比赛数据集），归一化之后效果并不理想。    
6）gbdt控制过拟合的手段，min_split_gain，min_child_weight, min_data_leaf, depth, num_leaf, reg_alpha, reg_lambda, early stopping。 

### ROC曲线以及AUC             
1）ROC曲线的面积AUC（area under curve）通常是我们判断一个分类模型好与坏的重要指标（一般是2分类模型，2分类模型才有正样本和负样本）。        
2）ROC曲线为向左上角凸的曲线，如果roc曲线为一条从左下角至右上角的一条直线，那说明你的模型和瞎猜并没有什么区别（50%猜中）。         
3）ROC曲线的Y轴为真阳率（TP rate），等同于recall rate，TPrate = TP/(TP+FN),即真正的正样本有%多少被你成功找出来了。        
4）ROC曲线的X轴是假阳率（FP rate）= FP/（FP+TN),即有%多少的负样本被你错误的预测成了正样本。          
5）这两个指标是完全相反的（我们需要在最大化真阳率的同时最小化假阳率），假如我全部预测为正样本，此时真阳率必为1，但是假阳率同样为1，这是我们不想看见的。 
6）所以我们通过调整不同的threshold（阈值），可以描绘出一个模型的roc曲线，从而得到他的AUC。                   







