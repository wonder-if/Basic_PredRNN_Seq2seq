# Basic_PredRNN_Seq2seq
Basic_PredRNN_Seq2seq_Radar_Prediction
从Convlstm2D的基础上改编: https://github.com/ndrplz/ConvLSTM_pytorch 可用于雷达回波等短临预报领域,采用模仿Dr.SXJ的Seq2seq结构.

PredRNN++是最近南京信息工程大学强对流天气精细预报的研讨会中国家气象局短临预报的标配预报模型。但是论文中官配的PredRNN完全体代码简直就是崩溃(菜鸡我看不懂昂)，因此在几个群友的教唆下，开源一个简单易懂版的PredRNN。
首先这里先感谢几位大佬.
京东的张老师/群主一号,神一样的男人.
上海眼控科技的吕.老师/哥.
东南大学的蜗牛哥/群主一号Plus.
黑总地主/虽然我不知道这货真实名字是啥.
大佬Plus号喵老师.
气科院的方祖亮/我是他的粉丝N号.
##############说实话在这个群,看着他们说话我都能学到很多东西QAQ###########
复现这类时空序列预测的代码个人建议可以参照Ai蜗牛车公众号的时空预测专栏。
ConvLSTM2D->ConvLSTM3D->PredRNN ->PredNet ->Memory in Memory-> E3D-LSTM是我原始复现路线.
按照国家气象局官方的短临预报PPT,我就先绕过PredNet复现了PredRNN和PredRNN++,因此时间仓促致使有些Bug暂时没有发现,肯定需要其他人进行指正(蟹蟹各位大佬)(完成MIM并且检查前面没问题的情况下再放出PredRNN++的简易版,以免坑人)
※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※下面是经过自己理解,在ConLSTM2D开源代码的基础上复现的一个简易版的PredRNN.
主要的代码解释已经标注在对应的代码中.主要Debug点是Cell中的卷积,欢迎大家指正.
雷达回波数据使用的是厦门，杭州，宁波的雷达拼图,由于资料的保密性，因此个人没有公开.
实况为第7次外推的结果.即从时刻0-9外推到时刻10-16的第16
由于本机配置实在很低,所以给出的是100×100的分辨率.模型设置Layer=2, hidden_dim(隐藏层维度)分别为7和1, Layer方向上时间状态M由于当前层输入和输出维度的一致性，因此统一成dim=7.
模型Train使用的是0-9时刻的6min雷达回波图,采用教师强迫的Seq2Seq形式.
模型Test利用t-1时刻的Output作为t时刻的Input,去预测t时刻的雷达回波特征.
结果是任何指标上都要明显好于pytorch和tensorflow版的ConvLSTM2D(即使ConvLSTM2D在模型深度的设置上要更占优势).
时间关系后续再放上其它几类模型的对比结果吧.
PredRNN++效果并没有比PreRNN好太多,暂时还在Debug阶段.
