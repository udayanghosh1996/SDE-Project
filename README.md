

System Requirement

1. Linux OS
2. The system root directory `/` must have at least 20 GB free space
3. Docker 

 Installation

Build the Docker image:

docker build -f Dockerfile -t SDE-Project







First, launch a Docker container `sde-demo`:
```bash
docker run --name sde-demo -i -t sde --rm -v `pwd`:/Scratch
```

Then, set up the environment:
```bash
conda activate relancer
python setup_nltk.py
```

These commands activate the Conda environment and set up NLTK resources. 

If successful, there will be a `(relancer)` prefix on your command line prompt. For example,  
> (relancer) root@udayanghosh:/home/relancer#  

And there will be command line output like this:
> [nltk_data] Downloading package stopwords to /root/nltk_data...  
> [nltk_data]   Unzipping corpora/stopwords.zip.  
> [nltk_data] Downloading package wordnet to /root/nltk_data...  
> [nltk_data]   Unzipping corpora/wordnet.zip.  



The patch `auto-imports-beginner-level-analysis.patch` should be like this:
```diff
--- /home/relancer/relancer-exp/original_notebooks/toramky_automobile-dataset/auto-imports-beginner-level-analysis.py 2021-07-08 05:25:33.406257335 -0500
+++ /home/relancer/relancer-exp/fixed_notebooks/relancer/toramky_automobile-dataset/auto-imports-beginner-level-analysis.py 2021-07-08 05:25:42.890223574 -0500
@@ -1,3 +1,4 @@
+from sklearn.impute import SimpleImputer
 #!/usr/bin/env python
 # coding: utf-8
 
@@ -49,7 +50,7 @@
 # Import Linear Regression machine learning library
 from sklearn.linear_model import LinearRegression
 
-from sklearn.preprocessing import Imputer
+pass
 
 from sklearn.preprocessing import Normalizer
 
@@ -158,7 +159,7 @@
 
 
 # Imputting Missing value
-imp = Imputer(missing_values='NaN', strategy='mean' )
+imp = SimpleImputer(missing_values=np.nan, strategy='mean' )
 df_1[['normalized-losses','bore','stroke','horsepower','peak-rpm','price']] = imp.fit_transform(df_1[['normalized-losses','bore','stroke','horsepower','peak-rpm','price']])
 df_1.head()
 #########################################################################################################################
```

In this case, Relancer performs two fixes:  
1. Update the fully qualified name of API `sklearn.preprocessing.Imputer` to `sklearn.impute.SimpleImputer`  
2. Update the value of parameter `missing_values` from `'NaN'` to `np.nan`

