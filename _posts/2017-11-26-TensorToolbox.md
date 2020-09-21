---
toc: true
layout: post
description: tensor toolbox for fortran
categories: [markdown]
title: Initial Release of Tensor Toolbox for Fortran
---

# Introducing Tensor Toolbox for Fortran

[Tensor Toolbox for Modern Fortran (ttb)](https://github.com/adtzlr/ttb) is a Fortran module to add Tensor features to Fortran. It provides derived data types from general arrays for rank 2 and rank 4 tensors (and it's symmetric variants). Computation of the deviatoric part, fourth-order identity tensor, dot product, double-dot product, etc. is available without constructing any loops by the user. For further information read the full post or have a look at the [ttb-repository](https://github.com/adtzlr/ttb).

## A short overview

Commercial FEM software packages often offer interfaces (user subroutines written in Fortran) for custom defined user materials like UMAT in Abaqus or HYPELA2 in MSC.Marc. Unlike other scientific programming languages like MATLAB or Python Fortran is not as comfortable to use when dealing with high level programming features of tensor manipulation. On the other hand it's super fast - so why not combine the handy features from MATLAB or Python's NumPy/Scipy with the speed of Fortran? That's the reason why I started working on a simple but effective module called **Tensor Toolbox for Modern Fortran**. I adopted the idea to my needs from [Naumann, C. (2016)](http://nbn-resolving.de/urn:nbn:de:bsz:ch1-qucosa-222075).

It provides the following basic operations for tensor calculus (all written in double precision `real(kind=8)`):
- Dot Product `C(i,j) = A(i,k) B(k,j)` written as `C = A*B` or `C = A.dot.B`
- Double Dot Product `C = A(i,j) B(i,j)` written as `C = A**B` or `C = A.ddot.B`
- Dyadic Product `C(i,j,k,l) = A(i,j) B(k,l)` written as `C = A.dya.B`
- Addition / Subtraction `C(i,j) = A(i,j) + B(i,j)` written as `C = A+B` or `C = A.add.B`
- Multiplication and Divison by a Scalar `C(i,j) = A(i,j) - B(i,j)` written as `C = A-B` or `C = A.sub.B`
- Deviatoric Part of Tensor  `dev(C) = C - tr(C)/3 * Eye` written as `dev(C)`
- Transpose and Permutation of indices `B(i,j,k,l) = A(i,k,j,l)` written as `B = permute(A,1,3,2,4)`
- Assigment of a real-valued Scalar to all components of a Tensor `A = 0.0` or `A = 0.d0`
- Assigment of a real-valued Array to a Tensor with matching dimensions `A = B` where B is an Array and A a Tensor
- Rank 2 Identity tensor of input type `Eye = identity2(Eye)` with `C = Eye*C`
- Rank 4 Identity tensor (symmetric variant) of input type `I4 = identity4(Eye)` with `C = I4(Eye)**C` or `inv(C) = identitiy4(inv(C))**C`

## Basic Usage
The most basic example on how to use this module is to [download the module](https://github.com/adtzlr/ttb/archive/master.zip), put the 'ttb'-Folder in your working directory and add two lines of code:

```fortran
include 'ttb/ttb_library.f'

program script101_ttb
use Tensor
implicit none
! user code

end program script101_ttb
```
The `include 'ttb/ttb_library.f'` statement replaces the line with the content of the ttb-module. The first line in a program or subroutine is now a `use Tensor` statement. That's it - now you're ready to go.

## Neo-Hookean Material
With the help of the Tensor module the Second Piola-Kirchhoff stress tensor `S` of a nearly-incompressible Neo-Hookean material model is basically a one-liner:

```fortran
S = dev(det(F)**(-2./3.)*Eye*C)*inv(C)+p*det(F)*inv(C)
```


## Sources
Naumann, C.: [Chemisch-mechanisch gekoppelte Modellierung und Simulation oxidativer Alterungsvorgänge in Gummibauteilen (German)](http://nbn-resolving.de/urn:nbn:de:bsz:ch1-qucosa-222075). PhD thesis. Fakultät für Maschinenbau der Technischen Universität Chemnitz, 2016.
