# Learning Continuous System Dynamics from Irregularly-Sampled Partial Observations

The codes are avaiable in [this repo](https://github.com/ZijieH/LG-ODE).

## Introduction

Many real-world systems, such as moving planets, can be considered as multi-agent dynamic systems, where objects interact with each other and co-evolve along with the time. Such dynamics is usually difficult to capture, and understanding and predicting the dynamics based on observed trajectories of objects become a critical research problem in many domains. Most existing algorithms, however, assume the observations are regularly sampled and all the objects can be fully observed at each sampling time, which is impractical for many applications. In this paper, we propose to learn system dynamics from irregularly-sampled partial observations with underlying graph structure for the first time.

## Related Work

Existing works have developed various neural-based physical simulators that learn the system dynamics from data. Most existing approaches restrict themselves to learn a fixed-step state transition function that takes the system state at time t as input to predict the state at time t + 1. However, they can not be applied to the scenarios where system observations are irregularly sampled. Our model handles such issue by combining a neural ODE  to model continuous system dynamics and a temporal-aware graph neural network followed by a temporal self-attention module to estimate system initial states. Another issue lies in that they need to observe the full states of a system; but in reality, system states are often partially observed where number and set of observable objects vary over time. A recent work tackled this issue where system is partially observed but observations are regularly sampled by learning the dynamics over a latent global representation for the system, which is for example an average over the sets of object states. However it cannot directly learn the dynamic state for each object. In our work, we design a dynamic model that explicitly operates on the latent dynamic representations over each object. This allows us to define object-centric dynamic.


## Solution

We propose to learn the dynamic nature of a system using neural ordinary differential equations, where we parameterize ODE function with a GNN to capture continuous interaction among agents. In this way, obsevations (X) are now used for supervision signals to adjust the latent trajectories, thus can be irregular not temporarily aligned. We infer the initial states for each agent simultaneously using variational autoencoder, as agents are highly-coupled and related in multi-agent dynamic systems.



The encoder comprises three parts: temporal graph construction; dynamic node representation learning and temporal self-attention. The key idea is to introduce cross-temporal edges among observations and combine graph neural network with learnable temporal encoding to generate temporal and structural-aware node representations.


## Experimental results

LG-ODE is evaluated on two simulated datasets (charged particles and particles connected by springs) and one real dataset (CMU Motion Capture Data).  We conduct experiment on both interpolation task and extrapolation task with different observation ratios.  Overall, LG-ODE consistently outperforms other baselines under different settings. Notably, the performance gap between LG-ODE and other methods increases when the observation percentage gets smaller, which indicates the effectiveness of LG-ODE on sparse data.

## Major conclusions

We propose LG-ODE for learning continuous multi-agent system dynamics from irregularly-sampled partial observations. We model system dynamics through a neural ordinary differential equation and draw the latent initial states for each object simultaneously through a novel encoder that is able to capture the interaction among objects. The joint learning of initial states not only captures interaction among objects but can benefit the learning when an object only has few observations. We achieve state-of-the-art performance in both interpolating missing values and extrapolating future trajectories. 


## Cons

An limitation of current model is that we assume the underlying interaction graph is fixed over time. In the future, we plan to learn the system dynamics when the underlying interaction graph is evolving.