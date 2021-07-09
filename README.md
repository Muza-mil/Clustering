# Introduction to the project

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

![Alt text](../-/blob/master/steps.jpg?raw=true "Implementation Steps")

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
1. Run the `clustering2.py` file .Once that's gets done Dendogram png file will be available in TEMP_TEST folder.

### Nice to know
All the routines are well documented in case you want to see the work flow inside pipelines. 

