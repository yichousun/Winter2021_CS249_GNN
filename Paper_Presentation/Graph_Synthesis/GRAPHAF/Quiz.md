T/F: For autoregressive conditional probabilities parameterized by Gaussians, the mean and standard deviation of the latent distribution are only a function of the current sampled output

True

False

SC: Why is GRAPHAF training efficient?

a) The Jacobian of the inverse of normalizing flow is sparse

b) GRAPHAF utilizes transformers for graph generation which is more parallelizable than RNNs

c) Iterations of the graph generation can be trained independently because masking satisfies the autoregressive property

SC: How does GRAPHAF handle valency constraints in the generation process?

a) Use the constraint as a term in the loss function and optimize using gradient descent

b) At every step in sequential generation, check if the newly generated molecule obeys the valency constraint

c) After the molecule has been generated, use a pruning algorithm to remove excess edges
