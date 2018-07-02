## Grammer chunking and model evaluation 

followings are the steps involved in order to achieve the objective

```
1) using conll2000 corpus from nltk taking out some statistics. such as number of tokens & tags.
2) making pos out of a small part of dataset 
3) NER
4) Manually correcting the NER, Chunking/Grammar 
5) evolution by using two ways and comparing its accuracy score.
```
desclaimer  - you don't need anything else except some basic packages of nltk to be installed. Thanks

Here is the code snippet which will help you to understand how to chunk a given text and the tree visualization as well. 

```python
import nltk
from nltk.corpus import conll2000
cp = nltk.RegexpParser('CHUNK: {<V.*> <TO> <V.*>}')
corpus = nltk.corpus.conll2000
for sent in conll2000.tagged_sents():
    tree = cp.parse(sent)
    for subtree in tree.subtrees():
        if subtree.label() == 'CHUNK': print(subtree)
```
to print the tree use following line of the code

```python
