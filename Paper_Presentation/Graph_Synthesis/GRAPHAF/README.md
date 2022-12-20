# GRAPHAF: a Flow-based Autoregressive Model for Molecular Graph Generation

By: Chence Shi, Minkai Xu, Zhaocheng Zhu, Weinan Zhang, Ming Zhang, Jian Tang

# Introduction

The success of deep generative models in drug discovery is measures by two metrics. Drug-likeness measures how much a proposed molecular structure looks like a real drug and property optimization is a measure of how much a proposed molecular structure displays desired properties. GRAPHAF proposes a framework based on autoregressive flow to ensure the validity of a drug while also using reinforcement learning to generate structures that exhibit desired properties. In addition to these metrics, GRAPHAF is shown to have a significant speedup in training time over current state of the art methods.

# Related Work

Previous papers have proposed a variety of different solutions, each with their own advantages, to the drug discovery problem. Generative models such as Variational Autoencoders and Generative Adversarial Networks have been translated into the graph domain and provide a straightforward way of generating structures in a way that maximizes the likelihood that the learned distribution matches the desired distribution of drugs. Autoregressive models such as MolecularRNN are iterative in nature and allow for generated structures to be checked for validity constraints at each step. Reinforcement learning approaches like Graph Convolutional Policy Network directly optimizes for desired properties in the proposed structure.

# Method

GRAPHAF aims to create a framework that can make use of the advantages in each of the above methods. The result is a flow based autoregressive model fine tuned with a reinforcement learning. 

## Normalizing Flow

Like VAEs and GANs, Normalizing Flow belongs to a family of generative models that learn a mapping from one distribution to another. This means that flow based models can be used to sample and generate new data from a latent dsitribution.

## Autoregressive Models

Autoregressive models are models where the output at a certain step is only a function of outputs at previous steps. Like MolecularRNN, this means that the graph generation procedure can be formulated as a sequential generation task where at each step, a new component is added. Due to the autoregressive property, this new addition is only a function of the previous iterations of the graph. This allows for validity checks to be places at each step in the procedure.

## Reinforcment Learning

Since the graph generation procedure is formulated in a sequential manner, reinforcment learning can be leveraged to select the best addition to make to the graph at each time step. Therefore, the incorporation of a Graph Convolutional Policy Network means that the generation procedure makes additions that ultimately optimize the for a desired property. 

The GRAPHAF framework combines the advantages of the three techniques above in the following way. The autoregressive property to converts the graph generation problem into a sequential generation process. At each step in the process, normalizing flows are used to model a latent distribution that can be sampled and converted into an addition on the graph. The sequential process also has the advantage of allowing for validity checks to occur after every sample. This whole process is optimized by a Graph Convolutional Policy Network so that the selected samples maximizes a desired property of the resulting graph.

# Experiments

Network structure:
The R-GCN is implemented with 3 layers, and the embedding dimension is set as 128. The max graph size is set as 48 empirically. For density modeling, we train our model for 10 epochs with a batch size of 32 and a learning rate of 0.001. For property optimization, we perform a grid search on the hyperparameters and select the best setting according to the chemical scoring performance. We use Adam to optimize our model.

Evaluation Tasks. We conduct experiments by comparing with the state-of-the-art approaches on three standard tasks. 
Density Modeling and Generation evaluates the model’s capacity to learn the data distribution and generate realistic and diverse molecules. 
Property Optimization concentrates on generating novel molecules with optimized chemical properties. 
Constrained Property Optimization aims at modifying the given molecule to improve desired properties while satisfying a similarity constraint.

Link to a Google colab script that runs the results:
https://colab.research.google.com/drive/1Ud_37N0yTMLaYhaax-Om-2HOnKNDlwnl?usp=sharing

