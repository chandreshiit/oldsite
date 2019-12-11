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

```latex
$$
\begin{align*}
y = y(x,t) &= A e^{i\theta} \\
&= A (\cos \theta + i \sin \theta) \\
&= A (\cos(kx - \omega t) + i \sin(kx - \omega t)) \\
&= A\cos(kx - \omega t) + i A\sin(kx - \omega t)  \\
&= A\cos \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big) + i A\sin \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big)  \\
&= A\cos \frac{2\pi}{\lambda} (x - v t) + i A\sin \frac{2\pi}{\lambda} (x - v t)
\end{align*}
$$
```





