# eacl-2017-code-dataset

This repository contains the code used for dependency parsing and information about how to obtain the dataset presented in the work:

[Reconstructing the house from the ad: Structured prediction on real estate classifieds](https://bekou.github.io/papers/eacl2017/bekoulis-eacl2017.pdf).

The dataset includes 2,318 manually annotated property advertisements from a real estate company.

If you use part of the code or the dataset please cite:
  
> @InProceedings{bekoulis-EtAl:2017,  
> author    = {Bekoulis, Giannis  and  Deleu, Johannes  and  Demeester, Thomas  and  Develder, Chris},  
> title     = {Reconstructing the house from the ad: Structured prediction on real estate classifieds},  
> booktitle = {Proceedings of the 15th Conference of the European Chapter of the Association for Computational Linguistics: Volume 2, Short Papers},  
> month     = {April},  
> year      = {2017},  
> address   = {Valencia, Spain},  
> publisher = {Association for Computational Linguistics},  
> pages     = {274--279}  
> }  


### Pre-requisites ###

The code is written for Python 2.7. Some of the python packages needed to run these files, best installed using *pip*.

* scikit-learn (machine learning)
* pandas (Data manipulation)
* pandas_confusion (performance measures)

#### Dependency parser ####

In the repository, one can find the 4 models (Threshold, Edmond, Structured Prediction via the Matrix-Tree Theorem (MTT), Transition-based) that we have developed for dependency parsing. One should run the *run_script.py* file that serves as a main function.

#### Dataset ####

To obtain the anonymized dataset fill in and sign [this](https://github.com/bekou/ad_data/raw/master/agreement/data-agreement.pdf) form. Follow the instructions and we will get back to you as soon as possible with information about how to download the anonymized dataset. 
