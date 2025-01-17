# COPULA-SHIRLEY
Implementation for the COPULA-SHIRLEY framework for differerentially-private synthetic data generation. This implementation is used on the following paper:

Gambs, S., Ladouceur, F., Laurent, A. and Roy-Gaumond, A., 2021. Growing synthetic data through differentially-private vine copulas. Proceedings on Privacy Enhancing Technologies, 3, pp.122-141. https://www.petsymposium.org/2021/files/papers/issue3/popets-2021-0040.pdf

## Requirements
### R
- r-base (4.0.3)
- rvinecopulib (0.5.5.1.1) 

### Python
- numpy (1.19.5)
- scipy (1.6.0)
- pandas (1.2.1)
- scikit-learn (0.24.1)
- category_encoders (2.2.2)
- diffprivlib (0.4.0)
- xgboost (1.3.0)
- rpy2 (3.4.2)

### Example of setting the conda environnement
0. With conda installed, create a new environnement (here we named it copulashirley):
```conda create -n copulashirley```
1. Activate the environnement:
```conda activate copulashirley```
2. You might have to add conda-forge as a channel for the following commands:
```conda config --add channels conda-forge```
3. In the copulashirley environnement first install r-base with the following command:
```conda install r-base=4.0.3```
4. Run the R CLI in the conda by running:
```R```
5. In the R CLI, install the rvinecopulib package and dependencies with the command:
```install.packages('rvinecopulib')```
6. Quit the R CLI and in the copulashirley environnement install the Python packages with the following command:
```conda install numpy=1.19.5 scipy=1.6.0 pandas=1.2.1 scikit-learn=0.24.1 category_encoders=2.2.2 diffprivlib=0.4.0 xgboost=1.3.0 rpy2=3.4.2```


## How-to
- To output synthetic data: run main.py

- To output tests scores using k-fold cross-validation: run crossval.py

#### Parameters for main.py
```python
--dataset, default='adult' #Input dataset ('adult', 'compas' or 'texas_hospital')
--model, default='cop-shirl', choices=['cop-shirl', 'privbayes', 'dpcopula', 'dp-histogram'] #Generative model to use
--seed, type=int, default=76543
--n-sample, type=int, default=None #Number of synthetic samples to generate
--categorical-encoder, default=None, choices=('ORD', 'WOE', 'GLMM', 'OHE') #The encoder for categorical attributes
--cat-encoder-target, type=str, default=None #The target attribute for surpervised categorical encoder ('WOE' and 'GLMM')
--dp-epsilon, type=float, default=1.0 #The global budget for differential-privacy
--dp-mechanism, default='Laplace', choices=['Laplace', 'Gaussian', 'Geometric'] #The mechanism used for do-histograms computation in copula-shirley
--dp-global-sens, type=int, default=2 #The global sensitivity for the dp mechanism
--dp-gaussian-delta, type=float, default=0.001 #The delta for gaussian mechanism
--vine-sample-ratio, type=float, default=0.5 #The ratio for model vs. dp-histogram training (0.7 means 70% of data will be used as pseudo-observations for the vine-copula model and 30% will be used for dp-histograms)
--vine-family-set, type=str, default='all' #See rvinecopulib reference
--vine-par-method, type=str, default='mle' #See rvinecopulib reference
--vine-nonpar-method, type=str, default='constant' #See rvinecopulib reference
--vine-selcrit, type=str, default='aic' #See rvinecopulib reference
--vine-trunc-lvl, type=int, default=None #See rvinecopulib reference
--vine-tree-crit, type=str, default='tau' #See rvinecopulib reference
--privbayes-degree-max, type=int, default=3 #The maximum number of children for PrivBayes network  
--output-dir, type=str, default='./out' #Output directory
--n-cores, type=int, default=None #Number of cores to use (if None, inferred)
```

#### Parameters for crossval.py
```python
--n-folds, type=int, default=5 #The number of folds for k-fold cross-validation
--dataset, default='adult' #Input dataset ('adult', 'compas' or 'texas_hospital')
--model, default='cop-shirl', choices=['cop-shirl', 'privbayes', 'dpcopula', 'dp-histogram'] #Generative model to use
--seed, type=int, default=76543
--n-sample, type=int, default=None #Number of synthetic samples to generate
--categorical-encoder, default=None, choices=('ORD', 'WOE', 'GLMM', 'OHE') #The encoder for categorical attributes
--cat-encoder-target, type=str, default=None #The target attribute for surpervised categorical encoder ('WOE' and 'GLMM')
--dp-epsilon, type=float, default=1.0 #The global budget for differential-privacy
--dp-mechanism, default='Laplace', choices=['Laplace', 'Gaussian', 'Geometric'] #The mechanism used for do-histograms computation in copula-shirley
--dp-global-sens, type=int, default=2 #The global sensitivity for the dp mechanism
--dp-gaussian-delta, type=float, default=0.001 #The delta for gaussian mechanism
--vine-sample-ratio, type=float, default=0.5 #The ratio for model vs. dp-histogram training (0.7 means 70% of data will be used as pseudo-observations for the vine-copula model and 30% will be used for dp-histograms)
--vine-family-set, type=str, default='all' #See rvinecopulib reference
--vine-par-method, type=str, default='mle' #See rvinecopulib reference
--vine-nonpar-method, type=str, default='constant' #See rvinecopulib reference
--vine-selcrit, type=str, default='aic' #See rvinecopulib reference
--vine-trunc-lvl, type=int, default=None #See rvinecopulib reference
--vine-tree-crit, type=str, default='tau' #See rvinecopulib reference
--privbayes-degree-max, type=int, default=3 #The maximum number of children for PrivBayes network  
--MIA-n, type=int, default=500 #The number of synthetic profiles used per iteration of the Membership Inference Attack
--MIA-metric, type=str, default='hamming' #The distance used for the MIA
--MIA-n-iter, type=int, default=50 #The number of iteration
--output-dir, type=str, default='./out' #Output directory
--n-cores, type=int, default=None #Number of cores to use (if None, inferred)
--verbose, type=bool, default=True
```


## Code Author
- Alexandre Roy-Gaumond
