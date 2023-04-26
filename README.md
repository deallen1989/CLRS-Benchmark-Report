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

 The restrictions placed on which algorithms are included in the benchmark, while understandable, present a problem - how do we represent problems that might be traditonally thought of as having numerical outputs?
 
 The paper uses the example of Insertion Sort to explain how every problem is represented on graphs.  With insertion sort, each element is considered in turn, and inserted into the right-most position where it is greater than every element to the left.  Thus we might think that the output of Insertion Sort is a series of numbers.  
 
 However there is a way to represent this problem on a directed graph - by having each node assigned to a value of the array to sort, and an edge from one node to the node directly to the left of it.
 
 <img width="149" alt="verthints" src="https://user-images.githubusercontent.com/52665911/234607234-10a96338-c502-40b0-b824-d104c4b824f0.png">
 
 Above, we see a graphical representation of Insertion sort on the series 52431.  All this representation is doing is iterating along each element (the red pointer), finding the node that should point to it (the blue pointer), and rearranging the edges of the graph so the nodes are sorted up to that element.

### Trajectories of Algorithm Processes

 Given that neural networks are famously black boxes that make it difficult if not impossible to figure out their inner workings, how will we know if a network is simply memorizing outputs rather than learning the actual reasoning of an algorithm?
 
 To address this, the CLRS Benchmark team devised a system of hints, or states that the algorithm should be in after a certain number of steps, assuming the network is performing the algorithm correctly.
 
 Again for the example of insertion sort, after two iterations of the algorithm we want the network to have the array represented like the figure above.  If instead the network was simply searching for the lowest value node and building a new graph from scratch, that would not be the desired output at all.
 
 Therefore, the benchmark will provide, with probability $P=.5$, a hint to the network as it progresses through the algorithm.  The rationale for noisy hinting is given in [this paper on "Noisy Nodes"](https://arxiv.org/abs/2106.07971).
 
 Below is an example for pseudocode on how the benchmark constructs hints, following the color code of the previous figure:
 
 <img width="240" alt="pseudocode" src="https://user-images.githubusercontent.com/52665911/234617349-b7500fb0-7d48-48f2-89a9-9e0d74ae4ebf.png">
 
### Feature Types and Loss Functions

 Finally, for each feature of a graph, there is a value type and corresponding loss function that the benchmark uses to evaluate performance:
 
 |Type|Description|Loss|
 |---|---|---|
 |Scalar| $\mathbb{R}$| Mean Squared Error|
 |Cateorical | $1,$ . . . $,K$ | Cross-Entropy|
 |Mask | { $0,1$ } | Binary Cross-Entropy|
 |Mask_One| "One Hot" | Categorical Cross-Entropy|
 |Pointer|Similarity Between Nodes | Categorical Cross-Entropy|

## Results of Baseline Architectures

### Processor Network Description

 The CLRS Benchmark team used several baseline models to kickstart the search for improved performance, but before getting into the results, it will be helpful to describe the neural networks they used - called Processor Networks.
 
 The processor networks used at baseline architectures for the benchmark follow a three-step process:
 1. Encode
 2. Process
 3. Decode

#### 1. Encode

Encoding takes the raw values ($x_i$ for node $i$ , $e_{ij}$ for an edge between nodes $i$ and $j$ , and $g$ for a feature of the overall graph), and encodes them with node, edge, and graph functions $f_n$ , $f_{e}$ , or $f_g$ , to create encoded values $h$ as follows:

* $h_i = f_n(x_i)$
* $h_{ij} = f_e(e_{ij})$
* $h_g = f_g(g)$
 
#### 2. Process

Once the encoded values are calculated, the network "passes messages" $m_{ij}$ along each edge between nodes.  A message function $f_m$ builds the message, and an aggregation function $\oplus$ compiles all the messages sent to a single node to create the aggregate message for node $i$ , $m_i$.  Finally, a new encoded value $h_i'$ is calculated for each node based on the old encoded value $h_i$ and the aggregate message $m_i$ with a readout function $f_r$ :

* $m_{ij} = f_m(h_i,h_j,h_{ij},h_g)$
* $m_i = \underset{(i,j) \in E}{\oplus} m_{ji}$
* $h_i' = f_r(h_i,m_i)$

The aggregation function $\oplus$ changes but can be anything from a summation, a maximum, or a self-attention softmax.  Descriptions for each baseline model will be given later where applicable.

This processing is better understood visually:

<img width="400" alt="cs224" src="https://user-images.githubusercontent.com/52665911/234652617-6429a7d3-2deb-4a78-8ca9-7b2659fc3d6e.png">

#### 3. Decode

Finally, after a certain number of iterations, a decoding process takes place where we get new "raw values" $y_i$ and $y_{ij}$ with decode functions $f^{-1}_n$ and $f^{-1}_e$ :

* $y_i = f^{-1}_n(h_i')$
* $y_{ij} = f^{-1}_e(h_i',h_j')$

**Each Encode-Process_Decode procedure is a single step of the algorithm.**  All of the functions $f$ above have parameters that can be taught based on the loss functions comparing decoded values to true values, either at the hints given randomly or the final output.


### Baseline Model Overview



### Results

## Application and Future Work

