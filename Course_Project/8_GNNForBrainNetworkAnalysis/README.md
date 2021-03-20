# GNN for Brain Network Analysis

This is the submission folder for Team 8

The link to repo - https://github.com/NShah19/CS249_GNN The slides for the presentation are in this folder while all other documentation is currently in the repository.

The task table is below:
A: Nilay Shah
B: Xuan Lin 
C: Nima Zaghari
D: Daisy Zheng
E: Everyone

| Task                   | People        |
| -------------          | ------------- |
| Slides                 | E             |
| HPC data processing    | B             |      
| ABIDE data processing  | D             |
| Optuna Framework       | A             |
| Optuna Visualization   | D             |
| Report: Abstract       | A, C          |
| Report: Intro          | A             |
| Report: Problem        | B             |
| Report: Related Work   | A, B, C       |
| Report: Methods        | B             |
| Report: Exp. Design    | A, C, D       |
| Report: Evaluation     | D             |
| Report: Discussion     | D             |


### Files: 

main.py : runs brain network classification model

optimize.py : runs optuna study for hyperparameter optimization

AbideData.py : Abide Dataset class

process_data.py : used for preprocessing the ABIDE data 

### Setup:
The following requirements must be installed before running the model:
```bash
pip install -r requirements.txt
pip install torch==1.8.0+cu111 torchvision==0.9.0+cu111 torchaudio===0.8.0 -f https://download.pytorch.org/whl/torch_stable.html
pip install torch-scatter -f https://pytorch-geometric.com/whl/torch-1.8.0+cu111.html
pip install torch-sparse -f https://pytorch-geometric.com/whl/torch-1.8.0+cu111.html
pip install torch-cluster -f https://pytorch-geometric.com/whl/torch-1.8.0+cu111.html
pip install torch-spline-conv -f https://pytorch-geometric.com/whl/torch-1.8.0+cu111.html
pip install torch-geometric
```
### Running main model to classify brain networks:
```bash
python main.py --dataroot ${YOUR_PROCCESSED_DATA_DIR} --dataset {abide | hcp}
```
Note: additional command line parameters can be specified to set hyperparameter values

### Performing Hyperparameter Optimization:
```bash
python optimize.py --dataroot ${YOUR_PROCCESSED_DATA_DIR} --dataset{abide | hcp}
```
