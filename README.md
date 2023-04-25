# CLRS-Benchmark-Report
A review and introduction to the CLRS Benchmark developed by the team at Deepmind

## Topics Covered

* Introduction to the CLRS Benchmark Paper and Background Context
  * Neural Networks vs Algorithms
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
