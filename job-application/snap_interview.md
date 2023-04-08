
- Practice LeetCode. Questions related to ML. Write a convolution from scratch.
- Why are Convolutional NNs important?
- What losses would you use when training CNNs?
  - Mean Squared Error (MSE) Loss: The MSE loss is a common choice for image reconstruction tasks. It measures the average squared difference between the predicted and ground-truth images. The advantage of this loss is that it is simple to implement and optimize. However, it tends to produce blurry images, especially when the input images are noisy.
  - Structural Similarity (SSIM) Loss: SSIM is a metric that measures the similarity between two images based on their structural information. It is used as a loss function by minimizing the difference between the predicted and ground-truth SSIM scores. This loss is known to produce sharper images than MSE loss, but it is more complex to implement and optimize.
    - The SSIM loss is based on three components: luminance, contrast, and structure. The luminance component measures the difference in overall brightness between the two images. The contrast component measures the difference in contrast between the two images. The structure component measures the difference in structural information between the two images.
    - The luminance component is calculated using the mean brightness of the two images. The contrast component is calculated using the standard deviation of the brightness of the two images. The structure component is calculated using the covariance of the two images.
    - The overall SSIM index is calculated by combining the three components using a weighted sum. The weights can be adjusted to give more importance to certain components depending on the specific requirements of the task.
  - L1 Loss: The L1 loss is another commonly used loss function for image reconstruction. It measures the absolute difference between the predicted and ground-truth images. Compared to MSE loss, L1 loss tends to produce sharper edges in the reconstructed image. However, it is more sensitive to outliers in the input data.
  - Perceptual Loss: Perceptual loss is a combination of content loss and style loss. It is used to train CNNs to reconstruct images that have similar content and style to the ground-truth images. The advantage of perceptual loss is that it can produce images that are more visually pleasing than other loss functions. However, it is more computationally expensive to implement and optimize.
  - Adversarial Loss: Adversarial loss is used to train CNNs to generate images that are indistinguishable from real images. It involves training a discriminator network to distinguish between real and fake images, and a generator network to generate images that can fool the discriminator. Adversarial loss can produce highly realistic images, but it is more difficult to optimize and prone to producing artifacts in the reconstructed image.
- What would you use when 2 images don't have to match exactly? Use feature-wise losses.
  - If the output image of a CNN for an image reconstruction task should not match exactly the ground-truth image, then a perceptual loss function would be a good choice. Perceptual loss is a combination of content loss and style loss, which are designed to encourage the reconstructed image to match the content and style of the ground-truth image, rather than the exact pixel values.
  - Content loss measures the difference between the feature representations of the ground-truth and reconstructed images at a specific layer of a pre-trained CNN. By minimizing the content loss, the network is encouraged to produce an image that has the same high-level features as the ground-truth image.
  - Style loss, on the other hand, measures the difference in the Gram matrices of the feature representations of the ground-truth and reconstructed images at different layers of a pre-trained CNN. By minimizing the style loss, the network is encouraged to produce an image that has the same texture and color distribution as the ground-truth image.
    - This is because the Gram matrix contains information about the correlations between the features in each layer, which can capture the texture and style of an image.
    - The Gram matrix is calculated by taking the outer product of the feature maps in a given layer, and then computing the dot product between the resulting matrices. This operation effectively computes the correlation between the features in the layer. By comparing the Gram matrices of the ground-truth and reconstructed images, the style loss is able to measure the similarity of their texture and style.
    - The activations from each channel can be taken, each flattened out into a 1 dimensional vector, then the dot products of each of those vectors with each other is taken to form a gram matrix. The dot product gives an indication of how correlated each combination of the channels are. If a channel was indicating texture and another channel was indicating brightly colours then a high dot product would indicate cells with texture also tend to have bright colours.
    - In contrast, measuring the difference between the feature representations themselves would only capture differences in the high-level content of the images, such as the presence of objects or the overall structure of the scene. By ignoring the correlations between the features in each layer, this approach would not be able to capture the texture and style of the image, which are important for tasks such as style transfer or image generation.
  - The combination of content and style loss can produce visually pleasing images that capture the essence of the ground-truth image while allowing for some degree of variation in the reconstructed image. Perceptual loss is particularly useful in situations where the exact pixel values of the ground-truth image are not important, such as in artistic style transfer or image generation tasks.
- Why do GANs work well? What's the difficulty with training GANs? How do you resolve mode-collapse?
- Diffusion models specifically for this position.
- Ask about different regularisations. What kinds of regularisations do you know? L2, L1, dropout, batchnorm, adaptive instance normalization, layer normalization. Batchnorm will be asked in detail (training / testing). What are the advantages 
- How does backprop work? Stochastic gradient descent / ADAM / Weight decay / Nestorov normalization. Different learning rate schedules. How to choose the learning rate schedules?
  - Nestorov normalisation
    - In standard momentum optimization, the update to the weights at each iteration is a combination of the current gradient and the previous update step. The idea behind momentum optimization is to use the momentum term to smooth out the gradient descent process and accelerate convergence towards the minimum of the loss function.
    - Nesterov normalization modifies the standard momentum optimization method by computing the gradient at a future location, instead of the current location, before computing the update to the weights. This technique helps to reduce oscillations and overshooting of the weight updates, resulting in faster convergence towards the minimum of the loss function.
    - In other words, in Nesterov normalization, the momentum term is used to update the weights "ahead of time" based on an extrapolation of the gradient at the future location, rather than the current location. This helps to correct for the effects of momentum and reduces the impact of overshooting, which can cause the optimizer to oscillate around the minimum of the loss function.
  - Learning rate schedules.
    - Start with a relatively high learning rate: It is often a good idea to start with a relatively high learning rate and gradually decrease it during training. This can help to speed up convergence and avoid getting stuck in local minima.
    - Consider using adaptive learning rate methods: Adaptive learning rate methods, such as Adam, Adagrad, and RMSprop, can automatically adjust the learning rate based on the gradients and second-order moments of the weights. These methods can help to speed up convergence and improve the stability of the training process.

Overall, selecting the right learning rate schedule can be a trial-and-error process that requires careful experimentation and monitoring. It is important to be patient and persistent, as training a large deep network for computer vision can be a time-consuming and computationally expensive task.

- Candidates would fail when being asked detailed questions. How are GANs trained? Do you train the networks together?
- Different kinds of image augmentation.
  - Some common image augmentation techniques used to train deep neural networks in computer vision include:
  - Random cropping: A random portion of the image is selected and cropped, which can help the network to learn to recognize objects at different scales and positions.
  - Random flipping: The image is randomly flipped horizontally or vertically, which can help to prevent overfitting and increase the robustness of the network.
  - Random rotation: The image is randomly rotated by a certain degree, which can help the network to learn to recognize objects at different orientations.
  - Random scaling: The image is randomly scaled up or down by a certain factor, which can help the network to learn to recognize objects at different sizes.
  - Random brightness and contrast adjustments: The brightness and contrast of the image are randomly adjusted, which can help the network to learn to recognize objects under different lighting conditions.
  - Random color jitter: The colors of the image are randomly adjusted, which can help the network to learn to recognize objects under different color distributions.
  - Gaussian noise: Gaussian noise is added to the image, which can help the network to learn to recognize objects under noisy conditions.
- Ask Param about coding questions.

Read Aliaksei's article on Acing ML Interview. Papers with Code summaries.

### From Param

1. Implement a 2D convolution with padding.
2. An ideal number has the only factors 3 and 5. Find all the ideal numbers in a range between x and y.

## Future interviews.

Generative models. Image augmentation. GANs, VAEs, pix2pix, normalizing flows, diffusion models.

Describe a conflict situation. Describe a situation where you failed. Describe a moment you failed. Describe when you challenged the status quo.

Screening interview - 1 hour
Full-day interview - 4-5 interviews
