---
layout: post
title:  "Explaining Y"
date:   2018-02-20 17:06:00 -0500
---
<div style="display:none">
$$
\newcommand{\Y}{\mathbf{Y}}
\newcommand{\om}{\mathbf{\omega}}
\newcommand{\Om}{\mathbf{\Omega}}
\newcommand{\Th}{\mathbf{\Theta}}
$$
</div>

In the lambda calculus, given a term $$F$$, how can we find a _fixed point_ for $$F$$---that is, a term $$X$$ such that $$FX=X$$? Well, if infinite terms were allowed, we could just take

$$X=F(F(\cdots))$$

with $$F$$ repeated infinitely many times. Because then we would have

$$FX=F(F(F(\cdots)))=X$$

Sadly, infinite terms are not allowed. However, we can achieve the desired goal by constructing a term which "generates" infinitely many $$F$$'s. First consider

$$\om=\lambda x.xx$$

and

$$\Om=\om\om$$

Then $$\Om$$ $$\beta$$-reduces to itself infinitely since

$$
\begin{align*}
\Om&=\om\om&&\text{by definition of }\Om\\
	&=(\lambda x.xx)\om&&\text{by definition of }\om\\
	&=\om\om&&\text{by }\beta\text{-reduction}\\
	&=\Om&&\\
	&=\cdots&&
\end{align*}
$$

If we introduce $$F$$ into $$\om$$, we can generate an $$F$$ at each $$\beta$$-reduction step of $$\Om$$. Let $$\om_F=\lambda x.F(xx)$$ and $$\Om_F=\om_F\om_F$$ (where $$x$$ does not occur free in $$F$$). Then

$$\Om_F=\om_F\om_F=(\lambda x.F(xx))\om_F=F(\om_F\om_F)=F(\Om_F)$$

In other words, $$X=\Om_F$$ is a fixed point of $$F$$.

We can generalize this and define the fixed-point combinator

$$\Y=\lambda f.\ \Om_f=\lambda f.(\lambda x.f(xx))(\lambda x.f(xx))$$

So $$\Y F=F(\Y F)$$ is a fixed point of $$F$$ for any $$F$$. This is the $$\Y$$ combinator.

The $$\Y$$ combinator is important because it lets us define _recursive_ functions in the lambda calculus. For example, if we want $$G$$ such that $$GX=X(XG)$$ for all $$X$$, we would have it if

$$G=\lambda x.x(xG)=(\lambda gx.x(xg))G$$

So we can just take $$G=\Y(\lambda gx.x(xg))$$.

The $$\Y$$ combinator is not the only fixed-point combinator. Above, we might have interchanged the order of $$\lambda f$$ and $$\lambda x$$ to obtain

$$A=\lambda xf.f(xxf)$$

and

$$\Th=AA$$

Then

$$\Th F=AAF=(\lambda f.f(AAf))F=F(AAF)=F(\Th F)$$

This is Turing's fixed-point combinator, which has certain advantages over the $$\Y$$ combinator. There are infinitely many more.

### References
- Barendregt, H. and E. Barendsen. _Introduction to Lambda Calculus._ 2000.

