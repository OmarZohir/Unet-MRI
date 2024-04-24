
## Summary
This project involves training a U-Net model on single-coil knee MRI data for image reconstruction, on the fMRI Unet model from [this paper](https://arxiv.org/abs/1811.08839). This generative model allows to generate different images than those of the dataset, yet belong to the same distribution, which can then be used for training other models (e.g., for classification problems). The dataset consists of training images and corresponding ground truth images generated from fully sampled k-space data. The goal is to reconstruct images from 8-fold accelerated k-space data. 

## Model Training
- **Dataset**: Dataset per [the baseline](https://arxiv.org/abs/1811.08839) used 973 volumes. However, due to hardware limitations, we were only able to use 88 volumes to shorten the training duration.
- **Optimizers**: RMSprop overfitted less compared to Adam.
- **Epochs**: Models were trained to monitor validation loss decrease to save weights and avoid overfitting. After 5 epochs, the validation loss did not change much, and started to significantly fluctuate betweem 20-30 epochs. Thus, 5 epochs were used.
- **Loss Function**: Investigated MSE, MAE, and SSIM loss functions with MAE yielding the best results as follows:

## Results
### Loss Function Metrics
| Metric | MSE Loss | MAE Loss | SSIM Loss |
|--------|----------|----------|-----------|
| NMSE   | 0.136    | 0.103    | 0.103     |
| SSIM   | 0.437    | 0.482    | 0.465     |
| PSNR   | 22.26    | 22.85    | 22.27     |

### Model Performance Comparison
| Model  | NMSE     | SSIM     | PSNR  |
|--------|----------|----------|-------|
| Ours   | 0.103    | 0.482    | 22.85 |
| Baseline | 0.049  | 0.654    | 29.86 |

- Our model was able to reconstruct the undersampled MRI images using with 74% accuracy (Per SSIM), using only 9% of the data used in [the baseline](https://arxiv.org/abs/1811.08839) model
