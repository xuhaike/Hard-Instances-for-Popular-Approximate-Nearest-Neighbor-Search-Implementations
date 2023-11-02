This repository contains the implementations of the hard instances designed in our paper [Worst-case Performance of Popular Approximate Nearest Neighbor Search Implementations: Guarantees and Limitations](https://arxiv.org/abs/2310.19126) to appear in NeurIPS 2023

# Data files for the two hard instances we present in our paper

We provide the three data sets we construct for DiskANN, NSG, and HNSW algorithms described in our paper (Figure 2 and 4), for  $n=10^6$. The data sets for NSG and HNSW only differ in their format. These three datasets are in different binary formats compatible with their respective implementations （[DiskANN code link](https://github.com/microsoft/DiskANN), [NSG code link](https://github.com/ZJULearning/nsg), [HNSW code link](https://github.com/nmslib/hnswlib)）

Note that some of the implementations require that the data dimension is a multiple of $8$, so for consistency, we complement the remaining $6$ dimensions with $0$ for the three datasets we are submitting. In what follows, we have dimension $d=8$. Our query file only contains one query, and we search for the top-5 nearest neighbors.

## DiskANN 
- Point set: test_diskann_1e6_learn.fbin
- Query point set: test_diskann_1e6_query.fbin
- Groundtruth: test_diskann_1e6_groundtruth.fbin

For point sets, the first $4$ bytes represent the number of points $n$ as an integer (for query point set, $n=1$). The next $4$ bytes represent the dimension of data as an integer $d$ ($d=8$). The following $n*d*4$ bytes contain the content of the point set, where each dimension of a point is represented by $4$ bytes (float32).

For groundtruth file, the first $4$ bytes represent the number of queries $n$ as an integer ($n=1$). The next $4$ bytes represent the number of nearest neighbors it contains $k$ ($k=5$).
The next $n*k*4$ bytes, where $n=1$ is the number of queries, $k=5$ is the number of nearest neighbors we are asking for. Each $4$ bytes represent the id of a top-k nearest neighbor.

## NSG
- Point set: test_nsg_1e6_learn.fvecs
- Query point set: test_nsg_1e6_query.fvecs
- Groundtruth: test_nsg_1e6_groundtruth.ivecs

Each .fvecs point set contains $n*(d+1)*4$ bytes representing $n$ points ($n=1$ for the query point set), where for each $(d+1)*4$ bytes, the first $4$ bytes represent the dimension $d$ ($d=8$) as an integer and the next $d*4$ bytes represent the point's $d$ dimensions using float32.

Groundtruth file is stored in .ivecs format, which contains $n*(k+1)*4$ bytes representing $n$ queries ($n=1$, $k=5$ for our case). For each chunk of $(k+1)*4$ bytes, the first $4$ bytes is the number of nearest neighbors it contains $k$ ($k=5$) as an integer, and the next $k*4$ bytes represent the ids for $k$ nearest neighbors in integer format.

## HNSW
- Point set: test_hnsw_1e6_learn.pickle
- Query point set: test_hnsw_1e6_query.pickle
- Groundtruth: test_hnsw_1e6_groundtruth.pickle

Point set is a numpy array of dimensions $n*d$ ($d=8$) containing $d$ dimensions for $n$ points. 
query point set is a numpy array of dimensions $n*d$ ($n=1$, $d=8$) containing $d$ dimensions for $n$ query points.
groundtruth is a numpy array of dimension $n*k$ ($n=1$, $k=5$) containing the id of $k$ nearest neighbor for each query.
All three .pickle files are stored by pickle.dump() in python.

## Citation
Please cite our paper if it is useful in your work.
```
@misc{indyk2023worstcase,
      title={Worst-case Performance of Popular Approximate Nearest Neighbor Search Implementations: Guarantees and Limitations}, 
      author={Piotr Indyk and Haike Xu},
      year={2023},
      eprint={2310.19126},
      archivePrefix={arXiv},
      primaryClass={cs.DS}
}
```