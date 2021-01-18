# Composition-based Multi-Relational Graph Convolutional Networks

The Slides are avaiable as [Google Slides format](https://github.com/malllabiisc/CompGCN).

The codes are avaiable in [this repo](https://github.com/malllabiisc/CompGCN).

## Introduction

As graphs are one of the most expressive data structures it is often used for understanding social behaviour, performing scientific prediction and tackling other nobel problems. Traditionally  Convolutional neural networks could only handle euclidean data or were focused on learning the representation of nodes in simple undirected graphs. Previous works on multi-relational graphs suffered from over parameterization and were not applicable for tasks such as link prediction for relation in graphs.

Research over Knowledge graphs have led to learning of both the nodes and the relations.  But, they are limited to learning embeddings using link prediction objectives or learning from task-specific objectives (like classifications) in a non-relational graph setting.

Due to the current state, the authors propose a novel framework for incorporating multi-relational information in Graph Convolutional Networks which leverages a variety of composition operations from knowledge graph embedding techniques to jointly embed both nodes and relations in a graph.

## Related Works

Graph Convolutional Networks: GCNs were first introduced by Bruna et al. (2013). Currently most of the existing GCN methods follow Message Passing Neural Networks (MPNN) framework (Gilmer et al., 2017) for node aggregation.
GCNs for Multi-Relational Graph: An extension of GCNs for relational graphs is proposed by Marcheggiani & Titov (2017). Ye et al. (2019) have also proposed an extension of GCNs for embedding both nodes and relations in multi- relational graphs.
Knowledge Graph Embedding: Knowledge graph (KG) embedding is a widely studied field (Nickel et al., 2016; Wang et al., 2017) with application in tasks like link prediction and question answering (Bordes et al., 2014). Most KG embedding approaches define a score function and train node and relation embeddings such that valid triples are assigned a higher score than the invalid ones.

## Background

GCN on Undirected Graphs: Given a graph G = (V,E,X), where V denotes the set of vertices, E is the set of edges, and  XR|v|*d0 represents d0- dimensional input features of each node. The node representation for a single GCN layer is defined as: H=f(ẬXW)Here,Ậ = D-1/2(A+I)D+1/2,  Dii=∑j(A+I)ij ,WRd0xd1and f is some activation function. H encodes the immediate neighborhood of each node in the graph. For capturing multi-hop dependencies Hk+1=f(ẬHkWk), where k denotes the number of layers, WkRdkxdk+1and H0 = X.

GCN on Multi-Relational Graphs: For a multi-relational graph G = (V,R,E,X), where R denotes the set of relations, and each edge (u, v, r) represents that the relation r ∈ R exist from node u to v. The GCN formulation as devised is based on the assumption that information in a directed edge flows along both directions. Hence, for each edge (u, v, r) ∈ E, an inverse edge (v, u, r-1) is included in G. The representations obtained after k layers of directed GCN is given by Hk+1=f(ẬHkWrk),where Wkrdenotes the relation specific parameters of the model. To prevent over-parameterization they use direction-specific weight matrices. Schlichtkrull et al. (2017) address over- parameterization by proposing basis and block-diagonal decomposition of Wkr.


## Methods

In order to relax the issue of over parameterization, CompGCN proposes to learn a d-dimensional relational representation, along with the standard node embedding. Relationships are represented as vectors and undergo certain compositional transformations, such as subtraction, multiplication, and circular-correlation. The aforementioned compositions are not learnable for simplicity in this work, however, CompGCN can handle parameterized composition functions as well. The node embedding update rule for the CompGCN is then defined by aggregations of a learnable matrix multiplied by the composed relational representations and node embedding. ComGCN handles inverse relations with a different parameterization matrix. Relational representations are being updated with a learnable matrix likewise.

In order to handle a large number of relations, CompGCN proposes to represent relational vectors as linear combinations of several learnable base vectors, while the linear combinational weights are learnable as well. CompGCN, compared to many other variants of GCNs, are more parameter efficient, and can derive a reduction to other variants.

## Experiments

There are three standard tasks being evaluated in this work: (1) Link Prediction which predicts the missing relations on knowledge graphs, (2) Node classification which predicts the type of nodes, and (3) graph classification, which predicts the overall types of a given graph. Baselines are relational-GCN, directed-GCN, and weighted-GCN, where they all do not resolve the over parameterization issue, but handle relations on graphs. The experimental results show that CompGCN outperforms all the other baselines (or at least on par) with different scoring functions. There are also several interesting analyses conducted, such as analysis on how performance changes against different number of relational basis vectors and relationships themselves.
The experiments prove the claims of effectiveness and the scalability of the proposed CompGCN.

## Major Conclusions and Pros

1. This work proposes CompGCN, a variant of GCN utilizes relational representations on multi-relational graphs, which alleviates the over parameterization issue of conventional GCN.

2. CompGCN proposes a simple yet effective way to make good use of both relational and node embeddings.

3. This work is general as it can handle different versions of compositional functions of relational vectors.

4. This work provides nice and concise summaries of how CompGCN is related to other variants of GCNs.

5. The linear combination idea of composing complex relational vectors is neat.
The scalability and effectiveness of CompGCN is justified through a set of extensive 
experiments.

## Cons or Improvements

1. For simplicity, this work only handles non-parameterized compositional functions, while many prior works on knowledge graph embedding could not be utilized, such as Conv-E or NTN. Showing that these meaningful pretrained knowledge graph embedding can further improve the CompGCN model would be an exciting work for extensions.

2. Although using the linear combinations of basis vectors can lead to very good scalability, the interpretability of basis vectors versus specific relation types is rather unclear. Maybe some categorical features can be leveraged to imply some interpretations versus relations.

3. Future work can include knowledge base population tasks as we suppose this work can provide stronger generalization ability over TranE and ConvE.