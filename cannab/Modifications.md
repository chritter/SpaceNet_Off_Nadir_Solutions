# Modifications and Notes for STC

Christian Ritter

* Setup of Cannab for space-net-challenge-off-nadir-buildings task
* https://medium.com/the-downlinq/the-spacenet-challenge-off-nadir-buildings-introducing-the-winners-b60f2b700266

### Comments

* Loss function: Loss function used for training NN is combination of Dice and Folca losses: (Dice + 10 * Focal)
* Models rely on catalog id and nadir angle, this gave some score improvement. So for new data from another satellite positions need to retrain with subset of new data.
* Main input is an image
    * with 9 channels: 4 channels from Pan-Sharpen image + 
    * 4 other channels from MUL images + 1 PAN channel.
    * Additional inputs fused with decoder layers: nadir, catalog id one-hot encoded, tile x and y coordinates.
    * Data: https://spacenetchallenge.github.io/datasets/spacenet-OffNadir-summary.html
    * Training data size: 186GB images


* Ensemble of models:
    * seresnext50: [1] https://arxiv.org/abs/1709.01507
        * SeResNext50_9ch_Unet, in  train50_9ch_fold.py
        * ResNext architecture with squeeze-and-execitation (SE) module
    
    * dpn92: [2] https://arxiv.org/abs/1707.01629
    * senet154: [1]
    * seresnext101: [1]
* Next part is post-processing with watershed algorithm and LightGBM models to predict True Positives and False Positives.
* See instructions.txt 

* 
    * 

