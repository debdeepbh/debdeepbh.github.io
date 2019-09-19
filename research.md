---
title: Research
---

## Research Interests

I enjoy problems with a good mix of abstraction and applicability. I work on a variety of problems coming from 
* [nonlinear dispersive partial differential equations](#nonlinear-dispersive-equations)
* [signal processing](#signal-processing)
* [solid mechanics](#solid-mechanics) 
* [machine learning](#machine-learning) 

[//]: this is a comment 

***

### Nonlinear Dispersive Equations
[Dispersive equations](https://en.wikipedia.org/wiki/Dispersive_partial_differential_equation) model the propagation of waves in various media. Nonlinearities make the study of dispersive equations more realistic, as well as mathematically interesting. For example, when the effect of nonliearity opposes the effect of dispersion (defocusing case), these equations exhibit peculiar solutions called [solitons](https://en.wikipedia.org/wiki/Soliton) that retain their spacial localization for a long time. [John Scott Russell](https://en.wikipedia.org/wiki/John_Scott_Russell) observed such a solitary-wave in a shallow river in 1834. [Here](https://www.youtube.com/watch?v=w-oDnvbV8mY) is an experiment.


My work on nonlinear dispersive equations has been about the low-regularity theory, especially in the critical regime, where we can observe a dichotomy between global existence and blow-up of the solution, depending on the mass of the initial data. 
With my advisor [Svetlana Roudenko](https://case.fiu.edu/about/directory/people/svetlana-roudenko.html) and collaborator [Luiz Gustovo Farah](https://sites.google.com/site/lgfarah/), I have studied the Zakharov-Kuznetsov equation and its modifications, which model [ion-accoustic wave](https://en.wikipedia.org/wiki/Ion_acoustic_wave) propagation in magnetized plasma. It is also a generalization of the celebrated [Korteweg-de Vries equation](https://en.wikipedia.org/wiki/Korteweg%E2%80%93de_Vries_equation) for shallow water waves.

The study of global well-posedness of low-regularity data requires the careful investigation of the interaction of constituent frequencies of the solution, together with tools from Harmonic analysis such as [Fourier analysis](https://en.wikipedia.org/wiki/Fourier_analysis) and [Paley-Littlewood analysis](https://en.wikipedia.org/wiki/Littlewood%E2%80%93Paley_theory) -- a technique collectively known as the *I*-method. On the other hand, low-regularity solutions that blow up in finite time have the property that the mass concentrates inside a ball of shrinking radius. The main tools here are the *I*-method and profile decomposition.

[//]: Currently, I am studying the inhomogeneous [nonlinear Schr&ouml;dinger](https://en.wikipedia.org/wiki/Nonlinear_Schr%C3%B6dinger_equation) and the [Hartree equation](https://en.wikipedia.org/wiki/Hartree_equation).

* _Global well-posedness for low regularity data in the 2d modified Zakharov-Kuznetsov equation_ with [Luiz Gustovo Farah](https://sites.google.com/site/lgfarah/) and [Svetlana Roudenko](https://case.fiu.edu/about/directory/people/svetlana-roudenko.html) (Submitted) [(arXiv)](https://arxiv.org/abs/1906.05822)
* _Mass concentration of $H^s$ blowup solution to 2D modified Zakharov-Kuznetsov equation_ with [Luiz Gustavo Farah](https://sites.google.com/site/lgfarah/) (In preparation)

***

### Signal Processing
Even though I was first exposed to Harmonic analysis as a tool to study dispersive equations, I became interested in its application in other areas of science, in particular signal processing, when I took a class on [frames](https://en.wikipedia.org/wiki/Frame_(linear_algebra)), [wavelets](https://en.wikipedia.org/wiki/Wavelet), time series analysis and [compressed sensing](https://en.wikipedia.org/wiki/Compressed_sensing) by [John Benedetto](https://www.math.umd.edu/~jjb/). 

During Summer 2018, I had the opportunity to work with the [ANITA](https://en.wikipedia.org/wiki/Antarctic_Impulse_Transient_Antenna) collaboration, a research group conducting balloon experiments in the antarctic region with a goal to detect ultra-high energy neutrinos. Filtering out electro-magnetic noises picked up by the highly sensitive antennas of ANITA payload and de-blurring the signals is known as the [deconvolution problem](https://en.wikipedia.org/wiki/Deconvolution) in signal processing. I worked with the astrophysicists at the University of Hawaii under the supervision of [Peter Gorham](https://www.phys.hawaii.edu/~gorham/) on the optimal deconvolution problem using Fourier and Wavelet analysis and implemented a C++ library called [libWTools](https://github.com/debdeepbh/libWTools). I am currently working on a multi-antenna generalization of this algorithm.

* Report on _Deconvolution problem and application to ANITA signals_, submitted to ANITA collaboration at University of Hawai'i at Manoa [(link)](/content/report-anita.pdf)
* _Generalized ForWaRD algorithm for multi-antenna model_ (Preprint)

***

### Solid Mechanics
Understanding how solid materials deform and fail under external loading conditions has been a long-standing area of research for scientists and engineers for centuries. 
The classical approach is to treat the solids as a [continuum](https://en.wikipedia.org/wiki/Continuum_mechanics) and model the displacements of material points as a solution to a differential equation, known as the [Cauchy Momentum equation](https://en.wikipedia.org/wiki/Cauchy_momentum_equation).
However, due to the differential formulation, the classical theory fails to describe material behavior when the deformation field is non-differentiable at certain material points, for example, when a fracture is formed.

Introduced by [Stewart Silling](https://www.sandia.gov/~sasilli/) in 2000,  [peridynamics](https://en.wikipedia.org/wiki/Peridynamics) has become useful to address this limitations.
Peridynamics assumes that every material point interacts with its neighbors via a bond force and reformulates material deformation using an integral equation, thus accommodating discontinuous deformations, such as fractures. Peridynamics has been used to model crack formation and crack branching, among many other fracture problems.

 ![crack-branching](content/meshout.gif)
*Simulation of crack propagation and branching in soda-lime glass with a pre-notch under external force in the outward vertical direction* [[code]](https://github.com/debdeepbh/numerical/tree/master/crack) 


Working with [Pablo Seleson](https://web.ornl.gov/~selesonpd/) and [Jeremy Trageser](https://cam.ornl.gov/jtrageser2.html) at the [Oak Ridge National Laboratory](https://www.ornl.gov/), 
I considered three-dimensional axisymmetric problems, where the geometry of the material is symmetric about an axis of symmetry and the external loading conditions are such that the deformation fields are symmetric about the same axis of symmetry. This is an important class of problem in solid mechanics where the symmetry can be exploited to reduce dimension of the problem. We derived the two-dimensional model that exactly represent the full 3D axisymmetric linear peridynamic model by incorporating out-of-plane bond forces into the representative 2D plane, thus reducing the computational cost significantly.



[//]: I am currently working on a similar treatment for the fully nonlinear 3D axisymmetric peridynamic model.

* Report on _Reduction of three-dimensional axisymmetric problems to two dimensions in Peridynamics_, submitted to the NSF as part of [MSGI](https://orise.orau.gov/nsf-msgi/) program [(link)](/content/NSF-report-signed.pdf)
* _Reduction of three-dimensional axisymmetric problems to two dimensions in Peridynamics_ with [Pablo Seleson](https://web.ornl.gov/~selesonpd/) and [Jeremy Trageser](https://cam.ornl.gov/jtrageser2.html) (Preprint)

***

### Machine Learning

During Summer 2018, I was learning to use  popular machine lerning techniques using *scikit-learn* as yet another problem-solving tool. While documenting my understanding, I became more interested in the underlying mathematics of it.
With [Radu Balan](https://www.math.umd.edu/~rvbalan/) and Naveed Haghani, I am working on a 
 permutation-invariant encoding algorithm of data points in Euclidean space.

*  [My repository](https://github.com/debdeepbh/ml) to document notes and solved exercises from the book *Hands-On Machine Learning with Scikit-Learn and TensorFlow*
* _Permutation-invariant encoding of data in Eulidean space_, with [Radu Balan](https://www.math.umd.edu/~rvbalan/) and Naveed Haghani (In preparation)

***


