---
layout: post
title:  "Calculate permutation sign using cyles"
date:   2026-01-09 10:14:29 +0800
categories: jekyll update
---
# Calculate Permutation Sign using cycles 
 {% highlight ruby mark_lines="1 2" %}
def parity(permutation):
    ## permutation is a list of integer number range(0,n+1)
    ## it means  a two column representation of permutation
    ## (0 1 2 3 ... n)
    ## (per[0],per[1],... per[0] )
    ## for example if per=[3,2,1,0]
    ## we want to calculate all cycle
    ## then calculate the sign of all cycle
    circles=[]
    n_perm=len(permutation)
    for i in range(n_perm):
        ## check if this is a new circle
        in_circle=False
        for circle in circles:
            if i in circle:
                in_circle=True
                break
        if in_circle:
            continue
        ## generate new circle
        new_circle=[]
        new_circle.append(i)
        next_term=permutation[i]
        while next_term!=new_circle[0]:
            new_circle.append(next_term)
            next_term=permutation[next_term]
        ## save circle
        circles.append(new_circle)
    count=0
    for circle in circles:
        count+=len(circle)-1
    sign=(-1)**count
    return sign

if __name__=="__main__":
    from sympy.combinatorics import Permutation
    from sympy.core.random import shuffle,randint
    n_per=randint(2,100)
    per=list(range(0,n_per))
    shuffle(per)
    print("rand range",per)
    p = Permutation(per)
    print(parity(per))
    print(p.is_even)

 {% endhighlight %}



[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
