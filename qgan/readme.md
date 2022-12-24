# QGAN


The implementation is based on [Experimental Quantum Generative Adversarial Networks for Image Generation](https://arxiv.org/pdf/2010.06201.pdf)
All figures on this page are from this paper.


## Machine learning procedure
* Training data
* machine learning model     &ensp;&ensp;&ensp;&ensp;    =>  &ensp;&ensp;      Parameterized quantum circuit
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

### Parameter shift rule

we can view a quantum circuit as a black box and the gradient of this black box simply the difference between that quantum circuit evaluated at θ+s and θ−s. For parameterized quantum circuits, object function and respective gate can be written like these.

```math
U_G\left(\theta\right)=e^{-ia\theta G},&ensp;&ensp; f\left(\theta\right)=\left\langle\psi\left|U_G^{\dagger}\left(\theta\right)\ A\ U_G\left(\theta\right)\ \right|\psi\right\rangle
```
By differentiating the two equations and using idempotent of Hermitian generator, Euler’s identity, we get the below equation. 

```math
\begin{align}
{\partial \over {\partial\theta}} f(\theta)
\\\\
&= \left\langle\psi\right|\left[+iaG\right]U^{\dagger}_G\left(\theta\right)\ A\ U_G\left(\theta\right)\ \left|\psi\right\rangle
+\langle\psi|U_G^{\dagger}\left(\theta\right)\ A\ \left[-iaG\right]U_G\left(\theta\right)\ \left|\psi\right\rangle
\\\\
&=\frac{r}{2}\left\langle\psi\right|U_G^{\dagger}\left(\theta\right)\ (I+i\frac{a}{r}G)\ A\ (I-i\frac{a}{r}G)\ U_G\left(\theta\right)\left|\psi\right\rangle-\frac{r}{2}\langle\psi|U_G^{\dagger}\left(\theta\right)\ (I-i\frac{a}{r}G)\ A\ (I+i\frac{a}{r}G)\ U_G\left(\theta\right)\ \left|\psi\right\rangle
\\\\
&=r\left\langle\psi\right|U_G{^\dagger}\left(\theta+\frac{\pi}{4r}\right)\ A\ U_G\left(\theta+\frac{\pi}{4r}\right)\ \left|\psi\right\rangle\ -r\langle\psi|U_G^{\dagger}\left(\theta-\frac{\pi}{4r}\right)\ A\ U_G\left(\theta-\frac{\pi}{4r}\right)\ \left|\psi\right\rangle
\\\\
&=r\left[f\left(\theta+\frac{\pi}{4r}\right)-f\left(\theta+\frac{\pi}{4r}\right)\right]
\end{align}
```

For the Pauli gate, the eigenvalues are $\pm 1$ and a can be set to $\frac{1}{2}$ . More detail, see [this paper](https://arxiv.org/pdf/1905.13311.pdf![image](https://user-images.githubusercontent.com/70127344/208100418-e92b189c-7076-452a-acb5-12620f8d8b33.png)
)


## The resource-efficient quantum GAN scheme

![quantum patch gan](https://user-images.githubusercontent.com/70127344/208101486-5affbafa-9470-49d7-8296-a6571097bacf.png)

For encoding they use rotation y gate and alpha is sampled from the uniform distribution. The ancillary bit is for the non-linearity. Through the unitary gate, generated state psi is partially measured to obtain the classical result. For discriminator fully connected neural network is used

## Result
![qgan_result](https://user-images.githubusercontent.com/70127344/209433747-67ba33af-e6fc-4dac-8eb6-ff1a1726de66.png)

