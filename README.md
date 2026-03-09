# Document-denoising
## Overview
This project attempts to denoise images of documents using two approaches - one using Basic Autoencoder and the other using Residual Autoencoder.
## Dataset
Source: https://www.kaggle.com/datasets/mohamedkhaled201841/image-denoising <br>
The dataset has 3 directories:
1. train - contains 144 noisy document images
2. train_cleaned - contains clean versions of the 144 noisy images
3. test - contains 72 noisy images
No ground truth (that is, cleaned images) are available for the test images.<br>
The images are of different sizes. So, for the purpose of training and testing, they are all resized to 256 x 256 x 1.<br>
The pixels are normalised to [0,1).
## Training
The noisy images are split into training and validation sets. The corresponding ground truth images are also split.<br>
Mean Squared Error is taken as the loss function. Peak Signal to Noise Ratio (PSNR) and Structural Similarity Index (SSIM) are used as metrics.<br>
Early stopping based on validation loss is used. <br>
Batch size=4, epochs=150<br>
### Approach 1: Using Basic Autoencoder
The network tries to learn to reconstruct clean image from the noisy image.
<img width="1706" height="461" alt="Screenshot (4999)" src="https://github.com/user-attachments/assets/7176fb87-f9f8-4861-82a0-6ce0ca7d6bfc" />
<br> Applying the autoencoder on a test image
<img width="1788" height="486" alt="Screenshot (5000)" src="https://github.com/user-attachments/assets/0b53b614-8702-4f0b-bf86-86780c81654b" />
<br> As can be seen from the above images, eventhough the noise is removed, the clarity of the text in the cleaned document has reduced.
### Approach 2: Using Residual Autoencoder
The network predicts only the difference between the noisy and clean image. This difference is called the residual.
Then, denoised image is computed as: **Clean Image = Noisy Image + Residual**<br>
<img width="1701" height="509" alt="Screenshot (5001)" src="https://github.com/user-attachments/assets/2f9eb404-e1e1-4995-9c2c-d43aa9d56725" />
<br> Applying the autoencoder on a test image
<img width="1694" height="471" alt="Screenshot (5002)" src="https://github.com/user-attachments/assets/1bc79ace-2111-4cb0-a08a-a5dc810e831b" />
<br> As can be seen from the above images, eventhough the clarity of the text in the cleaned document is high, the noise is not completely removed.
## Conclusion
This project tried two approaches to remove noise from document images. While basic autoencoder removes noise, residual autoencoder preserves the clarity of the text. 












