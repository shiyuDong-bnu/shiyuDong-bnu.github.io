---
layout: post
title:  "Extrapolation "
date:   2026-02-02 10:14:29 +0800
categories: jekyll update
---
## papers
- Chemical Physics Letters Volume 286, Issues 3–4, 10 April 1998, Pages 243-252
- Phys. Rev. 126, 1015 – Published 1 May, 1962
- J. Chem. Phys. 106, 9639–9646 (1997)
## Estimate the number of basis set
For the correlaiton-consistent basis set the following simple formula is 
\begin{equation}
N_{cc-pVXZ}=\frac{1}{3}(X+1)(X+\frac{3}{2})(X+2)
\end{equation}
\begin{equation}
N_{cc-pCVXZ}=N_{cc-pVXZ}+N_{cc-pV(X-1)Z}-1
\end{equation}
##  Method of Extrapolation
In solving the electronic Schrodinger equation for molecular systems,two
approximations are induces: (1) the truncation in the one-electrn space to a finit basis ,and (2) the selection of in complete N-electron description inthe Fock space of the chosen one-electron basis.
A knowlege of the basis-set limits of the N-electron approximation is important, as it gives us information about the intrinsic errors of the different N-electron models, enabling us to investigate the accuracy of standard basis sets and correlation models.


 The use of extrapolations of fits to results obtained in hierarchical sequences of basis sets represents another way of deducing the basis-set limit that may be applied for cases that are prohibitively large for the R12 method.

 It is therefore important to establish the accurancy of the differenct extrapolation schemes,since a fit that reproduces the calculated finite basis-set result will not necessaritly yield the correct basis-set limit when extrapolated.

The correlation-consistent polarized valence basis sets,cc-pVXZ,and the correlation consistent
polarized core-valence basis sets,cc-pCVXZ,of Dunning and coworkers are examples of hierachical sequences of basis sets developed for valence correlatin energies and all-electron correlation energies,respectively.

In this study,we present standard calculations of CH2 at CASSCF and DSRG-PT2 . cc-pVXZ ,X=DTQ5,6,basis sets will been employed ,correlating only the valence electronss.We also presetn result of F12-DSRG-PT(2).
## Theory  of Extrapolation
Importance of angular correlation by Charles Schwartz:
The well-known Hartree approximation takes a spherical average of the interaction adn allows for only some radial correlation in the wavefunction.This method often gives quite satisfactory answers,and its goodness is easily atributed to the long-range nature of the force.Yet $$e^2/r_{12}$$ dose have some singularity  at small separations and this implies some important contributions from states of large relative-angular momentum.
Legendre Expansion of 
\begin{equation}
\frac{1}{r_{12}}=\sum_{l=0}^\infty \frac{r_<^l}{r_>{l+1}} P_l(\cos(\theta))
\end{equation}
Spherical harmonic expansion
\begin{equation}
\frac{1}{r_{12}}=4\pi\sum_{lm}\frac{1}{2l+1}\frac{r_<^l}{r_>{l+1}} Y_{lm}(\theta_1)Y^*_{lm}(\theta_2)
\end{equation}

By perburbation theory we know that  second order correlation energy
\begin{equation}
E_2=\sum_n \frac{\vert <0|1/r|  nh>}{E_0-E_n}=\sum_{l}E_2(l)
\end{equation}
\begin{equation}
\Psi_1=\sum_n \vert n \rangle \langle n \vert 1/r \vert /(E_0-E_n)
\end{equation}
When $$r_1\approx r_2$$
\begin{equation}
(\nabla_1^2-\nabla_2^2) \Psi_1\approx r \Psi_0
\end{equation}
\begin{equation}
E_2(l)\ge (45/256)l^{-4}
\end{equation}
\begin{equation}
\int^\infty_{L+1/2}(l+1/2)^{-4}=1/3 (L+1)^{-3}
\end{equation}

\begin{equation}
E_{corr}=a+bX^{-3}
\end{equation}
\begin{equation}
E_{SCF}=a+b e^{-c X}
\end{equation}

[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
