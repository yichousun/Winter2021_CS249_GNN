# [Learning to Simulate Complex Physics with Graph Networks](https://arxiv.org/abs/2002.09405)
Authors: Alvaro Sanchez-Gonzalez, Jonathan Godwin, Tobias Pfaff, Rex Ying, Jure Leskovec, Peter W. Battaglia, ICML 2020.  
Presenters: **Yuanhao Xiong**, **Xiangning Chen**, **Li-Cheng Lan**
Codes: (https://github.com/deepmind/deepmind-research/tree/master/learning_to_simulate)
Video site: (https://sites.google.com/corp/view/learning-to-simulate)

## Introduction
Realistic simulators of complex physics are invaluable to many scientific and engineering disciplines. However, building a high-quality simulator is faced with significant difficulties, such as substantial computational resources, lack of knowledge of underlying physics and parameters, and the like. An attractive alternative to traditional simulators is to use machine learning to train simulators directly from observed data. In this paper, a powerful machine learning framework forlearning to simulate complex systems from data — “GraphNetwork-based Simulators” (GNS) is presented. Experiments have shown that GNS can learn to accurately simulate a wide range of physical systems, generalized well to much larger systems and longer time scales than those on which it was trained.


## Related works



## Method
![GNS framework](framework.pdf)


## Experimental Results
The experiments are conducted on three domains: n-body problem, balls bouncing in a box and n-mass string. And IN is evaluated on two prediction tasks: 1) predict velocity at the next time step, 2) estimate potential energy at the current time step. And it is compared with three other models: 1) constant velocity model that outputs the input velocity, 2) baseline MLP model that takes the flattened input data, 3) dynamics-only IN that eliminates the relation model.

As for the next-step velocity prediction task, IN showcases orders of lower MSE test error compared to other baseline models. And it also generalizes well to systems with fewer and greater number of objects. The model trained on systems with larger number of objects also perform better than models trained on less complex system.

As for the abstract value estimation task (potential energy), IN is also much accurate in potential energy prediction than all other baselines. It presumably learns the gravitational and spring potential energy functions, applies them to the relations ihe domain, and combines the energy estimation results.


## Major Conclusions
- IN shows strong ability to learn accurate physical simulations and can automatically generalize their training to novel contexts.
- It can roll out thousands of realistic future state predictions, even when trained only on single-step predictions.
- IN present the first general-purpose learnable physics engine that can scale up to real-world problems.
- IN provides a powerful general framework for reasoning about object and relations in complex real-world domains.


## Pros and Cons
- Pros
    - First general-purpose physical engine
    - Generalize their training to novel systems with different numbers and configurations of objects and relations
    - Could also learn to infer abstract properties of physical systems, such as potential energy
- Cons
    - If to handle very large systems with many interactions, then we need to reduce computation through methods like culling interaction computations with negligible effects
    - Only support binary relation
        - How to extend it to n-th order relations by combining n senders in each bk.
        - The interactions could even have variable order, where each bk includes all sender objects that interact with a receiver, but would require a f_R than can handle variable-length inputs.
    - Take the graph as input
        - Objects and relations are known
        - Prepend a perceptual front-end that can infer the graph from raw observations

