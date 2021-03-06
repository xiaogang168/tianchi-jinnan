# ---天池 津南智造
比赛链接：https://tianchi.aliyun.com/competition/entrance/231695/introduction

比赛是典型的回归预测，评价参数是常见的均方差。不同之处在于在复赛阶段要求提供最优的参数，即是预测值最高的一组样本。
比赛同kaggle比赛类似，所选用的特征都是匿名特征。

首次提交比赛，得分为：，
下面是模型预测的效果图：

* 数据探索：
样本集：1396*44
测试集：150*43
样本集有44个特征变量，按照比赛描述，前43列均为流水线上每个环节的参数，最后一列是最终的产品收率。
  * 43列特征中，有若干时间特征，
time = ['A5','A9','A11','A14','A16','A20','A24','A26','A28','B4','B5','B7','B9','B10','B11']
这些时间特征取值相对固定，一般是某个整点时间或者整点时间段，根据这个特点，可以考虑将时间特征转变成固定数值的编码。因为时间特征会有先后顺序，因此，将不采用独热编码的形式。
  * 有一类特征的缺省值严重，缺省值比例占到了90%以上；或者某一固定值站到90%以上，将此类特征没有参考意义。
drop_col = ['A2','A7','A8','B13','B3','A23','A18','A13']
  * 类别特征，跟时间特征类似，该特征只会取某些固定的值，因此这类特征调整成数值编码
此外，还有连续特征（continue_col = ['A6','A27','B6','B8','B1','A1','A12','A15','A17']），还有特征分布不均衡，采用对数转换的形式将特征转换成对数的形式（log_col = ['A3','A4','B2','B12']）

* 特征预处理：
  * 空值处理：将空值根据特性类型，分别采用均值填充和样本中最频繁的值进行填充
  * 上述特征进行归一化，很多计算距离的算法会对特征的量纲有要求，特征归一化是必须的。

* 建模与预测
初次比赛，使用线性模型进行拟合，对训练样本交叉检验，最终均方差差值为：0.0006375，与排行榜上第一名奖金相差一个数量级，模型调优的空间还是相当大的。
