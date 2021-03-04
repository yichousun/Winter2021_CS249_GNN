# Provably Powerful Graph Networks

## Background and Motivation

Popular message passing GNN cannot distinguish between graphs that cannot be distinguished by the 1-WL test, while many simple graphs are indistinguishable by the 1-WL test. Therefore, it demands to develop more powerful graph networks that can provably enjoy higher expressiveness. Recently, it has the shown that the k-order invariant and equivariant graph neural networks can be possibly more powerful than messagge passing GNNs. Based on this idea, this paper construct a new GNN model that provably achieves the same expressiveness as the 3-WL test.

## Preliminaries

### k-WL and k-FWL

The k-WL and k-FWL are a series of tests similar to that of the WL isomorphism test, except they look at k-tuple combinations of verticies and their neighbors (as opposed to just one vertex by itself). There are a few important properties of these tests that motivate this work:

<ol>
<li>1-WL and 2-WL have equivalent discrimination power.</li>
<li>k-FWL is equivalent to (k + 1)-WL for k ≥ 2.</li>
<li>For each k ≥ 2 there is a pair of non-isomorphic graphs distinguishable by (k + 1)-WL but
not by k-W</li>
</ol>

As these tests get more powerful as k increases, it is advantageous to construct networks that can be expressive as the k-WL test for some arbitrary k. The k-FWL test is included in this work as it allows us to get 3-WL expressivness with a lower computational complexity.

## Contributions and Results
* This paper proves that there exists a k-order GNN that can be as powerful as the k-WL test.
* This paper builds a provably stronger, simple and scalable model which has a provable 3-WL expressive power.
* In experiments, the proposed GNN model has achieved the state-of-the-art performance on popular graph classification and regression tasks.


