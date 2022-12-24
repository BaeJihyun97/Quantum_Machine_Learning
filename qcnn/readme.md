# QCNN


The implementation is based on [Quantum convolutional neural network for classical data classification](https://arxiv.org/abs/2108.00661)
All figures on this page are from this paper.


## Quantum data encoding

Several encodings are introduced in this paper, amplitude encoding was chosen despite the computational overhead because it does not require classical dimension reduction. 

```math
\begin{align}
U_\phi\left(x\right)∶x\ \in\mathbb{R}^N\ \ \rightarrow\ \ \left|\phi\left(x\right)\right\rangle=\frac{1}{\parallel x\parallel}\sum_{i=1}^{N}{x_i\left|i\right\rangle}
\end{align}
```

Since 8 qubits are used in this implementation, the MNIST 28x28 dimension data are reduced to 16x16 robositically(mean value with padding) in preprocessing process. 


## Schema of QCNN
![qcnn1](https://user-images.githubusercontent.com/70127344/209432379-3abcbe41-a3da-410b-b92e-d1f713005158.png)
The convolution and polling process can be represented like this

```math
\left|\psi_i\left(\theta_i\right)\right\rangle\left\langle\psi_i\left(\theta_i\right)\right|=Tr_{B_i}\left(U_i\left(\theta_i\right)\left|\psi_i\left(\theta_i\right)\right\rangle\left\langle\psi_i\left(\theta_i\right)\right|U_i\left(\theta_i\right){^\dagger}\right)
 ,&ensp;where  &ensp;  B_i  ∈ C^(2^n/2^i )
```

$U_i$ is the parameterized unitary gate operation that iscludes quantum convolution and the gate part of pooling. Following images are detailed convolution and pooling layer used in this implementation. It is known that this convolutional circuit can implement arbitrary SO(4) gates.

![qcnn2](https://user-images.githubusercontent.com/70127344/209433098-ef576b1a-ec28-48ef-8230-09eebc489c86.png)

## Other details
* Binary Cross Entropy Loss is used for loss
* Parameter shift rule is used for weight updating. See [this](https://github.com/BaeJihyun97/Quantum_Machine_Learning/blob/main/qgan/readme.md)

## Result
Trained using 1000 images of 0 and 1 hand written digits with 1 interation.
![accuracy_test](https://user-images.githubusercontent.com/70127344/209433564-061d97d5-65cb-420d-b47d-a9d3784adab9.png)
![loss_test](https://user-images.githubusercontent.com/70127344/209433571-8de026a3-264c-4060-b43d-0488dbf21f25.png)
![loss_train](https://user-images.githubusercontent.com/70127344/209433574-5440506d-57a7-4a09-8f82-cd03f4bf7e06.png)
