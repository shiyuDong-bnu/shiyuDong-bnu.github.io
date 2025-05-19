---
layout: post
title:  "Calculation of C2H2 methylene"
date:   2025-05-19 17:13:29 +0800
categories: jekyll update
---
Here we want to calculate the adiabatic excitation energy of C2H2

The difference between vertical adiabatic and 0-0 exciation energy can be found at  this paper
"dx.doi.org/10.1021/jp501974p | J. Phys. Chem. A 2014, 118, 4157−4171"
The structure of single is optimized using dft ,taken from si of this paper
"dx.doi.org/10.1021/ct200272b | J. Chem. Theory Comput. 2011, 7, 2376–2386"
Using  singlet as an example, we describe the calcultion of caspt2-f12 and nevpt2-f12 in molpro and orca respectivly

The strucutre of methylene is
{% highlight ruby mark_lines="1 2" %}
4

c 0.00000000000000 0.00000000000000 1.13109775801047 
c 0.00000000000000 0.00000000000000 -1.13109775801047 
h 0.00000000000000 0.00000000000000 3.13996154221094 
h 0.00000000000000 0.00000000000000 -3.13996154221094 
{% endhighlight %}
The input of molpro is 
{% highlight ruby mark_lines="1 2" %}
gprint,orbitals=2,civector
basis=cc-pvdz-f12
bohr
geometry=C2H2X.xyz
{HF;
}
put,molden,hf.molden
{multi,
occ  3,1,1,0,2,1,1,0 ;
closed  3,0,0,0,2,0,0,0; 
wf,elec=14,spin=0,sym=1;
!rotate 4.1,6.1,90
!rotate 3.5,6.5,90
}
put,molden,cas.molden
{RS2-F12,shift=0;
wf,symmetry=1,spin=0;
}
{% endhighlight %}
The input of orca is 

{% highlight ruby mark_lines="1 2" %}
!HF  cc-pvdz-f12 Usesym   bohrs largeprint 
*xyzfile  0 1  C2H2X.xyz
{% endhighlight %}
{% highlight ruby mark_lines="1 2" %}
!HF  cc-pvdz-f12 Usesym   bohrs
!moread
%moinp "HF.gbw"
% scf 
  rotate 
        {6,9,90}
  end
end
%casscf 
   nel 4
   norb 4
   PTMethod fic_nevpt2
   ptsettings
     f12 true
   end
   
end 
*xyz  0 1  
c 0.00000000000000 0.00000000000000 1.13109775801047 
c 0.00000000000000 0.00000000000000 -1.13109775801047 
h 0.00000000000000 0.00000000000000 3.13996154221094 
h 0.00000000000000 0.00000000000000 -3.13996154221094 
*
{% endhighlight %}
The output of molpro is 
{% highlight ruby mark_lines="1 2" %}
         RS2-F12           MULTI          HF-SCF
    -77.18737976    -76.91519896    -76.84728822
{% endhighlight %}

The output of orca is 
{% highlight ruby mark_lines="1 2" %}

 ===============================================================
                       NEVPT2 Results  
 ===============================================================
   *******************************
    MULT 1, IRREP  Ag, ROOT 0 
   *******************************

  Class V0_ijab :	 dE = -0.067841971472 
  Class Vm1_iab :	 dE = -0.061599918270 
  Class Vm2_ab  :	 dE = -0.026472162485 
  Class V1_ija  :	 dE = -0.008119245188 
  Class V2_ij   :	 dE = -0.001871859387 
  Class V0_ia   :	 dE = -0.050330027838 
  Class Vm1_a   :	 dE = -0.001943111619 
  Class V1_i    :	 dE = -0.000000000000 

 --------------------------------------------------------------- 
 	 Total Energy Correction : dE = -0.21817829625785
 --------------------------------------------------------------- 
 	 Reference  Energy       : E0 = -76.91519884161944
 --------------------------------------------------------------- 
{% endhighlight %}
[forte_home]: https://github.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
