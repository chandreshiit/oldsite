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



