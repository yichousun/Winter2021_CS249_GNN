# Graphite: Iterative Generative Modeling of Graphs


## Introduction
There are many data without labels in the real world. It is hard to unrealistic to label every data using human resource. Therefore, in many training tasks, augmented data is necessary to fulfil the data gap. Generative models can usually be really helpful in generating fake examples unsupervisedly from the original data. Some known generative models are Autoregressive models (e.g. GPT), Generative Adversarial Networks (GAN), and Variational Autoencoder (VAE). In this paper, the author continue exploring the original Variational Graph Autoencoder and make modifications on the decoding structure, which achieves the state of the art performance on various tasks including link prediction, density estimation, and semi-supervised node classification.


## Related Work

The following subsections are related work to this paper.

### Probabilistic Modeling
Graphite incorporates probabalistic modeling on graphs, which was first studied by (Erdos & Renyi, 1959), in which edges were formed with constant probability. Since then, better models have emerged such as Small-world model (Watts & Strogatz, 1998) or Barabasi-Albert models (Barabasi & Albert, 1999). However, these models do not use representation learning.

### Representation Learning
Graphite additionally has representation learning, which comes in three forms. The first is matrix factorization, like graph Laplacians, which do not scale well to large graphs. Second is random walk approaches, such as node2vec which incorporates skipgram. Lastly is the GNN approach, which Graphite uses. 

### Latent Variable Models
Previously studied are Bayesian models with deep neural nets (Hu et al., 2017; Wang et al., 2017), Adversarial generative approaches (Bojchevski et al. 2018; Li et al. 2018), and small-scale latent variable models (Jin et al., 2018; Samanta et al., 2018; Simonovsky & Komodakis, 2018). Each is not without its own problem: the Bayesian models are very restrictive and task-specific. Encoders cannot be used to acquire the latent variables in the Adversarial approach, and the the other latent-variable model approaches do not generalise well to large graphs. 

### Autoencoder
An autoencoder is a structure that aims to reconstruct the original input via transformation. There are many applications for the autoencoder (dimensionality reduction, denoising). However, normal autoencoder is not a generative model which cannot generate fake data. Instead of using a normal autoencoder, variational autoencoder which is a generative model is widely used to generate arbitrary data.

### Variational Autoencoder
Variational Autoencoder has a strong theoretical background in probabilistic graphical models. It tries to model the dependency between the latent variable z and the observed variable x. If the dependency or probabilistic of P(z|x) can be computed, we can sample data from the distribution directly without the need of retraining the network with new data. Another benefit of constructing the probabilistic model is that the model can generate new data from the distribution and therefore be served as a data augmentation technique for other tasks.

### Variational Graph Autoencoder
One of the closest work to this paper is the VGAE proposed by Thomas Kipf and Max Welling. It is an extension based on the VAE that uses graph data and Graph Convolutional Layer as the foundation block in the Autoencoder. The encoding is a two-layer GCN where the second layer has two different graph convolution layers modeling the mean and standard deriviation of the assumed Gaussian distribution. One major drawback of this model is that the decoder does not involve any learnable parameters. It is the inner product of the sampled latent representation **Z**. It leads to the solution of this paper which integrates the GCN architecture into the decoding stage.

## Solution
In this paper, the major contribution is in the decoding stage. The sampled latent representation **Z** is transformed using the following equation:
<img src="https://render.githubusercontent.com/render/math?math=\hat{\mathbf{A}} = \frac{\mathbf{Z}\mathbf{Z}^{T}}{||\mathbf{Z}||^{2}} %2B \mathbf{1}\mathbf{1}^{T}">

The intermediate adjacency matrix <img src="https://render.githubusercontent.com/render/math?math=\hat{\mathbf{A}}"> can then be used in message passing to obtain a meaningful final representation <img src="https://render.githubusercontent.com/render/math?math=\mathbf{Z}^{*}"> before going into the inner product decoder. The final representation <img src="https://render.githubusercontent.com/render/math?math=\mathbf{Z}^{*}"> can be formulated using the following formula:
<img src="https://render.githubusercontent.com/render/math?math=\mathbf{Z}^{*} = GNN_{\theta}(\hat{\mathbf{A}}, [\mathbf{Z}|\mathbf{X}])">

By adopting the above representation, the reconstructed adjacency matrix will be refined iteratively rather than deterministic compared to the VGAE. The experimental results also shows that this method will outperform VGAE and achieve the state of the art results in various tasks.

## Experiment Results
Two models are evaluated, Graphite-VAE and Graphite-AE. First, the model is evaluated in reconstruction and density estimation. The benchmark algorithms are GAE and VGAE. Graphite outperforms these models in mean reconstruction error. Next, the model is evaluated for link prediction. The benchmark datasets are Cora, Citeseer, and Pubmed. Graphite-VAE has the best overall performance compared to the benchmarks, and Graphite-AE performs well too. Next, the latent feature vectors are visualized using 2D t-SNE projection. The data clusters according to category labels, even though the training is unsupervised. This shows that the latent feature vectors are a valuable representation of the data. Finally, Graphite is evaluated on semi-supervised node classification. The benchmark algorithm is GCN. For node classification, Graphite builds on GCN by augmenting GCN with the Graphite objective and training for both objective functions. The hybrid Graphite approach outperforms GCN. 

## Conclusion
Graphite differs from VGAE/GAE by having learning parameters in decoding, to have a better latent variable model, and as such it is able to outperform existing methods. These latent features can be decoded to have minimal reconstruction loss due to the theory behind the update equations. While graphite was only tested for regular graphs (e.g. no time-varying graphs, no domain knowledge incorporated), it is still a novel approach which outperforms its predecessors. Future work may look to expand the model to encapsulate graphs with different structure, or to use a different GNN instead of graph conv net.

## Pros and Cons
Graphite is scalable to very large graphs, unlike its counterparts. It also outperforms most existing methods on link prediction, density estimation, and semi-supervised node classification.  However, Graphite still does not solve the problem of permutation invariance.
