# VAE-mnist

uses mnist data set and convolutional layers to compress and reconstrcutre the mnist dataset.  

analysis.py plots the 2 dimensional latent space 

An autoencoder is a NN architecture that compresses and reconstructs a set of inputs. As the network is trained, reconstruction improves.

The primary difference between a VAE and Vanilla Autoencoder is the VAE operates better for generative applications and unseen models.

The Vanilla autoencoder can be used to detect anomalies by way of comparing reconstruction losses between the trained class of inputs and untrained inputs. 
A better explanation: https://www.youtube.com/watch?v=2K3ScZp1dXQ

## Latent Spaces
*Variational Autoencoder vs Vanilla Autoencoder*

Legend: 
- Purple: 0
- Indigo: 1
- Blue: 2
- Cyan: 3
- Sea Green: 4
- Green: 5
- Lime: 6
- Yellow-Orange: 7
- Orange: 8
- Red: 9

The points of each color represent how the handwritten digits get relatively encoded in the latent space. 
Reconstruction error would drastically reduce with an increase of dimensionality to the latent space – 2 is easier to plot though.

### Variational Autoencoder
![download (1)](https://user-images.githubusercontent.com/54888442/150994364-89e0e71a-6ecb-482c-a7e1-0f2ed6daaab0.png)

![download](https://user-images.githubusercontent.com/54888442/150994253-40644979-28ed-4c39-a447-a0c517c6531c.png)


### Vanilla Autoencoder
![before-regularization](https://user-images.githubusercontent.com/54888442/150994305-7608b85d-0d61-4f55-8b9f-1be0f053fa4b.png)

### Differences

The variational autoencoder uses a different loss function which is sent inside of the model's compile function.

This loss function uses a combined loss composed of reconstruction loss and KL loss.

#### Reconstruction Loss
Error is defined by y-target minus y-predicted. Reconstruction loss is the Mean of the Squared Error with respect to the first, second, and third axises of the matrix representing the image data. This is because the MNIST image data set is 28x28 pixels, by 1 color depth parameter. This is the x-position, y-position, and BW alpha value.

#### KL Loss (Kullback–Leibler divergence)
https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence
KL Loss is -1/2 of the Sum of 1 + the log variance - the square of Mu - the log variance exponentiated. 
Log variance and Mu are used in a Lambda layer to sample a point.
Log variance is a Dense layer the size of the latent space. Mu is a Dense layer the size of the latent space.
The sampled point is Mu + 1/2 the log variance exponentiated * a random normal distribution  of Mu with a mean of 0 and a standard deviation of 1.

All of this is to say that the Variational Autoencoder regularizes the output of the encoder component. This regularization can be seen with a latent space of 2 plotted on a X, Y graph.
