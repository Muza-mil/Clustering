<h1 align="center">On generating cluster hierarchies based on Mol2Vec embeddings of compounds from large databases</h1>

# Introduction to the project

Generation of cluster hierarchies using structured large database from `PubChem` by embedding of molecular compounds into 300 dimentional stochastic vectors with Mol2Vec, a machine learning approach. Research and developement for accelerating similarity measuremnt of different compounds by clustering using agglomerative algorithm. Also computation of dendrogram (for the representation of cluster hierarchies of compounds), medoid, bounding box, variance of each sub-clusters. In addition benchmark it by performing similarity search a). Used naive algorithm 
b). Used Binary tree.   

## Environment Setup:
(Preferred : OS: ubuntu ,IDE: Pycharm )
### For Ubuntu :
1. Open Project in pycharm
2. Create new virtual environment or you can use the venv folder inside the project
3. Install all the requirements for the code (Pycharm will prompt you what to install)
4. Install addition requirements: \
pip install git+https://github.com/samoturk/mol2vec \
sudo apt-get install python3-rdkit librdkit1 rdkit-data \
virtualenv venv --system-site-packages \
sudo apt-get install build-essential \
pip3 install Cython \
pip install -Iv gensim==3.8.2 \
pip install launchpadlib \
PS.: You may need some additional libraries.

### For windows:

1. Open Project in pycharm
2. Create new conda environment using Pycharm (File>Settings> Project> Python Interpreter)
3. Install all the requirements for the code (Pycharm will prompt you what to install)
4. Install addition requirements: \
( Anaconda navigator > Environment > Your Project Environment) \
Conda install -c conda-forge rdkit \
Conda install pip \
pip install git+https://github.com/samoturk/mol2vec \
pip install Cython \
pip install -Iv gensim==3.8.2 \
pip install launchpadlib \
PS.: You may need some additional libraries.


## Pubchem Compounds Clustering `CODE BASE`
### Subtasks
1. Perform embedding of all about 111 million compounds from PubChem database 
2. Computer dendrogram from hierarchical clustering
3. Compute for each (sub)cluster the medoid compound
4. Compute for each (sub)cluster the variance (increase...)

5. Runtime experiments:
   Run one experiment for a query compound q brute-force against all compounds in sequential order
   Run one experiment for q using the hierarchy with medoids and variance


![Implementation Steps](../-/blob/master/steps.jpg?raw=true "Implementation Steps")

### Task 1
`Embedding of Compounds` \
\
For task 1 the workflows is as mentioned below:
Note : Download all the compound files from the PubChem database and extract them to SDF_BATCHES folder.
1. Run the `BATCH SPLITTING ROUTINE` from `main.py` file .Once that gets done SDF files will be visible in SDF_PER_COMPOUND folder.
2. Run the `MOL2VEC FEATURIZATION ROUTINE` from `main.py` file .Once that's gets done CSVs files will be available in CSVS folder.
3. Run the `MOL2VEC VECTORIZATION ROUTINE` from `main.py` file .Once that's gets done CSV file will be available in VECTORIZED_CSV folder.

### Task 2
`Dendogram Generation` \
\
For task 2 the workflows is as mentioned below:
1. Run the `generate_cluster()` from `clustering2.py` file .Once that's gets Dendogram image.

### Task 3
`Computation of medoid compound` \
For task 3, we devide this task into 4 subtask.
1. `Cut the dendrogram and extract clusters` \
   1.1 `store_cid_indexId()` use to maintain link between index and copmpound id, linkageMatrix provide us index of dataset instead of cpompound id. \
   1.2 `compute_a_helper_to_genarate_tree(linkageMatrix,no_of_leaves)` from `clustering2.py` file. Here we use linkageMatrix,no_of_leaves info from task 2. This function provide a dictionary of cluster's alighnmet which help later to construct tree. \
   1.3 `cut_dendrogram_in_joining_distance(linkageMatrix,no_of_leaves)` from  `clustering2.py` file. To extract each clusters. \
2. `Find medoid for each cluster` \
   2.1 `get_medoids_from_clusters()` from `clustering2.py` file. here dict_clusters is a dictionary of cluster id -> [medoid,cluster items,parent] \
   2.2 `store_medoid_list()` store cluster dictionary into a pickle file. this require for variance computation. \
3. `Construct a tree using medoid` \
   3.1 `bTree.ipynb` file contain data structure for tree construction.  \
   3.2 `insert_cluster_into_tree()` use to construct tree using cluster data from dictionary. \
   3.3 `store_tree()` use to store medoid tree into a pickle file for future searching. \
4. `Auxilary functions to retrive vectors for corresponding compound id and vice versa` \
   4.1 `create_dict_cid_vect()` from main.py to generate cid -> vectors dictionary. \
   4.2 `cid2vect()` from `extract_info.ipynb` use to retrive 300 vectors for corresponding cid \
   4.3 `vect2cid()` from `extract_info.ipynb` use to retrive cid for corresponding 300 vectors. \

### Task 4
`A . Computation of median absolute deviation (MAD)` \
\
For the computation of MAD:
You are required to have cluster with medoid as an input which can be acquired by loading a dictionary named
`medoid_cluster_dict.pkl` from the repo and yeild all the cluster with their medoids.

*) Run the `MAD(cluster, medoid)` in `variance.py` to get median absolute value.

`B . Computation of Bounding Box` \
\
For the computation of Bounding Box:
You are required to have a cluster of compounds as an input with upper and lower bounds of each 300 dimentional
compound vector in the cluster.

*) Run the `get_bbox(cluster)` in `variance.py` to get a bounding box for relevant cluster.

`C . Creating dictionary` \
\
For the creation of dictionary:
Can be used to searching new query compound having information of bounding box and MAD for each specific cluster .

*) Run the `compute_variance(medoid_list)` in `variance.py` to create a dictionary with 
   `[key -> clusterID: value -> [Bounding box, MAD value]]`.


### Nice to know
All the routines are well documented in case you want to see the work flow inside pipelines. 

