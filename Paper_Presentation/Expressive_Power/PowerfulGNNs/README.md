# How Powerful are Graph Neural Networks?

## Experimental Results

**Dataset**

The target task is graph classification. Datasets are from two domains:
* 4 bioinformatics datasets: MUTAG, PTC, NCI1, PROTEINS
* 5 social network datasets
  
![Social network datasets details](fig/datasets.png)

**Training Set Performance**

![Main result of training set performance](fig/figure4.png)

Higher accuracy in training set refect better representational power for GNNs. 

Main results:
* GINs are able to almost perfectly fit all the training sets
* Explicit learning of <img src="https://render.githubusercontent.com/render/math?math=\epsilon"> yields no gain compared to fixing <img src="https://render.githubusercontent.com/render/math?math=\epsilon"> to 0
* GNNs with MLPs are better than GNNs with 1 layer perceptrons
* GNNs with sum aggregators are better than GNNs with mean/max pooling aggregators
* WL subtree kernel is the method with the ceiling performance across all methods

**Testing Set Performance**

![Main result of testing set performance](fig/table1.png)

The better accuracy on test set reflects better generalization capacity and demonstrates stronger expressive power. Main results:
* GIN-0 is the best or very close to the best on all 9 datasets
* GIN-0 is better than GIN-<img src="https://render.githubusercontent.com/render/math?math=\epsilon"> due to its simplicity
* Mean-based GNNs perform much worse than sum-based GNNs

## Pros and Cons

