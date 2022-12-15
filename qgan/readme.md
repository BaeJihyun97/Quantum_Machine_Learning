# QGAN


The implementation is based on [Experimental Quantum Generative Adversarial Networks for Image Generation](https://arxiv.org/pdf/2010.06201.pdf)


## Machine learning procedure
* Training data
* machine learning model          =>        Parameterized quantum circuit
* Error function                  =>        GAN Loss
* An optimization algorithm       =>        Parameter shift rule
* Testing data




### GAN Loss

GAN loss is simple. There are two components generator, which make fake images, and discriminator that predict whether the images are fake or real. These two components play min max game on this loss function. 

```math
\min_\theta{\max_\gamma{\mathcal{L}\left(D_\gamma\left(G_\theta\left(z\right)\right),\ D_\gamma\left(x\right)\right)}}\ ∶=\mathbb{E}_{x~P_{data}\left(x\right)}\ \left[logD_\gamma\left(x\right)\right]+\mathbb{E}_{z~P(z)}[\log(1-D_\gamma(G_\theta\left(z\right))]
```


## The resource-efficient quantum GAN scheme


