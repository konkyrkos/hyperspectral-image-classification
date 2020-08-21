# Hyperspectral Image Classification

This repository provides my solution for Project assignment for the course of Machine Learning and Computational Statistics for the MSc in Data Science at Athens University of Economics and Business.

## Hyper Spectral Image (HSI)

An HSI depicts a specific scene at several (L) narrow continuous spectral bands (actually, they visualize the reflectance of the depicted scene
in various spectral bands). 
It can be represented by a MxNxL three-dimensional cube, where the first two dimensions correspond to the spatial information, while the third
corresponds to the spectral information. 
Thus, the (i,j) pixel in such an image, i=1,…,M, j=1,…,N, is represented by an L-dimensional vector (constituted by the corresponding
spectral bands), called the spectral signature of the pixel.
The HSI may depict specific scenes of the earth surface at a specific spatial resolution (that is, a single pixel
may represent an area from 3x3 m2 , to, e.g., 100x100m2 or more). 
That is, each pixel is likely to depict more than one materials depicted in the corresponding area of the
scene. 
Such pixels are called mixed pixels and they are the vast majority of the pixels in the image. On the other hand, there are (usually) a few pixels that depict a single
material. These are called pure pixels.

## Problem set - Processing HSI

### Spectral unmixing

The problem here is stated as follows: Assume that a set of m spectral signatures corresponding to the pure pixels in the HSI under study is given.
For a given pixel in the image, the aim is to determine the percentage (abundance) to which each pure material contributes in its formation. 
It is clear, that SU provides sub-pixel information for a given pixel. 
Speaking in mathematical terms, let
(i) y be the (column L-dimensional) spectral signature of the pixel under study,
(ii) x1,… xm, be the spectral signatures (column L-dimensional vectors) of the pure
pixels in the image (each one corresponding to a pure material met in the image) and
(iii) θ, the m-dimensional abundance vector of the pixel (its q-th coordinate
corresponds to the percentage to which the q-th pure pixel contributes to the
formation of the pixel under study).
Adopting the linear spectral unmixing hypothesis, the above quantities are related
as follows y = X * θ + η where η is an L-dimensional i.i.d., zero mean Gaussian noise vector. Note that,
physically, the entries of θ should be nonnegative and (ideally) they should sum to
one.

### Supervised Classification

In this case, the problem is stated as follows: Assume that all the pixels in the HSI under study are known to belong to one out of m
known classes. 
Given a specific pixel, the aim is to determine the most suitable class to assign it.

## Data explained

All questions in this project refer to the so called “Pavia University” HSI, which depicts
an area of the University of Pavia in Italy. It is a 300x200 spatial resolution HSI and
consists of 103 spectral bands, gathered by the ROSIS sensor. Its spatial resolution is
1.3m (that is, the HSI is a 300x200x103 cube). The HSI depicts materials from nine (9)
classes. The data that will be used are in the files “PaviaU_cube.mat” (the Pavia
University hypercube) and “PaviaU_ground_truth.mat” (the class label for each pixel). 
Only the pixels with nonzero class label will be taken into consideration in this
project.

## Project Description

### Spectral Unmixing

The “PaviaU” HSI includes 9 endmembers, each one corresponding to a certain material,
as described in the following table:
1) Water
2) Trees
3) Asphalt
4) Self-Blocking Bricks
5) Bitumen
6) Tiles
7) Shadows
8) Meadows
9) Bare Soil

The aim is to perform unmixing on each one of the pixels in the image with
nonzero label, with respect to the 9 endmembers using the following five different spectral unmixing methods:

(a) Least squares
(b) Least squares imposing the sum-to-one constraint
(c) Least squares imposing the non-negativity constraint on the entries of θ
(d) Least squares imposing both the non-negativity and the sum-to-one constraint on
the entries of θ
(e) LASSO, i.e., impose sparsity on θ via 𝑙1 norm minimization.

(A) For each method we:
(i) Derive the corresponding 9 abundance maps (one for each
endmember/material)
(ii) Compute the reconstruction error (for each (non-zero class label) pixel yi
compute the quantity ||𝒚𝑖 − 𝑋𝜽𝑖||^2 and then take the average over those pixels).

(B) We then compare the results obtained from the above five methods (focusing on the
abundance maps and the reconstruction error) and comment briefly on them using
the class information given in “PaviaU_ground_truth.mat”.

### Classification

In this case, we consider also the image pixels with non-zero class label. The task is to
assign each one of them to the most appropriate class, among the 9 known classes. To
this end four classifiers will be used: 
(i) the naïve Bayes classifier, 
(ii) the minimum Euclidean distance classifier, 
(iii) the k-nearest neighbor classifier and 
(iv) the Bayesian classifier.

#### Part A:

For each classifier:

(i) We train it based on the training set performing 10-fold cross validation. We report the estimated validation 
error as the mean of the ten resulting error values along with the associated standard deviation.

(ii) After that, we use the whole training set to train the classifier and evaluate their
performance on the test set as follows: First, we compute the confusion matrix and then 
we identify the classes that are not well separated by the classifier. 
Then, we compute the success rate of the classifier.


#### Part B:

We compare the results of the classifiers and comment on them 





