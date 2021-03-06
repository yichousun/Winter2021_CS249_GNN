# Provably Powerful Graph Networks

## Background and Motivation

Popular message passing GNN cannot distinguish between graphs that cannot be distinguished by the 1-WL test, while many simple graphs are indistinguishable by the 1-WL test. Therefore, it demands to develop more powerful graph networks that can provably enjoy higher expressive power. Recently, it has the shown that the k-order invariant and equivariant graph neural networks can be possibly more powerful than messagge passing GNNs. Based on this idea, this paper construct a new GNN model that provably achieves the same expressiveness as the 3-WL test.

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

### The Graph Network

In order to get expressive power of a k-WL graph, this paper constructs its networks to operate according to the rules of the k-WL test. This allows for the network to discriminate between graphs that the k-WL text can. However, we also want the property that isomorphic graphs will always produce the same output. In order to accomplish this, the network is constructed out of layers that are either equivariant or invariant with respect to the permutation group. This allows for the network to be invariant as a whole to the permutation group, which means that any graphs that are isomorphic to eachother will produce the same result from any network.

### Color Representation

In this paper colors are represented as vectors, and as such encoding can be done by concatenation. The difficult part is how we represent the colors of multisets generated during the k-WL updates, which maintaining an equivariant layer. To do this, they use Power-Sum Multi-symmetric Polynomials. This polynomial has certain properties that make it an unique representation of a multiset but still allow it to be equivariant to the permutation group. As a result this allows for an equivariant layer that follows the k-WL algorithm rules.

## Contributions and Results
* This paper proves that there exists a k-order GNN that can be as powerful as the k-WL test.
* This paper builds a provably stronger, simple and scalable model which has a provable 3-WL expressive power.
* In experiments, the proposed GNN model has achieved the state-of-the-art performance on popular graph classification and regression tasks.

## Pros and Cons

### Pros
* Very interesting theory about how to extend the expressivness of a GCN. Most other works seem focused on 1-WL tests.

* The developed GNN model is simple (compared with other GNN models with k-WL guarantees for k>2) and performs better than existing GNN models.

### Cons
* In practice the constructed GNN model does not follow the theoretical suggestions by using very high-dimensional embedding vectors. Therefore, it is not clear whether the proposed GNN model can be more powerful than 3-WL test empirically.

* Very mathematically dense paper. Sometimes authors make jumps in logic that aren't very clear.

