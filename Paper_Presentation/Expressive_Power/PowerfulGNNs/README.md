# How Powerful are Graph Neural Networks?

## Motivation

The design of new GNNs is mostly based on empirical intuition, heuristics, and experimental trial-and-error. There is little theoretical understanding of the properties and limitations of GNNs, and formal analysis of GNNs’ representational capacity is limited.

## Contributions and Results
* GNNs are at most as powerful as the WL test in distinguishing graph structures.
* Established conditions on the neighbor aggregation and graph pooling functions under which the resulting GNN is as powerful as the WL test.
* Identified graph structures that cannot be distinguished by popular GNN variants, such as GCN and GraphSAGE and characterized the kinds of graph structures such GNN-based models can capture. 
* Developed a simple neural architecture, Graph Isomorphism Network (GIN) and showed that its discriminative/representational power is equal to the power of the WL test.

## Preliminaries



## Experimental Results

**Dataset**

The target task is graph classification. Datasets are from two domains:
* 4 bioinformatics datasets: MUTAG, PTC, NCI1, PROTEINS
* 5 social network datasets
  
![Social network datasets details](fig/datasets.png)

**Training Set Performance**

![Main result of training set performance](fig/figure4.png)

Higher accuracy in training set refect better representational power for GNNs. 

Main results:
* GINs are able to almost perfectly fit all the training sets
* Explicit learning of <img src="https://render.githubusercontent.com/render/math?math=\epsilon"> yields no gain compared to fixing <img src="https://render.githubusercontent.com/render/math?math=\epsilon"> to 0
* GNNs with MLPs are better than GNNs with 1 layer perceptrons
* GNNs with sum aggregators are better than GNNs with mean/max pooling aggregators
* WL subtree kernel is the method with the ceiling performance across all methods

**Testing Set Performance**

![Main result of testing set performance](fig/table1.png)

The better accuracy on test set reflects better generalization capacity and demonstrates stronger expressive power. Main results:
* GIN-0 is the best or very close to the best on all 9 datasets
* GIN-0 is better than GIN-<img src="https://render.githubusercontent.com/render/math?math=\epsilon"> due to its simplicity
* Mean-based GNNs perform much worse than sum-based GNNs

## Pros and Cons

