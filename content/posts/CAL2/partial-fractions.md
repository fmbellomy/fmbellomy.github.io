---
title: "Partial Fractions"
date: 2022-09-01T17:40:10-05:00
draft: true
toc: false
katex: true
images:
tags:
  - untagged
---
Partial fractions is a technique used to transform a normally unapproachable integration problem involving a rational function of two polynomials into one that's more friendly to integration.

This article will not cover the actual integration step, only the conversion from the original nasty integral to a neater set of "easy" integrals.

Given a problem where a factor is repeated, you will need duplicate terms to take care of it.
When (x-a)^r appears in the factorization of the denominator, you will need r terms to take care of it.
$$\frac{f(x)}{(x-a)^r} = \frac{A}{(x-a)} + \frac{B}{(x-a)^2} + \frac{C}{(x-a)^2} + ... + \frac{A_r}{(x-a)^r}$$


$$\text{}$$
$$\text{}$$

$$\text{Given the following integral: }$$
$$\int\frac{x^2 + 4x + 6}{(x+1)^3}$$

$$\text{}$$

$$\frac{x^2 + 4x + 6}{(x+1)^3} = \frac{A}{x+1} + \frac{B}{(x+1)^2} + \frac{C}{(x+1)^3}$$
$$x^2 + 4x + 6 = A(x+1)^2 + B(x+1) + C$$

$$\text{}$$
$$x^2 + 4x + 6 = A(x^2 + 2x + 1) + B(x+1) + C$$
$$\text{coefficient of } x^2 = A = 1 $$
$$A = 1$$
$$\text{coefficient of } x \text{ (in this case) } = 2A + B$$
$$\therefore$$
$$B = 4 - 2(A)$$
$$B = 2$$
$$\therefore$$
$$C = 6$$


Given an irreducible quantity, we need a new term specifically for it.

$$\text{Given the following integral: }$$
$$\int\frac{5x^2+x+2}{x^3 + x^2 + x + 1}dx$$
$$\text{First, factor.}$$
$$ x^3 + x^2 + x + 1 = x^2(x+1) + 1(x+1)$$
$$=(x+1)(x^2+1)$$
$$\frac{5x^2+x+2}{x^3 + x^2 + x + 1} = \frac{A}{x+1} + \frac{Bx + C}{x^2 + 1}$$
$$5x^2 + x + 2 = A(x^2 + 1) + (Bx+C)(x+1)$$
$$\text{In order to set the second term of our partial fractions to 0 and find A:}$$
$$\text{Let }x = -1$$
$$5(-1)^2 + -1 + 2 = A(1 + 1) + (B(-1) + C)(0)$$
$$5 + -1 + 2 = 6 = A(2) + 0 = A(2)$$
$$\therefore$$
$$A = 3$$
$$\text{coeff of }x^2 = 5$$
$$5 = A + B$$
$$\therefore$$
$$B = 2$$
$$\therefore$$
$$C = -1$$
$$\therefore$$
$$\int\frac{5x^2+x+2}{x^3 + x^2 + x + 1}dx$$
$$=\int\frac{A}{x+1} + (\frac{Bx + C}{x^2 + 1})dx$$
$$=\int\frac{3}{x+1}dx + \int\frac{2x - 1}{x^2 + 1}dx$$