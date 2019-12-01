---
title: 'Dependency Parsing in 5 mins'
date: 2019-12-01
tags: [Dependency Parsing]
author_profile: false

---
**TL;DR**
Dependency parsing in natural language processing is a parsing technique which gives relations (labels) to words via head-dependent relationship. Contrary to constituent-based parsing where relationship between words is embedded in deep, in dependency graph (defined below), relationship are flat. More formally, dependency parsing  creates connected, directed, and labeled graph $$G=(V,E)$$ where $$V$$ is the set of words and $$E$$ is the set of edges consisting of ordered pair of verticies. The graph (dependency tree to be more precise)   has following properties.
1. There is **root** node which does not have any parent associated to it.
2. Every vertex in the graph has an incoming arc except the root.
3. There is a unique path from the root to every other vertics.
 

