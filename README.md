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

### Here is the code snippet which will help you to understand how to chunk a given text and the tree visualization as well. 

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
### Here is what `trigram chunker` look like 

```python
class TrigramChunkParser(ChunkParserI):
    def __init__(self, train_sents):
        # Extract only the (POS-TAG, IOB-CHUNK-TAG) pairs
        train_data = [[(pos_tag, chunk_tag) for word, pos_tag, chunk_tag in tree2conlltags(sent)] 
                      for sent in train_sents]
 
        # Train a TrigramTagger
        self.tagger = TrigramTagger(train_data)
 
    def parse(self, sentence):
        pos_tags = [pos for word, pos in sentence]
 
        # Get the Chunk tags
        tagged_pos_tags = self.tagger.tag(pos_tags)
 
        # Assemble the (word, pos, chunk) triplets
        conlltags = [(word, pos_tag, chunk_tag) 
                     for ((word, pos_tag), (pos_tag, chunk_tag)) in zip(sentence, tagged_pos_tags)]
 
        # Transform to tree
        return conlltags2tree(conlltags)
 
 
trigram_chunker = TrigramChunkParser(train_sents)
print (trigram_chunker.evaluate(test_sents))
```
and in later part I have tried one `another model` which can be seen in the script
