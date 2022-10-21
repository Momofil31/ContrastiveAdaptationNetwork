# Deep Learning Course Project
## Students:

* ### Filippo Momesso - filippo.momesso@studenti.unitn.it
* ### Thomas De Min - thomas.demin@studenti.unitn.it
  
## Introduction
This year's (A.Y. 2021/2022) Deep Learning course's project involves the topic of Unsupervised Domain Adaptation (UDA). We have been provided an UDA dataset consisting of two domains: <u>Real World</u> and <u>Product</u>. The objective is to "propose a UDA technique to counteract the negative impact of the domain gap". 

### Dataset
The dataset [Adaptiope](https://ieeexplore.ieee.org/document/9423412) counts 123 classes but, in this case, only 20 of them will be investigated, each of them is balanced. Indeed, each class is made of 100 samples. As requested by the assignment we used a 80% train/test split.

### Delivery
In order to deliver a competitive solution in the real world, as a Deep Learning's project, we decided to dig into the literature of Unsupervised Domain Adaptation. Moreover, we also investigated the results of some of the recent techniques on the provided dataset.

We decided to deliver:
* A **baseline** implementation, that involves a ResNet18 fine-tuned on the source domain and tested on the target domain, in order to investigate upper and lower bound on the accuracy;
* The implementation of the [**Contrastive Adaptation Network (CAN)**](https://arxiv.org/abs/1901.00976), one of the state-of-the-art techniques in the field and the most promising approach for Adaptiope Dataset;
* Our **improved version** of CAN.

[Here](https://wandb.ai/229356_229298/DL2022_229356_229298) you can find our Weight and Biases project with all the plots we showed and additional metrics and informations, like some wrongly predicted images.

> Note: In all these scenarios a ResNet18 has been employed as backbone model.

### Experiments
For each approach we performed the UDA experiment in both directions, one at a time.
* For the **baseline** approach we trained on Products and tested on Real World test set, in order to get a lower bound accuracy for the domain adaptation task. Vice-versa for Real World to Products. We also trained the network on both training sets and tested on their corresponding test set in order to get the upper bound accuracy.
* For the implementation of **CAN** and our further **improvements** we procedeed in a similar way, but we omitted the computation of the upper bound.
  
Since each approach has its own requirements we trained all approaches with 30 epochs, except for CAN vanilla which required 60 epochs in order to converge. We kept as best model the one with the highest accuracy on the test set. For reproducible results, train and test splits are handled by a Generator with seed 0.

> Note: We would have liked to train also the other approaches with 60 epochs, but it was time consuming in terms of GPU. 

### Requirements
* We expect to load the datasets from a directory positioned in the root of Google Drive, named "datasets". The file must be named `Adaptiope.zip` (default name). Basically we will load the dataset from the following path `/content/drive/MyDrive/datasets/Adaptiope.zip `
* By default weights are not saved throughout epochs but, if you would like to do so, please provide a directory in the root of Google Drive named "weights". Moreover, turn the save flag to `True` before running the training function. To load the stored weights, set the variable `weights=/path/to/weights` in the training loop function.

> Note: Weights saving can be enabled only for CAN and CAN improvements.