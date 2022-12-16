# QGAN


The implementation is based on [Experimental Quantum Generative Adversarial Networks for Image Generation](https://arxiv.org/pdf/2010.06201.pdf)
All figures on this page are from this paper.


## Machine learning procedure
* Training data
* machine learning model     &ensp;&ensp;&ensp;     =>  &ensp;&ensp;      Parameterized quantum circuit
* Error function             &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;     =>  &ensp;&ensp;      GAN Loss
* An optimization algorithm  &ensp;&ensp;     =>  &ensp;&ensp;      Parameter shift rule
* Testing data




### GAN Loss

GAN loss is simple. There are two components generator, which make fake images, and discriminator that predict whether the images are fake or real. These two components play min max game on this loss function. 

```math
\min_\theta{\max_\gamma{\mathcal{L}\left(D_\gamma\left(G_\theta\left(z\right)\right),\ D_\gamma\left(x\right)\right)}}\ ∶=\mathbb{E}_{x~P_{data}\left(x\right)}\ \left[logD_\gamma\left(x\right)\right]+\mathbb{E}_{z~P(z)}[\log(1-D_\gamma(G_\theta\left(z\right))]
```

### Parameterized Quantum Circuit

Parameterized quantum circuit is a special type of quantum circuit model that consists of two qubits gates and trainable single qubit gates.

![parameterized_qc](https://user-images.githubusercontent.com/70127344/207999926-b31e76e3-783d-4353-bca3-047a59596788.png)

```math
U\left(\theta\right)\ ≔ \prod_{l=1}^{L}\left(U_EU_l\left(\theta\right)\right) ,&ensp;&ensp; U_l\left(\theta\right)=\bigotimes_{i=1}^{N}{(U_S\left(\theta^{\left(i,\ l\right)}\right))},&ensp;&ensp; where\ U_S\in\ SU\left(2\right),\ \theta\in\ R^{N\times L}
```


## The resource-efficient quantum GAN scheme


