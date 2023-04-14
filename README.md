# Zernike convolutional neural network (ZerNet)

This repository contains the implementation of the following paper:

> **"ZerNet: Convolutional Neural Networks on Arbitrary Surfaces via Zernike Local Tangent Space Estimation**<br>
> Sun Z, Rooke E, Charton J, He Y, Lu J, Baek S. <br>
> Paper: https://onlinelibrary.wiley.com/doi/pdf/10.1111/cgf.14012 <br>
> Code: https://github.com/zhisun/ZerNet
>
> **Abstract:** *In this paper, we propose a novel formulation extending convolutional neural networks (CNN) to arbitrary two-dimensional manifolds using orthogonal basis functions called Zernike polynomials. In many areas, geometric features play a key role in understanding scientific trends and phenomena, where accurate numerical quantification of geometric features is critical. Recently, CNNs have demonstrated a substantial improvement in extracting and codifying geometric features. However, the progress is mostly centred around computer vision and its applications where an inherent grid-like data representation is naturally present. In contrast, many geometry processing problems deal with curved surfaces and the application of CNNs is not trivial due to the lack of canonical grid-like representation, the absence of globally consistent orientation and the incompatible local discretizations. In this paper, we show that the Zernike polynomials allow rigourous yet practical mathematical generalization of CNNs to arbitrary surfaces. We prove that the convolution of two functions can be represented as a simple dot product between Zernike coefficients and the rotation of a convolution kernel is essentially a set of 2 × 2 rotation matrices applied to the coefficients. The key contribution of this work is in such a computationally efficient but rigorous generalization of the major CNN building blocks.*


ZerNet extends convolutional neural networks (CNNs) to process 2D manifolds using orthogonal basis functions called [**Zernike polynomials**](https://en.wikipedia.org/wiki/Zernike_polynomials). Due to their orthonormality over the unit disk, the normalized Zernike polynomials can represent a complex function on a surface as a weighted sum, defined on the unit disk $[0,1] \times [0,2\pi]$:

$$ f(r, \theta) = \sum_{n=0}^{\infty} \sum_{m=-n}^{n} \alpha_{nm} \hat{Z}^m_n(r, \theta) $$


## Zernike polynomials

Zernike polynomials are a sequence of polynomials which are orthogonal on the unit disk. Named after optical physicist Frits Zernike, Zernike polynomials are used to describe the magnitude and characteristics of the differences between the image formed by an optical system and the original object [Lakshminarayanan11]. Formally, the polynomials can be separated into even and odd sequence: 

$$ Z^m_n(r, \theta) = R^m_n(r) cos(m\theta), $$
$$ Z^{-m}_n(r, \theta) = R^m_n(r) sin(m\theta), $$

where $m, n$ are non-negative integer with $m \le n$, $r \in [0, 1]$ is the radial distance, and $\theta$ is the azimuthal angle on the disk. $R^m_n(r)$ is the Zernike radial polynomial.

## Zernike convolution

The Zernike convolution applies filters tangent to the manifold which is locally parameterized. Let $f: \mathcal{M} \rightarrow \mathbb{R}$ be a small patch on the manifold, and $g: T_p \mathcal{M} \rightarrow \mathbb{R}$ be the filter. By representing $f, g$ locally at point $p$ using Zernike polynomials, the Zernike convolution is simply the vector product of the Zernike coefficient vectors on the tangent space centered by $p$.
