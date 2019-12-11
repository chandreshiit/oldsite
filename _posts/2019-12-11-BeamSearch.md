---
title: 'Beam search decoding in 5 mins'
date: 2019-12-11
tags: [Beam Search]
author_profile: false

---
### Beam Search

Over the years, beam search has become one of the most popular technique for decoding a sequence at test time. Most of the deep learning papers using sequence models use beam search to find alternative translations, part-of-speech tags, named-entities etc. In the post, I am going to cover beam search. 

Beam search is one of the many techniques for searching a graph such as *breadth-first-search, depth-first-search, best-first-search, hill-climbing* . You can think of it as a constrained version of the bread-first search where we explore only *k* best neighbours of the current node. Here , *k* is called **Beam Width**. The discussion here follows in terms of label prediction in the sequence models though it can be applied to other domains without loss of generality.

Imagine that you got the following output from one of your LSTM cell.

```Markdown
$$
\[\begin{bmatrix}
1&2&3\\
2&1&3\\
3&1&2\\
\end{bmatrix}\]
$$
```

You can read about beam search [here](http://www.qinuu.com/2019/04/23/3-sequence-models-attention-mechanism/) and [here](https://machinelearningmastery.com/beam-search-decoder-natural-language-processing/#comment-514613). What I will give you the code. 

```python
import tensorflow as tf, numpy as np
def beam_search_decoder(data, k):
    # first convert logits to probabilites so that all numbers are +ve
    data  = tf.nn.softmax(data)
    sequences = [[list(), 0.0]]
    # walk over each step in sequence
    for row in data:
        all_candidates = list()
        # expand each current candidate
        for i in range(len(sequences)):
            seq, score = sequences[i]
#             for j in range(len(row)): # instead of exploring all the labels, explore only k best at the current time
            # select k best
            best_k = np.argsort(row)[-k:]
            # explore k best
            for j in best_k:
                candidate = [seq + [j], score + tf.math.log(row[j])]
                all_candidates.append(candidate)
        # order all candidates by score
        ordered = sorted(all_candidates, key=lambda tup:tup[1], reverse=True)
        # select k best
        sequences = ordered[:k]
    return sequences
```

Above code expects that your data is just logits coming from the output of RNN/LSTM. It will compute the softmax first. Then, at each step, it iteratively expands each node and choosing the best K before expending.  If you call the above function on the sample data, you get the below output.

```python
data = np.array([[1.,2,3],[2,1,3],[3,1,2]])
seq = beam_search_decoder(data, k=3)
print(seq)
```

```
>[[[2, 2, 0], <tf.Tensor: id=10511, shape=(), dtype=float64, numpy=-1.2228178933331413>], [[2, 2, 2], <tf.Tensor: id=10505, shape=(), dtype=float64, numpy=-2.2228178933331413>], [[2, 0, 0], <tf.Tensor: id=10529, shape=(), dtype=float64, numpy=-2.2228178933331413>]]
```



