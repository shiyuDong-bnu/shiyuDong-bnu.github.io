---
layout: post
title:  "frozen core and basis set"
date:   2025-07-03 21:28:29 +0800
categories: jekyll update
---

## Background
reference 

J. Chem. Theory Comput. 2025, 21, 6, 2977–2987 https://doi.org/10.1021/acs.jctc.4c01731


A very widely applied approximation for electron correlation
methods  is the frozen-core approximation,
whereby the lowest lying MOs are “frozen”, prohibiting
excitations from these orbitals and only including excitations
from valence or “active” orbitals. This approximation also
coincides with an intuitive chemist’s picture where the core
electrons are considered to be less sensitive to changes in the
environment and chemical reactions are determined by valence
electrons. 
In fact, it has been found that the error introduced
by the frozen-core approximation is minimal in terms of
relative energies and additionally for geometries of
related methods.
Furthermore, for practical applications,
the use of the frozen-core approximation is preferred since
most of the commonly used basis sets are designed to correlate
the valence electrons only.
## basis set
Specifically, most AO and auxiliary
basis sets are not equipped to describe the core region
sufficiently and special basis functions, that is, Gaussians with
large exponents, would have to be added to the basis sets in
order to describe the correlation between core electrons as well
as core and active electrons such as, for example, in
Dunning’s cc-pCVXZ73 and cc-pwCVXZ74 basis sets (where X
= D, T, Q, 5, ...). 
## auxiliary basis set 
The problem with auxiliary basis sets is even
more obvious since they are often developed within the frozen-
core approximation and, thus, do not contain any core
functions. One possible solution is the use of automatically
generated auxiliary basis sets, for example, developed by Neese
and coworkers.75 However, these basis sets are usually about
twice the size of optimized basis sets, which makes the
computation much more expensive. Another possible solution
lies in the utilization of optimized auxiliary basis sets in
combination with the frozen-core approximation for the
underlying electron correlation method, which allows to
overcome the restrictions on the basis set selection.
## advatages of using frozen core approximation
A further
advantage when using the frozen-core approximation comes
with the increased computational efficiency since the active
occupied space excludes the core electrons. 
Thus, the limited
availability of all-electron basis sets together with the higher
computational cost for larger basis sets makes the use of the
frozen-core approximation preferable within electron correla-
tion methods.
In addition, the frozen-core approximation
entails no significant loss of accuracy for quantities such as
structural parameters or relative energies.

## How to   choose the number of frozen core and potential problem
The definition of core electrons,Chemical Physics Letters,Volume 350, Issues 5–6,2001,Pages 573-576,
https://doi.org/10.1016/S0009-2614(01)01345-8.


 A common practice is to carry out a Hartree–Fock calculation on the electronic ground state 
 and then to select the appropriate number of orbitals with the lowest one-electron energies .
However, difficulties arise when the core energies of one atom lie above the energies of some valence atomic orbitals of another atom .
A notable example is gallium trifluoride GaF3, where the energy of a gallium 3d-orbital lies above that of a fluorine 2s orbital. 
In the G2 model, the former is treated as a part of the core while the latter is part of the valence shell

The number of core electrons are 
2(Li to Mg) 10(Al to Ca) 18 (Sc to Kr)

### Conclusion 


[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
