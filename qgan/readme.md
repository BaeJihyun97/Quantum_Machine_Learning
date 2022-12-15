# QGAN

---

The implementation is based on [Experimental Quantum Generative Adversarial Networks for Image Generation](https://arxiv.org/pdf/2010.06201.pdf)

## Machine learning procedure

---

###GAN Loss

```math
min_\theta\ max_\gamma\funcapply\mathcal{L}(D_\gamma\ (G_\theta\ (z)),\ D_\gamma\ (x))\ \ \ \∶=\mathbb{E}_(x~P_data\ (x)\ )\ \ [logD_\gamma\ (x)]+E_(z~P(z)) [log⁡(1-D_γ (G_θ (z))]
```


## The resource-efficient quantum GAN scheme

---
