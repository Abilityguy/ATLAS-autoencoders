# ATLAS-autoencoders

Here, we train an autoencoder (AE) to compress the four-momentum data of jet particles. This data provides information on the four-momentum of particles from experiments run at ATLAS, CERN.

## Network
The AE is a simple feed forward network with tanh activation and layers whose size go from 4 to 200 to 20 to 3 and then back all the way to 4. The four-momentum features of the particles are compressed to a 3 features at the bottleneck of the AE.

## Preprocessing
Three different scaling methods have been applied to the data to identify the best method to apply.
- Min-Max Scaling - Features are scaled between [0, 1] based on the minimum and maximum values in the data.
- Standard Scaling - Features are scaled to have 0 mean and 1 variance.
- Custom Scaling - Here, we look at the distribution of each of the four-momentum particles and normalise each feature accordingly.
    - Since E and pT  follow the e-x distribution, a logarithm of the distribution is computed. Then, this data is min max scaled.
    - η is standard scaled since it follows a normal distribution.
    - ɸ is min-max scaled since it follows a uniform distribution.

## Results
The data is split into training and test splits in the ratio 70:30. The AE was trained on each preprocessing method and the mse loss averaged over 3 runs is tabulated below.

| Scaling Method| Testing Loss  |
| ------------- |:-------------:|
| Min-Max       | 1.32e-5       |
| Standard      | 1.03e-4       |
| Custom        | 1.89e-6       |

The results point that custom scaling method provides the best reconstructed data.

## Plots
Compression and residual plots generated can be found [here](https://github.com/Abilityguy/ATLAS-autoencoders/tree/master/plotOutput).
