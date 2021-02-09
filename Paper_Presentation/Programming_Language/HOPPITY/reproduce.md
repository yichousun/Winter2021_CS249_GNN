## Reproduce the Results

We follow the author's released code to reproduce their results https://github.com/AI-nstein/hoppity. 

Due to several reasons, we find it impractical to reproduce it on Colab or provide a demo:

1. Large dataset size. 
The dataset needed to run the code takes more than 34GB of disk space, which exceeds the limit of Colab. In addition, as Colab may drop connection and the data will be lost, reconnecting means re-downloading and unpacking the data, which is very time consuming.

2. Slow inference speed.
Even on our local machine with GPUs, inference takes 6 seconds per example. Given there are more than 30K examples to evaluate, finishing the inference simply takes too long.

3. Length code preprocess and no demo provided.
The authors do not provide a demo rather only provide code to evaluate the model on a given dataset. Creating a demo on arbitrary inputs is hard, as it involves processing the input code into AST trees (which involves complicated sub-modules) and then conduct inference.

However, we are able to reproduce the results on our local machine (please see our slides).

#### Online Demo

The authors also provide an online demo (not open-sourced yet) that is free to try (https://hoppity.cis.upenn.edu/demo).
