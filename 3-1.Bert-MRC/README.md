# Bert-MRC

### 原理
在输入文本前加上了实体类型的描述信息，这些实体类型的描述作为先验知识提高了模型抽取的效果，所以BERT-MRC模型在数据量匮乏的场景下，通过在输入文本前面拼接的query获得了一定的先验信息，提升了性能。本实验中拼接的query分别为：请找出句子中提及的机构/请找出句子中提及的地名/请找出句子中提及的人名。

1). model.py:
采用CrossEntropyLoss

2). model_1.py:
采用BCELoss, 将概率值做n次方缓解类别失衡问题，[参考](https://kexue.fm/archives/7161) 

3). model_2.py:
Focal loss for multiple class，[参考](https://zhuanlan.zhihu.com/p/49981234) 

### 模型预测效果

run demo_eval.py

```
Sent: 真情写英魂－－《张浩传奇》简介
NER: [['张浩', 'PER']]
Predicted NER: [['张浩', 'PER']]
---------------

Sent: 李一安
NER: []
Predicted NER: [['李一安', 'PER']]
---------------

Sent: 张浩（原名林毓英），是我国工人运动的卓越领导人。
NER: [['张浩', 'PER'], ['林毓英', 'PER']]
Predicted NER: [['张浩', 'PER'], ['林毓英', 'PER']]
---------------

Sent: 今年的2月25日，是他诞辰百周年纪念日。
NER: []
Predicted NER: []
---------------

Sent: 他出生在湖北农村一个手工织染家庭，1921年参加革命，1922年2月由林毓南、恽代英介绍入党，先后在武汉、长沙、黄石、安源、上海、广州、香港、哈尔滨、抚顺等地从事工人运动。
NER: [['湖北', 'LOC'], ['林毓南', 'PER'], ['恽代英', 'PER'], ['武汉', 'LOC'], ['长沙', 'LOC'], ['黄石', 'LOC'], ['安源', 'LOC'], ['上海', 'LOC'], ['广州', 'LOC'], ['香港', 'LOC'], ['哈尔滨', 'LOC'], ['抚顺', 'LOC']]
Predicted NER: [['湖北', 'LOC'], ['武汉', 'LOC'], ['长沙', 'LOC'], ['黄石', 'LOC'], ['安源', 'LOC'], ['上海', 'LOC'], ['广州', 'LOC'], ['香港', 'LOC'], ['哈尔滨', 'LOC'], ['抚顺', 'LOC'], ['林毓南', 'PER'], ['恽代英', 'PER']]
---------------

Sent: 1942年3月6日，因病在延安逝世，毛泽东等中央领导同志亲自为其抬棺。
NER: [['延安', 'LOC'], ['毛泽东', 'PER']]
Predicted NER: [['延安', 'LOC'], ['毛泽东', 'PER']]
---------------

Sent: 当年，张浩受共产国际派遣，只身一人从莫斯科出发，取道蒙古人民共和国，穿越茫茫荒原，不远万里抵达延安，在革命斗争的关键时刻将共产国际的指示带到了中共中央；
NER: [['张浩', 'PER'], ['共产国际', 'ORG'], ['莫斯科', 'LOC'], ['蒙古人民共和国', 'LOC'], ['延安', 'LOC'], ['共产国际', 'ORG'], ['中共中央', 'ORG']]
Predicted NER: [['共产国际', 'ORG'], ['共产国际', 'ORG'], ['中共中央', 'ORG'], ['莫斯科', 'LOC'], ['蒙古人民共和国', 'LOC'], ['延安', 'LOC'], ['张浩', 'PER']]

.
.
.

Sent: 希腊人将瓦西里斯与奥纳西斯比较时总不忘补充一句：他和奥纳西斯不同，他没有改组家庭。
NER: [['希腊', 'LOC'], ['瓦西里斯', 'PER'], ['奥纳西斯', 'PER'], ['奥纳西斯', 'PER']]
Predicted NER: [['希腊', 'LOC'], ['瓦西里斯', 'PER'], ['奥纳西斯', 'PER'], ['奥纳西斯', 'PER']]
---------------

Sent: 重视传统家庭观念的希腊人，对瓦西里斯幸福的家庭充满赞誉。
NER: [['希腊', 'LOC'], ['瓦西里斯', 'PER']]
Predicted NER: [['希腊', 'LOC'], ['瓦西里斯', 'LOC'], ['瓦西里斯', 'PER']]
---------------

gold_num = 6048
predict_num = 5558
correct_num = 4725
precision = 0.8501259445843828
recall = 0.78125
f1-score = 0.8142340168878166
```