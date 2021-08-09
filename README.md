# SSPWAM

This repository contains the implementation of the paper "Non-Reference, Pixel-Wise Assessment of Abdominal CT Image Quality" by Ayaan Haque, Adam Wang, and Abdullah-Al-Zubaer Imran.

We propose SSPWAM, a novel, self-supervised IQA model which predicts SSIM Image Quality maps from low-dose CT. We propose a self-supervised regularization task of dose-level estimation creating a multi-tasking framework to improve performance.

## Abstract

## Model

We predict SSIM IQA maps from inputted LD using a U-Net like model architecture. The groundtruth SSIM maps are generated by calculating an SSIM score for each individual pixel between the reference FDCT and LDCT. Instead of simply LDCT as our input, we use a high-pass filter (HPF) and LDCT concatenated input. The high-pass filter channel provides additional context for the model, improving its performance.

We simultaneously train the model to predict the dose level of LDCT as a self-supervised, auxiliary task. Each LDCT can be assigned a label of its dose. This is a self-supervised task because the dose level information is freely available. Training in a multi-task learning framework has been shown to improve performance, reduce overfitting, and improve generalizations because the model must fit to two separate tasks and data representations. Moreover, the information learned from one task can assist in the performance of the other task. 

## Dataset

We primarily collect abdomen scans from the publicly available Mayo CT data. 
The dataset includes CT scans originally acquired at routine dose level (full dose), so simulated quarter dose images are reconstructed through inserting Poisson noise into each projection dataset. We use 20 full dose abdomen CT and the corresponding quarter (25%) dose CT scans and select the middle 50 slices from each scan. We use 10 scans for training (500 slices) and 10 scans for testing (500 slices). Our dataset only contains one set of low-dose CT images at quarter dose. To perform IQA on CT images at other doses, we simulate different doses by scaling the zero-mean independent noise from 25\% to 5 separate dose levels: 5%, 10%, 50%, and 75%.

## Results

A brief summary of our results are shown below. Our algorithm SSPWAM and is compared to various baseline architectures and training procedures. In the table, the best scores are bolded.

## Code

The code has been written in Python using the Pytorch framework. Training requries a GPU. We provide a Jupyter Notebook, which can be run in Google Colab, containing the algorithm in a usable version. Open [SSPWAM.ipynb]() and run it through. Uncomment the training cell to train the model.

## Citation

If you find this repo or the paper useful, please cite:

```
citation
```

