# Project Recommender System

We study the problem of recommending items to users using a collaborative-based filtering approach. In particular, we are  given access to 10000 users and 1000 movies, and a subset of their ratings, and we would like to recommend new
movies by predicting the missing ratings. To this end, we
implement 16 different models. A modified version of Singular
Value Decomposition (SVD++) performs the best among these
models. It achieves a score of 0.97738 on Kaggle’s validation set. 
In order to improve our predictions even further, we
implement a ridge regression model that predicts ratings based
on the predictions of 13 different models. We obtain a slight
improvement over SVD++, increasing our accuracy score to
0.97368 on Kaggle’s validation set. 

## Setting up the environment

* Install a python environment. For all our tests, anaconda environment was used.

* Install custom surprise library:
	* Clone this repository: https://github.com/manzo94/Surprise/tree/integrated_model
	* Install requirements: pip install -r <path_of_Surprise_folder>/requirements.txt
	* Install library:  pip install <path_of_Surprise_folder>
	* ### Throubleshooting:
		* The library may ask the installation of the Visual Studio 2015 compiler.
		  If asked follow the link which shows up in the error message and install the software.
	    * If the library can't be installed try to update all the python modules with 
		  "conda upgrade --all" and "pip install -U <modules>"
        * If you are using a mac laptop, make sure to you have xcode downloaded. Also, command line tools should be installed (you can install them by running xcode-select --install). Note that command line tools should be up to date.

* Install requirements for the project
	* Run: pip install -r <folder_of_project>/requirements.txt  
	  (Install required modules using conda if you prefer)

* Data Sets:
    * Download the data_train.csv and sample_submission.csv files from the competition page on kaggle.
	  (https://www.kaggle.com/c/epfml17-rec-sys). The files should be put in the folder ../data, with
	  respect to the code folder.
	  
* Download of dumps of predictions
	* In order to speed up the code we provide a pickle dump of all the models used for the blending. The folders containing the dumps can be downloaded from Switch Drive at the link: https://drive.switch.ch/index.php/s/1zqfWRX7Xbgsybn.
	The folders "predictions" and "test" should be put in the main folder. At the end the tree of folders should be as we show here:
	
	--Recommender System  
	-------code  
	-------data  
	-------figures  
	-------predictions  
	-------test  
	
## Description of files

* run.py is the main code which generates dumps (if not already generated) and the final prediction file (after the blending). If you want to reproduce all the predictions of the model, you need to remove "predictions" and "test" folders.
* models.py contains all the models used in the blending. Both custom and Surprise models are included in this file.
Each model function creates a pickle dump of the predictions and during the blending all the predictions are collected again from the dump files. The parameters of the models are hardcoded in their respective functions. Default path of the dumps are: ../predictions and ../test. The folders are automatically created if missing.
* *_helpers are files which contain helper functions. The description of each function is inside the files.
* plot.py contains functions to plot some of the graphs in the figure folder.

## Performances

When run.py is run, it automatically create a kaggle submission in the data folder called "final_submission.csv". It is the one which scores 0.97368 on the Kaggle public leaderboard.

The code takes approximately 4 hours on a Intel i7 6700HQ when executed from scratch (no pickle dump provided) and less than 2 minutes when all the model predictions have already been dumped (only blending). The algorithms are not parallelized, so only a fraction of the total computational power of the	CPU is used. No GPU is required since it is not exploited. The RAM usage is always lower than 4GB. In our tests, the code ran perfectly on a 8GB system.
	
These are the minutes the models take separately with data splitted in 93.3% training, 6.7% testing. The models not listed take less than 1 minute.  

    matrix_factorization_SGD : 13  
    matrix_factorization_ALS : 13  
    KNN_user                 : 50  
    KNN_item                 : 5  
    slope_one                : 4  
    svdpp                    : 3  
    svdpp                    : 140  
	

 

