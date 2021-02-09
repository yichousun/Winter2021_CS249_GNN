# HOPPITY: LEARNING GRAPH TRANSFORMATIONS TO DETECT AND FIX BUGS IN PROGRAMS

## Introduction

It's hard for code to be free from bugs, therefore if we can detect bugs automatically during the development procedure, the burden of developers will be reduced a lot. This paper aims to find a method to detect bugs in Javascript language automatically.

Repairing Javascript code presents a unique challenge as bugs manifest in diverse forms due to unusual language features and the lack of tooling support. Therefore, the primary goal of their approach is generality since it needs to be effective against a board spectrum of programming errors. To be more specifically, this paper presents an end-to-end approach including localizing bugs, predicting the types of fixes, and generating patches.



## Solution

**Hypothesis:** A code snippet is buggy if it deviates from common practices -- Data driven training

#### Part 1: Embedding

The first part of the solution is to represent the graph. The paper firstly transform the program into  AST (Abstract Syntax Tree). Then, based on AST, it uses *GIN (Graph Isomorphism Network)* to embed the graph. There are three types of embedding: graph embedding, AT embedding and Value embedding.

#### Part 2: Controller

After we get the representation of the graph *(the embedding)*, we can now start to edit the program and fix bugs. In order to do that, we need a "controller", which is another embedding that we will use to work with the above embeddings together in a LSTM model. 

There are multiple steps during the bug fixing procedure. In each step, we try to use the graph and controller together to determine a bug and then fix it. There are five edit action: add, delete, replace value, replace type and No-operation. To be more specifically, in each step, it will firstly locate the bug and decide which action to take. Then generate a new value (if necessary) and a new type (if necessary). Finally it will complete the links for AST.



## Related Work

The existing works can be put into two categories: logical, rule-based technique and statistical, data-driven technique.

For the rule-based technique, it uses manually written rules capturing undesirable code patterns and scans the entire codebase for these classes of bugs. The drawback is that it is not able to detect a lot of bugs, for example the usage of method names. 

For data-driven technique, it learns to detect abnormal code from a large code corpus using deep neural networks. For example, Allamanis et al. (2018) used GNN to predict correct variable name given a buggy location. Vasic et al. (2019) developed pointer network on top of RNN. However, existing method are limited in generality because they target error patterns in specific codebaes or they target specific bug types. Besides that, they all need the bug location as input.



## Experimental Results


#### Data Collection
Authors automatically collected data from Github using heuristics: a commit with a smaller number of AST differences is more likely to be a bug fix.

#### Results
The authors first use a random baseline to show that the entire search space is large and Hoppity effectively outperforms it.

Compared to previous works, the model has an advantage in most cases. Especially, compared to seq2seq methods (i.e. treating bug fixing as a translation task), Hoppity holds a large advantage. In addition, previous methods require the bug location as input while Hoppity can identify the bug and perform fix in the same time.


## Major Conclusion (Pros) and Future Work (Cons)

#### Major Conclusion (Pros)

- A single model to deal with a wide range of bugs
- Fixing JS bugs is challenging due to anti-human syntactic designs
- Can handle complex bugs: adding/removing statements from a program
- End-to-End in the sense that:
  - propose bug location
  - propose fixes
  - implement fixes

#### Future Work (Cons)

- Bugs spanning multiple files
- Deploy in IDE
- Other languages
- The accuracy can be improved -- Now, correctly predicts 9490 out of 36361 code changes in real programs on Github
