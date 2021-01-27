# [Interaction Networks for Learning about Objects,Relations and Physics](https://arxiv.org/abs/1612.00222)
Authors: Peter W. Battaglia, Razvan Pascanu, Matthew Lai, Danilo Rezende, Koray Kavukcuoglu, NIPS 2016.  
Presenters: **Shuwen Qiu**, **Jiayue Sun (jysun@cs.ucla.edu)**, **Qing Li (dylan.liqing@gmail.com)**

## Introduction

## Related works

## Method
![Schematic of an interaction network](schematic.png)
This paper introduces the *Interaction Networks* (IN), which can reason how objects in complex systems interact, supporting dynamic prediction and inference about the systems' abstract properties. 

Take physical reasoning as an example. An interaction network takes objects and relations as input, reasons about their interactions, and applies the effects and physical dynamics to predict new states. Assuming two objects and one directed relationship, the first (sender) influences the second (receiver) via their interaction. This interaction's effect can be predicted by a relation-centric function, which takes as input the two objects and attributes of their relationship. The object-centric function takes as input the interaction and the current state of an object to predict its future state. 

The above formulation can be expanded to larger and more complex systems by representing them as a graph, where the nodes correspond to the objects and the edges to the relations. The model rearranges the objects and relations into interaction terms by a marshaling function and computes their effects via a relational model. The effects are then aggregated and combined by an aggregation function with the objects and external effects to generate input for an object model, predicting how the interactions and dynamics influence the objects. This basic IN can predict the evolution of states in a dynamical system; for example, in physical simulation, the final output may represent the objects' future states. The IN can also be augmented with an additional aggregation model to predict global properties, such as energies, for the whole system. 

## Exprimental Results

## Major Contributions

## Pros and Cons

