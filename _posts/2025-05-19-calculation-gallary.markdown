---
layout: post
title:  "Calculation of C2H2 methylene"
date:   2025-05-19 17:13:29 +0800
categories: jekyll update
---
Here we want to calculate the adiabatic excitation energy of C2H2

## Background
![AltText](/image/c2cs35394f-f1.gif)

The difference between vertical adiabatic and 0-0 exciation energy can be found at  this paper
"dx.doi.org/10.1021/jp501974p | J. Phys. Chem. A 2014, 118, 4157−4171"

The structure of single is optimized using dft ,taken from si of this paper
"dx.doi.org/10.1021/ct200272b | J. Chem. Theory Comput. 2011, 7, 2376–2386"

In this post ,we want to calculate the adiabatic excitateion energy  of Acetylene
of caspt2-f12 and nevpt2-f12 in molpro and orca respectivly.

## Ground State 


The strucutre of methylene is linear
{% highlight ruby mark_lines="1 2" %}
4

c 0.00000000000000 0.00000000000000 1.13109775801047 
c 0.00000000000000 0.00000000000000 -1.13109775801047 
h 0.00000000000000 0.00000000000000 3.13996154221094 
h 0.00000000000000 0.00000000000000 -3.13996154221094 
{% endhighlight %}
### molpro
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
#### Summary 
  1. The active space is C(2p) orbital,and we need to find two pi-bond orbital and two pi-antibond orbital. 
  2. The geomerty is linear 
  3. spin is singlet 
  4. wavefunction spatial symmetry is Ag
### orca
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
### Result
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
 	 Total Energy (E0+dE)    : E  = -77.13337713787729
 --------------------------------------------------------------- 
{% endhighlight %}

## Excited State
Now we need to calculate  the excited state.
In excited state, the geometry is as following 
![AltText](/image/excited_state.png)

{% highlight ruby mark_lines="1 2" %}
4

c -0.22872949141251 1.27002027174688 -0.00000000311696 
c 0.22872960517416 -1.27002040888460 -0.00000000311917 
h 1.29544929136450 2.67207978087269 0.00000003715195 
h -1.29545064696851 -2.67207814671517 0.00000003715897 
{% endhighlight %}
### molpro
In molpro the point group of excited state is denoted to be Cs
input
{% highlight ruby mark_lines="1 2" %}
gprint,orbitals=2,civector
basis=cc-pvdz-f12
bohr
geometry=C2H2A1.xyz
{HF;
}
put,molden,hf.molden
{multi,
occ  7,2 ;
closed  5,0; 
wf,elec=14,spin=0,sym=2;
state 2;
weight 1 0;
}
put,molden,cas.molden
{RS2-F12,shift=0;
wf,symmetry=2,spin=0;
}
{% endhighlight %}
output 
{% highlight ruby mark_lines="1 2" %}
 RS2-F12/cc-pVDZ-F12 energy=    -76.999081928598

         RS2-F12           MULTI          HF-SCF
    -76.99908193    -76.69704216    -76.75296781

{% endhighlight %}
### orca
In orca the point group of excited state is determinated to be C2h which is correct.
After HF we need to find the order of mos of four pi-bond and pi-antibond orbital

{% highlight ruby mark_lines="1 2" %}

----------------
ORBITAL ENERGIES
----------------

  NO   OCC          E(Eh)            E(eV)    Irrep 
   0   2.0000     -11.296779      -307.4010    1-Ag
   1   2.0000     -11.295308      -307.3610    1-Bu
   2   2.0000      -1.012950       -27.5638    2-Ag
   3   2.0000      -0.765920       -20.8417    2-Bu
   4   2.0000      -0.596013       -16.2183    3-Ag
   5   2.0000      -0.417948       -11.3729    3-Bu
   6   2.0000      -0.386648       -10.5212    1-Au
   7   0.0000       0.020162         0.5486    4-Ag
   8   0.0000       0.060384         1.6431    4-Bu
   9   0.0000       0.081533         2.2186    5-Ag
  10   0.0000       0.090870         2.4727    1-Bg
  11   0.0000       0.091065         2.4780    5-Bu
  12   0.0000       0.101260         2.7554    2-Au
  13   0.0000       0.129303         3.5185    6-Ag
  14   0.0000       0.137025         3.7286    7-Ag
{% endhighlight %}
The orbital in active space is 
{% highlight ruby mark_lines="1 2" %}
   5   2.0000      -0.417948       -11.3729    3-Bu
   6   2.0000      -0.386648       -10.5212    1-Au
   7   0.0000       0.020162         0.5486    4-Ag
  10   0.0000       0.090870         2.4727    1-Bg
{% endhighlight %}
First we need to rotate the group of {8,10}

Next the excitation is from 6-->7

The symmetry is Au X Ag = Au

The input of orca for casscf is 
{% highlight ruby mark_lines="1 2" %}
!HF  cc-pvdz-f12 Usesym   bohrs
!moread
%moinp "HF.gbw"
% scf 
  rotate 
        {8,10,90}
  end
end
%casscf 
   nel 4
   norb 4
   mult 1
   irrep  2 
   nroots 1
#   PTMethod fic_nevpt2
#   ptsettings
#     f12 true
#   end
   
end 
*xyzfile  0 1  C2H2A1.xyz
{% endhighlight %}
output is 
{% highlight ruby mark_lines="1 2" %}
 Symmetries of active orbitals:
   MO =    5  IRREP= 3 (Bu)
   MO =    6  IRREP= 2 (Au)
   MO =    7  IRREP= 0 (Ag)
   MO =    8  IRREP= 1 (Bg)
-------------------------   --------------------
FINAL SINGLE POINT ENERGY       -76.697042114451
-------------------------   --------------------
{% endhighlight %}

Finally the  f12 result is 
{% highlight ruby mark_lines="1 2" %}
 --------------------------------------------------------------- 
 	 Total Energy Correction : dE = -0.24327214974453
 --------------------------------------------------------------- 
 	 Reference  Energy       : E0 = -76.69704211445088
 --------------------------------------------------------------- 
 	 Total Energy (E0+dE)    : E  = -76.94031426419541
 --------------------------------------------------------------- 
{% endhighlight %}

## Wrong Result
When I first try to calculate the excited state, I use the spatical symmetry A^\prime instead of 
But I think what is wrong is active space.
## Conclusion 
Need to check all input parameter !!!

[forte_home]: https://github.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
