<!--
 * @Author: Zhenkun Shi
 * @Date: 2022-04-19 11:21:15
 * @LastEditors: Zhenkun Shi
 * @LastEditTime: 2023-10-06 11:52:41
 * @FilePath: /ECRECer/README.md
 * @Description: 
 * 
 * Copyright (c) 2022 by tibd, All Rights Reserved. 
-->

# DMLF: Enzyme Commission Number Predicting and Benchmarking with Multi-agent Dual-core Learning

This repo contains source codes for a EC prediction tool namely ECRECer, which is an implementation  of our paper: 「Enzyme Commission Number Prediction and Benchmarking with Hierarchical Dual-core Multitask Learning Framework」

Detailed information about the framework can be found in our paper

```bash
1. Zhenkun Shi, Qianqian Yuan, Ruoyu Wang, Hoaran Li, Xiaoping Liao*, Hongwu Ma* (2022). ECRECer: Enzyme Commission Number Recommendation and Benchmarking based on Multiagent Dual-core Learning. arXiv preprint arXiv:2202.03632.

2. Zhenkun Shi, Rui Deng, Qianqian Yuan, Zhitao Mao, Ruoyu Wang, Haoran Li, Xiaoping Liao*, Hongwu Ma* (2023). Enzyme Commission Number Prediction and Benchmarking with Hierarchical Dual-core Multitask Learning Framework. Research.
```


## Usage
### For simply use our tools to predict EC numbers, please visit ECRECEer websiet at https://ecrecer.biodesign.ac.cn


### For users who want to run ECRECer locally, please follow the steps below:
We provide docker image and singularity image for users to run ECRECer locally.

> <b>Docker image</b>: 

```bash
# 1. pull ecrecer docker image
docker pull kingstdio/ecrecer

# 2. run ecrecer docker image
# gpu version:
sudo docker run -it -d --gpus all  --name ecrecer -v ~/:/home/ kingstdio/ecrecer #~/ is your fasta file folder
# cpu version:
sudo docker run -it -d --name ecrecer -v ~/:/home/ kingstdio/ecrecer  #~/ is your fasta file folder

# 3. run ECRECer prediction 

sudo docker exec ecrecer python /ecrecer/production.py -i /home/input_fasta_file.fasta -o /home/output_tsv_file.tsv -mode h -topk 10

#-topk: top k predicted EC numbers
#-mode p: prediction mode, predict EC numbers only
#-mode r: recommendation mode, recommend EC numbers with predicted probabilities, the higher the better
#-mode h: hybird mode, use prediction, recommendation and sequence alignment methods

```

> <b>Singularity image</b>: 

```bash
# 1. pull ecrecer singularity image

# Image ~= 11GB, may take a while to download
wget -c https://tibd-public-datasets.s3.us-east-1.amazonaws.com/ecrecer/sifimages/ecrecer.sif

# 2. run ecrecer singularity image
# gpu version:
singularity run --nv ecrecer.sif python /ecrecer/production.py -i input_fasta_file.fasta -o output_tsv_file.tsv -mode h -topk 10
# cpu version:
singularity run ecrecer.sif python /ecrecer/production.py -i input_fasta_file.fasta -o output_tsv_file.tsv -mode h -topk 10

#-topk: top k predicted EC numbers
#-mode p: prediction mode, predict EC numbers only
#-mode r: recommendation mode, recommend EC numbers with predicted probabilities, the higher the better
#-mode h: hybird mode, use prediction, recommendation and sequence alignment methods

```




# To re-implement our experiments or offline use, pls use read the details below:

# Prerequisites

+ Python >= 3.6
+ Sklearn
+ Xgboost
+ conda
+ jupyter lab
+ ...

> Create conda env use [env.yaml](./env.yaml)

```python
git clone git@github.com:kingstdio/ECRECer.git
conda env create -f env.yaml
```

# Preprocessing

Download and prepare the data set use the.

> [prepare_task_dataset.ipynb](./prepare_task_dataset.ipynb)

Or directly download the preprocessed data from [aws public dataset](https://tibd-public-datasets.s3.amazonaws.com/ecrecer/ecrecer_datasets.zip) and put it in the rootfolder/data/datasets/

<!-- # Step by step benchmarking

### Task 1: Enzyme or None-Enzyme Prediction

> [./tasks/task1.ipynb](./task1.ipynb)

### Task 2: Polyfunctional Enzyme Prediction

> [./tasks/task2.ipynb](./task2.ipynb)

### Task 3: EC Number Prediction

> [./tasks/task3.ipynb](./task3.ipynb) -->

# High throughput benchmarking

# Train

```python
python benchmark_train.py
```

# Test

```python
python benchmark_test.py
```

# Evaluation

```python
python benchmark_evaluation.py
```

# Production

```python
python production.py -i input_fasta_file -o output_tsv_file -mode [p|r] -topk 5
```

# Citations

If you find these methods valuable for your research, we kindly request that you reference the pertinent paper:

```bib
@article{shi2023enzyme,
  title={Enzyme Commission Number Prediction and Benchmarking with Hierarchical Dual-core Multitask Learning Framework},
  author={Shi, Zhenkun and Deng, Rui and Yuan, Qianqian and Mao, Zhitao and Wang, Ruoyu and Li, Haoran and Liao, Xiaoping and Ma, Hongwu},
  journal={Research},
  year={2023},
  publisher={AAAS}
}
```

## Stargazers over time

[![Stargazers over time](https://starchart.cc/kingstdio/ECRECer.svg)](https://github.com/kingstdio/ECRECer/)
