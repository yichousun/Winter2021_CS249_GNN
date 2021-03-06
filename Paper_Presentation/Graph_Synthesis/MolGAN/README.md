# [MolGAN: An implicit generative model for small molecular graphs](https://arxiv.org/pdf/1805.11973.pdf)
**Authors:** Nicola De Cao, Thomas Kipf

**Presenters:** Daisy Zheng, Nilay Shah, Nima Zaghari

**Code:** https://github.com/nicola-decao/MolGAN

## Introduction

Finding new chemical compounds with desired properties is a challenging task in de novo drug design. The large space makes most search methods very expensive. Many techniques, such as SMILES, have disadvantages that are hard to overlook. The syntactic rules and strict representation make them difficult to implement. This paper will use implicit methods for molecular graph generation. More specifically, they utilize a generative adversarial network (GAN) and reinforcement learning (RL) objective to generate molecules with desired properties. This work is the first to address the generation of graph-structured data utilizing GANs for molecular synthesis. Discrete graph structures are predicted at once in an efficient manner. With the help of a discriminator and reward network, the generative model is able to work effectively directly on graph structured representations. 

## Related work

Objective-Reinforced Generative Adversarial Networks (ORGAN) is the closest comparison to this paper. They utilize SeqGan to learn output sequences. Where they differ is that they use SMILES as opposed to graphs for molecular representations. In their reinforcement learning, they also use REINFORCE for optimzation while this paper uses DDPG. Many works have adopted a similar approach of using a SMILES representation along with a variational auto encoder. These methods often limit the decoding process to follow semantic rules. In addition, they become prohibitively expensive when we consider the fact that we want to be invariant to node ordering.  

## Solution
The paper proposes an implicit generative model called MolGAN, which predicts the entire molecular graph structure at once for small molecules. The model is composed of 3 major parts: the generator, the discriminator, and the reward network.

**Generator:** The purpose of the generator is to learn a transformation from a prior distribution (noise sampled from a normal distribution) to the training data distribution, in order to generate a molecular structure that closely resembles molecules from the actual dataset. The generator takes in a vector representing random noise and outputs 2 objects: an annotation matrix **X** and an adjacency tensor **A**, which each contain categorical probability distributions over node (atom) and edge (bond) types - these are then categorically sampled to generate the actual molecule that will be used in the rest of the model. The generator is trained using a loss function that includes both the WGAN loss from the discriminator and the RL loss from the reward network.

**Discriminator:** The discriminator's job is to distinguish between generator samples (fake data) and dataset samples (real data). It takes samples from both the generator and the dataset as input and is trained using the WGAN objective to determine where the sample came from, outputting a representative scalar value. It uses a graph convolutional network (GCN) architecture to propogate the node signals over several layers before aggregating these embeddings into a graph representational vector and processing this a final graph level scalar to output.

**Reward Network:** The reward network is included to help optimize the generation of molecules to include certain desirable properties. It is trained (using mean squared error objective) to approximate a reward function that will output reward scores that closely match the scores given by some external software. Like the discriminator, it samples from both the generator and the dataset and outputs a scalar repesenting the expected reward scores. These scores are fed back to the generator as part of the reinforcement learning process in order to help train it to generate molecules that maximize the reward. The reward network follows the same GCN architecture as the disciminator.

## Experimental results

MolGAN is evaluated on the QM9 Dataset of 133,885 organic compounds composed entirely of carbon (C), hydrogen (H), oxygen (O), nitrogen (N), and fluorine (F) atoms. Each compound has at most 9 heavy atoms (CONF). The method evaluation metrics used are: 
* Validity = Valid structures / All generated structures 
* Novelty = Valid structures not in training dataset / All valid generated structures 
* Uniqueness = Unique valid structures / Total valid structures

The generated molecules are further evaluated on their: 
* Druglikeness = How likely a compound is to be a drug
* Synthesizability = How easy is a molecule to synthesize 
* Solubility = The degree to which a molecule is hydrophilic

**Experiment 1:** Experiment 1 explores the effects of varying the lambda hyperparameter which controls the trade-off between the WGAN and RL objectives in the combined generator loss function. It is found that the optimal value for lambda is 0 and only the reward loss is necessary. The intuition for this result is that valid molecules are implicitly optimized by the RL loss since invalid molecules receive zero reward during training. Therefore, if the RL loss component is strong, the generator is optimized to generate mostly valid molecular graphs. 

**Experiment 2:** Experiment 2 compares MolGAN to ORGAN, the closest related work to MolGAN. While MolGAN performs worse in the uniqueness metric with a value around 2%, indicating that it is susceptible to mode collapse, MolGAN outperforms ORGAN in validity and time consumption. The higher validity score stems from the indirect optimization from the GAN loss, while the computational efficiency is due to one-shot approach to molecular generation taken by MolGAN as opposed to the sequential approach taken by ORGAN.

**Experiment 3:** Experiment 3 compres MolGAN to variational autoencoding methods such as CharacterVAE, GrammarVAE, and GraphVAE. While the other models perform better in the uniqueness metric once again, MolGAN outperforms all by achieving high validity and novelty scores which none of the other methods accomplish. 


## Conclusions

This paper presents MolGAN, an implicit generative model for small molecular graphs. The model is able to outperfrom variational autoencoding methods by acheiving high validity and novelty scores while not requiring a permutation-dependent likelihood function and is superior to the recent SOTA sequential model, ORGAN, in achieving higher chemical property scores as well as having a ~5x computational speedup.  

## Pros and cons

Pros:
* Very high (~100%) valid output structure ratio
* GraphNN + RL is effective for biochemical optimization 
* Light computational cost, fast learning

Cons:
* Mode collapse - same structure is repeatedly generated
  * Normalization techniques (e.g. spectral normalization) could help
* Fixed atom count

