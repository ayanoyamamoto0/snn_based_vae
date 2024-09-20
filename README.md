# :brain: SNN-based VAE: Project Overview
* Preprocessed EEG data from Participant 1 from the DEAP dataset and converted them into spatially preserved EEG topographic maps
* From the 307,200 topographic maps, randomly downsampled the dataset into sets of 10,000, 20,000, 40,000, 80,000, and 160,000 images
* Built an SNN-based variational autoencoder for latent space interpretation and reconstruction of the topographic maps, with latent dimensions 25, 30, and 35
* Trained the models with datasets containing various number of images to test their scalability
* Compared it with ANN-variational autoencoders using MSE, MAE, and SSIM as evaluation metrics

## Reference
The code in this project is adapted from:

Kamata, H., Mukuta, Y., & Harada, T. (2022, June). *Fully spiking variational autoencoder*. In Proceedings of the AAAI Conference on Artificial Intelligence (Vol. 36, No. 6, pp. 7059-7067). [https://doi.org/10.1609/aaai.v36i6.20665](https://doi.org/10.1609/aaai.v36i6.20665 )

Github: [https://github.com/kamata1729/FullySpikingVAE](https://github.com/kamata1729/FullySpikingVAE)

## Other Code and Resources Used
* Environment: Python kernel on Google Colab
* Python Version: 3.10.12
* The DEAP dataset: [https://www.eecs.qmul.ac.uk/mmv/datasets/deap/](https://www.eecs.qmul.ac.uk/mmv/datasets/deap/)

## Creating Datasets
* [eeg_to_topographic_maps.ipynb](https://github.com/ayanoyamamoto0/snn_based_vae/blob/main/eeg_to_topographic_maps.ipynb) takes in the raw EEG data and filter it to isolate EEG data during music video playbacks. Then the data is filtered using a bandpass filter with a frequency range of 0.1 to 50 Hz, resampled to a reduced frequency of 128 Hz, and re-referenced to the average of all channels.
* [downsampling.ipynb](https://github.com/ayanoyamamoto0/snn_based_vae/blob/main/downsampling.ipynb) takes in the .npy file created by [eeg_to_topographic_maps.ipynb](https://github.com/ayanoyamamoto0/snn_based_vae/blob/main/eeg_to_topographic_maps.ipynb) and randomly downsamples them to a set number.

## Training, Validation, and Evaluation
* [snn_based_vae.ipynb](https://github.com/ayanoyamamoto0/snn_based_vae/blob/main/snn_based_vae.ipynb) and [ann_based_vae.ipynb](https://github.com/ayanoyamamoto0/snn_based_vae/blob/main/ann_based_vae.ipynb) individually processes each image by min-max normalisation, and trains and validates the models on the dataset split into subsets: 70% for training, 15% for validation, and 15% for testing.
* The reconstruction abilities of the models are evaluated using MSE, MAE, and SSIM.

## Results
* SNN-based models perform better with smaller datasets, and ANN-based models show better performance with larger datasets.
* The performance of ANN-based models significantly increases with dataset size, whereas the performance of SNN-based models does not scale with larger datasets.
* Increasing latent dimensions does not improve the performance of ANN-based VAEs, but SNN-based models benefit from a larger latent space.

3 samples each from the original images and the images reconstructed by ANN-based and SNN-based VAEs with latent dimension 35<br>
<img src="https://github.com/ayanoyamamoto0/snn_based_vae/blob/main/output_samples.jpg" width=50% height=40%>
