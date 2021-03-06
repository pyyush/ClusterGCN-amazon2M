# Cluster-GCN in PyTorch
[![Arxiv](https://img.shields.io/badge/ArXiv-1905.07953-orange.svg?color=blue&style=plastic)](https://arxiv.org/abs/1905.07953)
[![Download](https://img.shields.io/badge/Download-amazon2M-brightgreen.svg?color=black&style=plastic)](https://drive.google.com/drive/folders/1Tfn-yABlW5JheyYItyRyrMGtmQdYN7wm?usp=sharing)
> Cluster-GCN: An Efficient Algorithm for Training Deep and Large Graph Convolutional Networks
> Wei-Lin Chiang, Xuanqing Liu, Si Si, Yang Li, Samy Bengio, Cho-Jui Hsieh.
> KDD, 2019.
> [[Paper]](https://arxiv.org/abs/1905.07953)
Raw data files used to curate this dataset can be downloaded from http://manikvarma.org/downloads/XC/XMLRepository.html while the processed data files used in this implementation can be downloaded by clicking on the above Download amazon2M badge.

## GraphConv Layer module usage
```
from layers import GraphConv
gconv = GraphConv(in_features: int, out_features: int)
out = gconv(A: torch.sparse.Floattensor, X: torch.FloatTensor) # out.shape(N, out_features)
```
where, N = number of nodes in the graph \
       F = number of features per node \
       in_features = number of input features in X, \
       out_features = number of output features, \
       X  = a dense FloatTensor containing input features, \
       A  = a sparse FloatTensor representing the graph adjacency matrix created as follows
``` 
i = torch.LongTensor(indices)
v = torch.FloatTensor(values)
A = torch.sparse.FloatTensor(i.t(), v, shape)
```


## Requirements:
* install the clustering toolkit metis and other required Python packages.
```
1) Download metis-5.1.0.tar.gz from http://glaros.dtc.umn.edu/gkhome/metis/metis/download and unpack it
2) cd metis-5.1.0
3) make config shared=1 prefix=~/.local/
4) make install
5) export METIS_DLL=~/.local/lib/libmetis.so
6) pip install -r requirements.txt
```
## Usage:
* Run the below shell script to perform experiments on amazon2M dataset.
```
./amazon2M.sh
tensorboard --logdir=runs --bind_all (optional to visualize training)

NOTE: The Scipt assumes that the data files are stored in the following structure. 
./datasets/amazon2M/amazon2M-{G.json, feats.npy, class_map.json, id_map.json}
```
## Results:
* Test F1 **0.8880** (vs Cluster-GCN paper - 0.9041)
* Training Loss **0.3096**
<figure>
  <img src="W&B Chart 6_16_2020, 5_13_19 PM.png"/>
</figure>

* Training Accuracy **0.9021**
<figure>
  <img src="W&B Chart 6_16_2020, 5_13_29 PM.png"/>
</figure>
