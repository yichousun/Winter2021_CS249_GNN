# Heterogeneous Graph Transformer

## Introduction

Most GNNs are designed for homogeneous networks, in which all nodes or edges have the same feature space and representation distribution, making them infeasible for representing evolving heterogeneous structures. In this paper, we present the Heterogeneous Graph Transformer architecture for modeling Web-scale heterogeneous and dynamic graphs (Microsoft Academic Graph). The model can automatically learn and extract meaningful metapaths for different downstream tasks.

## Related Work

Heterogeneous graphs, or so-called relational graph, is a special type of graph, in which their nodes and edges are associated with a specific type. Heterogeneous graphs can model complex systems, and it’s flexible to capture rich semantic knowledge. For more details, we can refer to (this book)[https://www.morganclaypool.com/doi/abs/10.2200/s00433ed1v01y201207dmk005].


We firstly introduce a meta relation schema, which is a high-level description of a heterogenous graph semantic. For an edge e = (s, t) linked from source node s to target node t, its meta relation is denoted as ⟨τ (s), ϕ(e), τ (t)⟩. For example, the Microsoft Academic Graph (MAG) has the following schema, where the author and paper can be connected by different authorshiops, paper and venue can be connected by conf/journal, paper and field can be connected by different level.

Metapaths are is defined as a sequence of such meta relation. For example, A-P-A is the authors on the same paper, A-P-V is authors that publish papers at a particular venue. Metapathes denote a composition of relations. Utilizing metapaths, we can estimate the similarity of some nodes. For example, given A-P-A metapath, we can model the co-authorship of two authors. Using metapths we can estimate the node similarity on the graph. However, picking the correct path for a particular task is a non-trivial thing, as different metapaths lead to totally different outputs.

For example, when we ask who is most similar to Christos Fgaloutos, using the first metapath A-P-A we focus on the co-authorships, so most likely we get his students or clos collaborators. However, if we use A-P-V-P-A, which focus on authors publishing papers on the same venue, we most likely will get the other data mining researchers that work on similar works.


To sum up, metapath is a useful tool to mine a specific property of the heterogeneous graph, and different task might require different meta paths, which traditionally are designed by the researchers. 

When we come to deep learning days, people wants to represent the nodes and data into continuous space, and learn the representation by a objective in an end-to-end manner. For heterogenous graphs, there emerges a plenty of works that combine meta paths with graph representation learning methods, such as R-GCN and HetGNN. However, they still need to manually decide which meta paths to turn the graph into homogenous one, and then adopt standard GNN to handle it. Is there a way that we can automatically learn the meta paths on-the-fly, and also capture the rich semantic of the graph into model design?


## Solution

To automatically learn the meta-relations for a specific task, we propose to introduce node- and edge- dependent attention. We leverage meta relation <source node type, edge type, target node type> to parameterize attention and message passing weight. Following the Transformer architecture, we first calculate the message for each node, then calculate pair-wise attention, based on the weight matrices parametriced by meta-relation. Finally we aggregate messages by each attention weight.

To handle graph dynamics, instead of slicing the input graph into different timestamp, we propose to maintain all edges in different times and adopt RTE to encode time. For those general nodes (like author and venue), during subgraph sampling, we recursively let them inherit parents' timestamp. We further utilize layer-dependent importance sampling to sample subgraph, while keeping each type of nodes with a budget to have balanced size.


## Experimental results

HGT is evaluated on Microsoft Academic Graph (MAG), with paper-field, paper-venue and author disambiguation tasks. It outperforms sota GNN baselines by 9%-21%, and currently rank 1st on Stanford OGBN-MAG benchmark. 

## Major conclusions

To handle graph heterogeneity, we use meta-relation-triplet to parametrize weights. Model can automatically detect useful meta paths without manual design

To handle graph dynamics and large-scale, we design Relative Temporal Encoding to represent dynamic graph

To handle large-scale graph, we design Heterogeneous Mini-Batch Graph Sampling algorithm to conduct efficient training on billion-scale heterogeneous graph


## Cons

The HGT model maintains a different set of parameter for each node type, so the memory consumption is much larger than standard GNN model. It's worthwhile exploring whether the schema can be encoded as relational bias (similar to position / temporal encoding)


