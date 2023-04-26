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

Algorithms are well understood but require abstract inputs and create abstract outputs, both of which need interpretation in order to be applicable.  In the RAND report published in 1955 on evaluating railway network capacity summed up the problem nicely:

> The evaluation of both railway system and individual track capacities is, to a considerable extent, an art.  The authors know of no tested mathematical model or formula that includes all of the variations and imponderables that must be weighed.  Even when the individual has been closely associated with the particular territory he is evaluating, the final answer, however accurate, is largely one of judgement and experience.

If neural networks can learn to apply algorithmic reasoning to real data, this "art" can be augmented by machine learning.  Neural networks could discover new applications of existing algorithms, or, more excitingly, invent new algorithms that can themselves be proven and interpreted.

