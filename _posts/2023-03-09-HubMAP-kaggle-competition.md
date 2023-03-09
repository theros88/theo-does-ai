---
layout: post
---

# HuBMAP + HPA - Hacking the Human Body Kaggle Competition
The Human BioMolecular Atlas Program (HuBMAP) is working to create a Human Reference Atlas at the cellular level. Sponsored by the National Institutes of Health (NIH), HuBMAP and Indiana University’s Cyberinfrastructure for Network Science Center (CNS) have partnered with institutions across the globe for this endeavor. A major partner is the Human Protein Atlas (HPA), a Swedish research program aiming to map the protein expression in human cells, tissues, and organs, funded by the Knut and Alice Wallenberg Foundation.

In this competition, we had to identify and segment functional tissue units (FTUs) across five human organs. The notebooks in this project were used to build a model using a dataset of tissue section images and with the goal of segmenting FTUs as accurately as possible.

At first, a baseline was created by submitting segmentation masks which were produced randomly using a uniform distribution. This gave us a Public Score of 0.29014 accuracy (the actual metric that was used was the mean Dice coefficient).
Then, a U-Net CNN model is used based on a Resnet34 architecture, which is trained with optimal LR. Inference on the test dataset is performed in a seperate step and this gave a precision of 0.44730 (Public Score)

## Results and further development
After this attempt, it bacame obvious that there was an improvement in the accuracy from the baseline of ~1.5x, but in the private 50% of the test set only a marginal 1.042x was gained (private score inference:0.34321 vs baseline's: 0.32931), which is deemed insignificant. An ensemble of models could be further used to improve this accuracy, but the main issue is the down-sizing of the high-resolution medical images to 512x512 used for training. Above this resolution, it was impractical/unfeasible to train the model in a reasonable amount of time. Apparently, the loss of signal in the process of down-sizing and training is considerable and an alternative technique should be used (e.g. tiling of the original images and train the model(s) with the tiles) in order to achieve decent accuracy of the model used. 