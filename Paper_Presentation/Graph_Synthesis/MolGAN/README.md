# [MolGAN: An implicit generative model for small molecular graphs](https://arxiv.org/pdf/1805.11973.pdf)
**Authors:** Nicola De Cao, Thomas Kipf

**Presenters:** Daisy Zheng, Nilay Shah, Nima Zaghari

**Code:** https://github.com/nicola-decao/MolGAN

## Introduction

Finding new chemical compounds with desired properties is a challenging task in de novo drug design. The large space makes most search methods very expensive. Many techniques, such as SMILES, have disadvantages that are hard to overlook. The syntactic rules and strict representation make them difficult to implement. This paper will use implicit methods for molecular graph generation. More specifically, they utilize a generative adversarial network (GAN) and reinforcement learning (RL) objective to generate molecules with desired properties. This work is the first to address the generation of graph-structured data utilizing GANs for molecular synthesis. Discrete graph structures are predicted at once in an efficient manner. With the help of a discriminator and reward network, the generative model is able to work effectively directly on graph structured representations. 

## Related work

Objective-Reinforced Generative Adversarial Networks (ORGAN) is the closest comparison to this paper. They utilize SeqGan to learn output sequences. Where they differ is that they use SMILES as opposed to graphs for molecular representations. In their reinforcement learning, they also use REINFORCE for optimzation while this paper uses DDPG. Many works have adopted a similar approach of using a SMILES representation along with a variational auto encoder. These methods often limit the decoding process to follow semantic rules. In addition, they become prohibitively expensive when we consider the fact that we want to be invariant to node ordering.  

## Solution

## Experimental results




## Conclusions



## Pros and cons

Pros:
* Very high (~100%) valid output structure ratio
* GraphNN + RL is effective for biochemical optimization 
* Light computational cost, fast learning

Cons:
* Mode collapse - same structure is repeatedly generated
  * Normalization techniques (e.g. spectral normalization) could help
* Fixed atom count

