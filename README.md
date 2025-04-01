# Image Colorization using Deep Learning
Started playing with computer vision and deep learning more as I start doing more advanced robotics projects. Still playing with this project. Interested to research DL vs optimization for applications like medical imaging. This project builds a CNN for image colorization using deep transfer learning.

## Dataset

The model is trained on approximately 7,000 RGB landscape images and tested on 5 grayscale images. The training data enables the model to learn the mapping between grayscale inputs and their corresponding color outputs.

## Methodology

The colorization task is treated as a regression problem, predicting the 'a' and 'b' channels of the LAB color space from the 'L' (lightness) channel. The LAB color space is selected because it separates luminance (L) from chrominance (a, b), allowing the model to focus solely on color prediction without altering brightness.

The solution uses an autoencoder architecture:
- **Encoder**: Extracts features from the grayscale input using the convolutional layers of VGG16, pre-trained on ImageNet, with weights frozen to leverage transfer learning.
- **Decoder**: A custom CNN with upsampling layers that generates the 'a' and 'b' color channels from the encoded features.

### Key Steps

1. **Data Preprocessing**
   - Images are resized to 224x224 pixels to align with VGG16's input requirements.
   - RGB images are converted to LAB color space.
   - The 'L' channel serves as the input, while the 'a' and 'b' channels are the targets.

2. **Model Architecture**
   - The encoder uses the first 19 layers of VGG16, retaining pre-trained weights for robust feature extraction.
   - The decoder consists of convolutional and upsampling layers to reconstruct the color channels.
   - The combined model takes a grayscale image (L channel) and outputs the predicted 'a' and 'b' channels.

3. **Training**
   - The model is optimized using the Adam optimizer with mean squared error (MSE) loss.
   - Training runs for 2000 epochs with a batch size of 16.

4. **Inference**
   - For a test grayscale image, the model predicts the 'a' and 'b' channels.
   - These predictions are combined with the original 'L' channel and converted back to RGB for visualization

### References
This project is based on a similar one from a great platform I've been using to speed up my learning through videos and projects --> [ProjectPro](https://www.projectpro.io/)
