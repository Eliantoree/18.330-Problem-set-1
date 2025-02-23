# 18.330-Problem-set-1
18.330 Problem set 1

**Download Link:https://programming.engineering/product/18-330-problem-set-1/**

Description
5/5 – (2 votes)
The questions are a mixture of hand / analytical calculation and numerical cal-culation using Julia. You should submit a PDF file. You may photograph / scan your handwritten solutions for the theory parts, or (preferably) type them up as part of a Jupyter notebook that you print to PDF.

Exercise 1: Evaluating polynomials Consider the polynomial function

( , )= 0+ 1 +⋯+ .

Write a function poly_eval(a, x) to evaluate ( , ) in the naive way by just summing the terms as written. This should accept the coefficients 0, … , as a vector.

The Horner method is an alternative evaluation algorithm in which no powers of are (explicitly) calculated.

For example, for a quadratic ( ) = 2 2 + 1 + 0 we have ( ) =

0 + ( 1 + 2 )

Generalise this to polynomials of degree 3 and then degree

Implement this as a function horner(a, x).

Test horner to make sure it gives the same result as poly_eval.

Benchmark the two methods to evaluate the polynomial ( , ) = 1 + 2 + 3 2 + ⋯ + 10 10. Which algorithm is more efficient and by how much?

Count (approximately) the number of operations required by each of the two algorithms. Does this agree with your benchmarks? (Feel free to per-form more benchmarks to check this, e.g. using polynomials with random coefficients.)

Exercise 2: Calculating √ The Babylonian algorithm for calculating = √ is the following iteration:

1. Suppose that

+1

=

1

(

+

) .

.

that then we must have

2

∗

→ ∞

∗ = √

as

. Show

converges to some limiting value


To show that it does, in fact, converge, suppose (without loss of generality)

that 0 < √ .

Show that we then have < +1 < +1 < for all . Hence the form an increasing sequence that is bounded above, and hence they converge. (This is a theorem that we will just assume for this course.)

Write a function babylon that implements this algorithm. It takes a tolerance and iterates until the residual is < . It should return the sequence

( ).

Test your function to make sure it gives the correct result.

Use rational initial values to convince yourself that calculating with ratio-nals is a bad idea and that floating point is a good compromise.

Let = − ∗ be the distance of from the limiting value √ . (You may use Julia’s built-in sqrt function, or take the last data value as the limit.)

Plot the (absolute value of) as a function of on a suitable combination of linear and log scales. How fast does it seem to be converging?

Compare this on the same plot to the bisection algorithm from class. Which is better?

With defined as in [6.], show that +1 ≃ 2 (≃ means “is approxi-mately equal to”).

Hint: you may need to use a Taylor series expansion; if so you should calculate this (by hand).

Exercise 3: Collision of two discs [In this question we will finally find an actual use case for solving a quadratic equation!]

Suppose we have two discs located at positions x1 and x2, with velocities v1 and v2, respectively. The discs each have radius .

Find an expression for the condition that the discs collide (i.e. are touch-ing) at time , involving the distance between their centres.

Rewrite your expression from [1.] as a quadratic equation for the time . How many real solutions may this equation have? What do different numbers of solutions of this equation correspond to physically?

Write a function collision that takes all the data and calculates the collision time by using the quadratic formula. Make sure you take account of the answer to [2.]

Check that your code works by setting up some combinations of discs where you can do the calculation by hand (e.g. both discs moving at a 45-degree angle).


Exercise 4: Evaluating elementary functions

Implement the degree – Taylor polynomial approximation exp ( ) for exp( ) around = 0. Make sure that you do not explicitly calculate factorials in your code.

Make an interactive visualization using the Interact.jl package, showing exp and exp as varies.

Make another visualization showing the truncation error, i.e. exp( ) − exp ( ). How does it behave?

Calculate a bound for the truncation error using the Lagrange remainder. Use Stirling’s approximation to estimate how many terms you need to take for the error to be of a certain size .

Implement range reduction for the exponential function: instead of blindly applying a Taylor expansion (which will require many terms for large ), calculate exp( ) by reducing to the calculation of exp( ) for ∈ [−0.5, 0.5] using the relation

exp(2 ) = exp( )2.

Make an interactive visualization of the Taylor polynomial approximation to log(1+ ), showing visually that it fails outside a certain interval. Which interval is that, and why?

Exercise 5: Exactly representing irrationals using symbolic computing Here we will represent certain real numbers in the computer exactly. Effectively we will √use a type of symbolic computation, in which we explicitly keep the symbol 2, rather than approximating it by a floating-point number.

(Although this is not really the subject of the course, it’s useful to remember that there is a whole world of symbolic computation that can be applied to cer-tain problems, and that with a bit of work you often do not need an expensive commercial tool to do this!)

Consider the subset of the real numbers given by

= { +

2∶ , ∈ }

,

+

2

i.e. the set of numbers of the form

where

and

are rational.

√

1. Write down formulae for the sum,

difference and product of

√

1 + 1

√

2

and

, showing that the results are in .

they?

1/( +

)

is also in

by supposing that it equals

+

2

2. Show that

√

2+22

equations for

and

.

What type of equations are

and finding explicit√

and

√

Solve them to find explicit values for

in terms of and .


[This shows that we can also do division (by non-zero elements) and re-main within the set, i.e. that is a field, namely an extension field of ℚ.

]

Define a type FieldExtension to represent these number pairs, and the corre-sponding operations. Also define a show method to print them nicely using a √ symbol (typed as \sqrt<TAB>).

4.

sponding set.

1/(1 + √

2

+ √

3) as elements of the corre-

Find formulae to represent

Some Julia tips

Package installation

A package such as BenchmarkTools may be installed by running the following code a single time (only once in your current Julia installation):

using Pkg

Pkg.add(“BenchmarkTools”)

Load the package in each Julia session with

using BenchmarkTools

Benchmarking

Simple benchmarking (i.e. timing how long an operation takes) may be done using the @time macro:

“`julia

@time f(x)

“`

However, if the time taken is too short then this is not accurate. Instead, use the BenchmarkTools.jl package, with the syntax

“`julia

using BenchmarkTools

@btime f(1, $x)

“`

Note that any variables you pass in must be given $ signs like this.

Plotting

The Plots.jl package is used as follows after loading it with using Plots:


plot(x, y): plots the data with given coordinates and coordinates, join-ing those points with lines. These should be vectors.

plot(y): specifying only one argument plots the data against the numbers

1,2,…

plot(-1:0.1:1, f): you may pass in a range and a function instead of data.

plot!: adding ! adds a new plot to an existing one.

scatter: plots points instead of lines

Add yscale=:log10 inside the plotting command to use a logarithmic scale on the axis.

Note that there are small delays when first loading the package and for the first plot. Later plots will be quick.

Interactivity

The Interact.jl package enables us to generate simple interactive visualizations using a slider (and some other “widgets”).

To generate a single slider, wrap a for loop in the @manipulate macro, e.g.

@manipulate for i in 1:10

i^2

end

To manipulate a plot, put a plot as the result at the end of the for loop:

@manipulate for i in 1:10

plot(-5:0.01:5, x -> sin(i * x))

end

You can generate multiple sliders by using a joint for loop:

@manipulate for i in 1:10, j in 0.1:0.1:0.9

i + j

end
