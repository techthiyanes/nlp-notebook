# Pytorch implementation of Glove.

## Concept of Glove

![w2c](../images/w2c.png)

- [https://blog.csdn.net/coderTC/article/details/73864097](https://blog.csdn.net/coderTC/article/details/73864097)
- [https://juejin.cn/post/6844903923279642638](https://juejin.cn/post/6844903923279642638)
- [https://nlpython.com/implementing-glove-model-with-pytorch/](https://nlpython.com/implementing-glove-model-with-pytorch/)

![glove1](../images/glove1.png)
![glove2](../images/glove2.png)
![glove3](../images/glove3.png)
![glove4](../images/glove4.png)
![glove5](../images/glove5.png)
![glove6](../images/glove6.png)
![glove7](../images/glove7.png)

## Visualization

Save the embedding along with the words to TSV files as shown below, upload these two TSV files to [Embedding Projector](https://projector.tensorflow.org/) for better visualization.

```
def save_embedding(self, outdir, idx2word):
    embeds = self.in_embed.weight.data.cpu().numpy()        
    f1 = open(os.path.join(outdir, 'vec.tsv'), 'w')
    f2 = open(os.path.join(outdir, 'word.tsv'), 'w')        
    for idx in range(len(embeds)):
        word = idx2word[idx]
        embed = '\t'.join([str(x) for x in embeds[idx]])
        f1.write(embed+'\n')
        f2.write(word+'\n')
```