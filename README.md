# CLRS-Benchmark-Report
A review and introduction to the CLRS Benchmark developed by the team at Deepmind

## Topics Covered

* Introduction to the CLRS Benchmark Paper and Background Context
  * What is the CLRS Benchmark?
  * Neural Networks vs Algorithms
  * Recent Attempts at Teaching Neural Networks Algorithms
* Overview of the Benchmark
  * Motivation
  * Which Algorithms to Benchmark Against
* Implementation of the Benchmark
  * Representation of Problems
  * Trajectories of Algorithm Processes
* Results of Baseline Architectures
  * Processor Network Description
  * Baseline Model Overview
  * Results
* Applications and Future Work

## Introduction to the CLRS Benchmark Paper and Background Context

### What is the CLRS Benchmark?

 The CLRS Benchmark is an attempt at measuring the progress made towards teaching neural networks how to perform algorithmic reasoning tasks, such as sorting arrays or finding the shortest path between two nodes on a graph.
 
 The paper that introduces this benchmark was presented at the International Conference of Machine Learning (ICML) in 2022.  The main contributor is Petar Velickovic, a researcher at Deepmind.  You can find out more about Petar [here](https://petar-v.com/)
 
 The CLRS Benchmark takes its name from the authors of the seminal Introduction to Algorithms textbook by Cormen, Leiserston, Rivest, and Stein.  This textbook is ubiquitous among graduate level computer science programs.
 
<img src="https://user-images.githubusercontent.com/52665911/234370713-1cac148d-6561-4dbb-8798-613716a21dcc.jpg" width = "20%" height = "10%">

 You can view the entire public repository on Deepmind's github [here](https://github.com/deepmind/clrs)
 
 ### Neural Networks vs Algorithms
 
  Neural Networks and Algorithms are on opposite ends of the spectrum of tools to solve problems.  A simple way to break down their attributes is as follows:
  
  | Algorithms | Neural Networks |
  | ---        | ---             |
  | Can accept arbitrary-sized inputs | Extract important features of data|
  | Interpretable and provable | Once trained can be applied to different tasks|
  | Inputs need to conform to the algorithm | Massive data requirements | 
  | New task, new algorithm | Black boxes|
  
   Developting networks that can combine the strengths of algorithms and traditional neural networks while mitigating their weaknesses would be a powerful development.
   
 ### Recent Attempts at Training Neural Networks Algorithms
 
 Over the past five to ten years attempts have been made to construct neural networks that can learn from data how to perform algorithmic tasks.  [In this paper from Google Brain](https://arxiv.org/abs/1511.08228), convolutional gated recurrent units (CGRUs) are used to perform successive steps of basic tasks such as binary addition, sequence reversal, and sequence sorting.
 
<img width="564" alt="GPU" src="https://user-images.githubusercontent.com/52665911/234432590-d67c06e2-efd8-4ff6-9c19-9ddee097b02e.png">

In the above example, an $n$ dimensional array is input into three input nodes (each column is an input node), and it passes through one more layer with three nodes - this is supposed to be a single step of the algorithm being learned ($s_0, s_1$,...)

## Overview of the Benchmark

### Motivation - Why This Problem?

Algorithms are well understood but require abstract inputs and create abstract outputs, both of which need interpretation in order to be applicable.  In a [RAND report](https://apps.dtic.mil/sti/citations/AD0093458) published in 1955 on evaluating railway network capacity, the problem is summed up nicely:

> The evaluation of both railway system and individual track capacities is, to a considerable extent, an art.  The authors know of no tested mathematical model or formula that includes all of the variations and imponderables that must be weighed.  Even when the individual has been closely associated with the particular territory he is evaluating, the final answer, however accurate, is largely one of judgement and experience.

If neural networks can learn to apply algorithmic reasoning to real data, this "art" can be augmented by machine learning.  Neural networks could discover new applications of existing algorithms, or, more excitingly, invent new algorithms that can themselves be proven and interpreted.

### Motivation - Why a Benchmark?

Benchmarks have been useful in spurring on progress in many areas.  ImageNet created a lot of momentum in the development of convolutional neural networks.  The Wikipedia Treebank was extremely helpful in the development of using recurrent neural networks for natural language processing.

Benchmarks provide two things:
* A common set of problems and data to work with
* Performance metrics that can be understood across communities

By making algorithmic reasoning a benchmark for neural networks, a community can grow around this problem and develop further understanding about artificial general intelligence.

### Which Algorithms to Benchmark Against

The Introduction to Algorithms textbook has 94 algorithms, but not all of them are good candidates for a benchmark.  Velickovic and the team developing the benchmark decided on the following criteria on which algorithms _not_ to use:

* No NP-hard problems - the ground truth will be too hard to provide (to be discussed later)
* No tasks requiring a numerical output - floating point differences are not good indicators of reasoning performance
* No tasks on data structures - they do not in and of themselves test algorithmic reasoning
* No tasks requiring dynamic memory allocation - again difficult to provide ground truth

As such, the team was left with 30 algorithms:

- Sorting
  - Insertion sort
  - Bubble sort
  - Heapsort (Williams, 1964)
  - Quicksort (Hoare, 1962)
- Searching
  - Minimum
  - Binary search
  - Quickselect (Hoare, 1961)
- Divide and conquer
  - Maximum subarray (Kadane's variant) (Bentley, 1984)
- Greedy
  - Activity selection (Gavril, 1972)
  - Task scheduling (Lawler, 1985)
- Dynamic programming
  - Matrix chain multiplication
  - Longest common subsequence
  - Optimal binary search tree (Aho et al., 1974)
- Graphs
  - Depth-first search (Moore, 1959)
  - Breadth-first search (Moore, 1959)
  - Topological sorting (Knuth, 1973)
  - Articulation points
  - Bridges
  - Kosaraju's strongly connected components algorithm (Aho et al., 1974)
  - Kruskal's minimum spanning tree algorithm (Kruskal, 1956)
  - Prim's minimum spanning tree algorithm (Prim, 1957)
  - Bellman-Ford algorithm for single-source shortest paths (Bellman, 1958)
  - Dijkstra's algorithm for single-source shortest paths (Dijkstra et al., 1959)
  - Directed acyclic graph single-source shortest paths
  - Floyd-Warshall algorithm for all-pairs shortest-paths (Floyd, 1962)
- Strings
  - Naïve string matching
  - Knuth-Morris-Pratt (KMP) string matcher (Knuth et al., 1977)
- Geometry
  - Segment intersection
  - Graham scan convex hull algorithm (Graham, 1972)
  - Jarvis' march convex hull algorithm (Jarvis, 1973)

## Implementation of the Benchmark

### Representation of Problems

### Trajectories of Algorithm Processes

## Results of Baseline Architectures

### Processor Network Description

### Baseline Model Overview

### Results

## Application and Future Work

