# QGAN
---

The implementation is based on [Experimental Quantum Generative Adversarial Networks for Image Generation](https://arxiv.org/pdf/2010.06201.pdf)

## Machine learning procedure

---

### GAN Loss

```math
\min_\theta{\max_\gamma{\mathcal{L}\left(D_\gamma\left(G_\theta\left(z\right)\right),\ D_\gamma\left(x\right)\right)}}\ ∶=\mathbb{E}_{x~P_{data}\left(x\right)}\ \left[logD_\gamma\left(x\right)\right]+\mathbb{E}_{z~P(z)}[\log(1-D_\gamma(G_\theta\left(z\right))]
```


## The resource-efficient quantum GAN scheme

---
