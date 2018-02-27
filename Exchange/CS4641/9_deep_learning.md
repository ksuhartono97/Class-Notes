# Deep Learning
Fundamentally there's no difference between deep neural net and normal neural net.

Train error at bottom for 1, test error at top. At infinity, test error at same place as train error, and train error is at bottom, and maybe even lower than earlier datapoints. As datasize grows larger, test error grows smaller.

Deep learning generally tries to overfit the train data, the larger the amount of data, the better the performance.

Brittle model, if it moves a little bit from the training data, it's gonna do really really badly.

Implication: the DATA is the primary thing that determines success.

## CNN
A collection of neurons (3x3) are used to scan through an image, which is then used to set weights in order to learn local features that is usable to determine an image.

Typically used for image classification.

## LSTMs
Better at global coherency than CNN. The local bits are more understandable, but globally bad. Want to pay attention to global features more than local features!

Exercise 2:
- CNN : image recognition, CNN better
- LSTM : text, LSTM better at recognizing
- LSTM: can be used to detect patterns in the music, local patterns that can be detectable.

## Layers

### Dropout
Helps with overfitting. Not going to just learn the most specific model for the data, going to be a little bit more general.

## Architectures
- Autoencoder/ autodecoder: learn an embedding of something.
- Generative Adversarial Networks: generate out content without ever actually training it.

Exercise 3:
- Autoencoder
- Autoencoder: basically repairing an image of a car.  
- GAN: one of the big things that people use GANs for.
