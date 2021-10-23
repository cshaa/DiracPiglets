# Dirac Piglets: The Lebesgue Integral (script)
Author: Michal Grňo

----


## Abstract
Lorem ipsum. Prerequsites: limits, Riemann integral

## Intro / Channel Theme
Dirakovská prasátka + cool hudba.

## Motivation
“vertical” Riemann integral

  * overview on $f: \mathbb R \to \mathbb R$
  * what about $\mathbb R^n$, $S^1$, $S^n$, Klein bottle?
  * value of $\int_0^1 \chi_{\mathbb Q}(x) \; \mathrm{d}x$?
  * incompleteness of $\mathscr R$, eg. $g_n(x) = \max\{-n,\, \ln x\}$
  * something something limiting process


Generalization for $f: X \to \mathbb R$

  * “horizontal” Lebesgue integral
  * measuring $\Omega \subset X$ is easier than partitioning it
  * naïve definition of Lebesgue integral if we know how to $\mu(\Omega)$


## Motivation for measure theory
Imagine you have a sphere with surface area equal to one. One day a friend of yours comes by and asks you, whether you could measure the area of a particular subset of that sphere. You might think: “Well, of course, it is my sphere and I can do anything with it. Surely I can measure the area of any subset you wish!” And you'd be wrong. Surprisingly, there are certain subsets whose area you just cannot measure, no matter how hard you try.

To see this is true, we don't have to look any further than to the famous Banach-Tarski paradox. In case you haven't heard of the Banach-Tarski paradox, there is a [great video by Vsauce](https://youtu.be/s86-Z-CbaHA) which I very much recommend you to watch! However, here's a quick rundown for you:  If you have a sphere, you can divide it into a bunch of disjoint subsets in such a way that these subsets can then be rearanged into two complete spheres of the same exact size as the original. Weird, huh? Feel free to pause the video and think about it!

In fact, it is because the five sets are actually eldritch lovecraftian monsters waiting to claim our world and eat our souls—

From this paradox, it should be quite obvious that we cannot tell the area of those intermediate sets. For the sake of argument, suppose we *can*. We started with a sphere of area one and cut it into five disjoint pieces – this means that the areas of those pieces should add up to one. However, we also used those pieces to put together *two* spheres with total area of two, therefore the areas of those pieces should add up to two. Aha, a contradiction!

## Measurable spaces
All right, we have shown that in order to measure sets, we can't just make do with our intuition, we have to build a more rigorous theory. But where do we start? Remember, we want to eventually measure all kinds of stuff: lengths on the real line, areas on various curved surfaces, volumes in 3D, maybe even hypervolumes in curved spacetime. So let's try specifying the most general rules, which must be obeyed by every single set we might possibly want to measure.

Imagine we have a space $X$ and a measuring device $\mu$. We'll be using a sphere to depict the space $X$, but keep in mind that it might also be a plane, a 3D volume – anything along these lines. Now, we might choose a subset of $X$ and ask the measuring device $\mu$ to measure it. $\mu$ will either display a number, telling  us the length / area / volume of that subset (in short called the *measure* of the subset), or it will tell us that this particular subset cannot be measured and display an error.

For the measuring device to be any good, it should be able to measure the empty set. If we ask it about the empty set, it should simply display a zero. It should also be able to measure the entire $X$ – for our example sphere it would show 1, for a different sphere it might be for example 13.6 and for a plane it would be infinity – but it should be *a* number, not an error. Furthermore, if $\mu$ can measure some subset $A$, it should also be able to measure its complement, $X$ minus $A$, as it can just subtract one from the other. And finally, let's say there are two disjoint sets $A$ and $B$ which both can be measured. Then it only makes sense if $A$ union $B$ can also be measured – its measure is just the sum of the two!

$$
\begin{align*}
    &\, \emptyset \, \text{ is measurable} \\
    &X\text{ is measurable} \\
    &\text{if }A\text{ is measurable, then }X \setminus A\text{ is measurable}\\
    &\text{if }A, B\text{ are disjoint and measurable, then }A \cup B\text{ is measurable}
\end{align*}
$$
What if the sets aren't disjoint? Then there's no easy way of calculating the measure of $A$ union $B$, but I mean – wouldn't it be really weird if we could measure two sets, but not their union? You know what? This is our theory, we make the rules. Let's just get rid of that disjointness premise.
$$
\begin{align*}
    &\, \emptyset \, \text{ is measurable} \\
    &X\text{ is measurable} \\
    &\text{if }A\text{ is measurable, then }X \setminus A\text{ is measurable}\\
    &\text{if }A, B\text{ are measurable, then }A \cup B\text{ is measurable}
\end{align*}
$$
This is better! Notice how these rules also give us intersections for free, since the intersection of $A$ and $B$ is the complement of the union of *their* respective complements.
$$
    A \cap B = X \setminus \Big( \, (X\setminus A) \cup (X\setminus B) \, \Big)
$$
These rules we've created come up in other parts of maths too, so they've been given a name. Somewhat confusingly, they're called *an algebra of sets*. You probably know the algebraic operations on numbers – addition, negation, etc.  You see, the union of sets is a little like addition of numbers, and the complement is a little like negation. To be honest, I don't think that giving two things that are just *a little* similar the exact same name is a particularly good idea, but we'll just roll with it.

Okay, we almost have our definition of measurability. There's just one small detail left. The rule which tells us that a union of measurable sets is measurable also works for the union of more than two sets. We can use induction to prove that the union of any *finite* number of measurable sets is itself measurable.
$$
\begin{align*}
    A \cup B \cup C \cup D
    &= {\underbrace{A \cup B}_{\text{measurable}}\!} \cup C \cup D \\[5pt]
    &= {\underbrace{(A \cup B)\cup C}_{\text{measurable}}} \cup D \\[5pt]
    &= \underbrace{\big( (A \cup B)\cup C \big) \cup D}_{\text{measurable}}
\end{align*}
$$
But does it work for an *infinite* sequence of sets? In fact, no, it doesn't. Proofs by induction don't tell us anything about infinity. And, as it turns out, measure theory without infinite union would be pretty toothless – we'll see why in a while. Therefore, let's change the fourth rule: if we have a sequence of sets $A_i$ where each set is measurable, their union is also measurable.
$$
\begin{align*}
    &\, \emptyset \, \text{ is measurable} \\
    &X\text{ is measurable} \\
    &\text{if }A\text{ is measurable, then }X \setminus A\text{ is measurable}\\
    &\text{if }A_i\text{ where }i \in \mathbb{N}\text{ are measurable, then }\bigcup_i A_i = A_1 \cup A_2 \cup\text{... is measurable}
\end{align*}
$$
These rules are a stricter version of algebra, called a $\sigma$-algebra. And it is exactly this $\sigma$-algebra that we'll use as our definition of measurability. Specifically, if we have a space $X$ and a $\sigma$-algebra of its measurable subsets, we call it a measurable space. Okay, case closed, see you in the next video!

Whatcha say? That this is too abstract? That you have no idea how to use it? Oh, I see, you do have a point – this definition *is* very abstract. Let's do a few examples to hopefully sort things out.

## Examples of measurable spaces
We'll start with the simplest possible example: we'll make $X$ a finite set. Let's say it contains six objects: a pineapple, a rubber duck, a pencil and three leaves. Our measuring device $\mu$ will be a digital scale. Let's also say that we know for certain that $\mu$ can measure:

* the rubber duck together with the pineapple
* the rubber duck together with the pencil
* the three leaves together

Which other combinations of objects can it also measure?
$$
    X = \{🍍,🦆,🖍,🍁,🍃,🍀\}
$$

$$
\begin{align*}
    \{ 🦆, 🍍 \} &\in M \\
    \{ 🦆, 🖍 \} &\in M \\
    \{ 🍁, 🍃, 🍀 \} &\in M
\end{align*}
$$
Let's use the rules of $\sigma$-algebra to find out. From the first two rules, we see that the empty set and the entire $X$ must also be measurable.
$$
\begin{align*}
    \{\} &\in M \\
    \{
        🍍,
        🦆,
        🖍,
        🍁,
        🍃,
        🍀
    \} &\in M
\end{align*}
$$
Now, we apply the third rule which says that the complement of each measurable set is also measurable.
$$
\begin{align*}
    \{
        🖍,
        🍁,
        🍃,
        🍀
    \} &\in M \\
    \{
        🍍,
        🍁,
        🍃,
        🍀
    \} &\in M \\
    \{
        🍍,
        🦆,
        🖍
    \} &\in M
\end{align*}
$$
Then we apply the fourth rule, listing all possible unions of measurable sets.
$$
\begin{align*}
    \{
        🍍,
        🦆,
        🖍
    \} &\in M \\
    \{
        🍍,
        🦆,
        🍁,
        🍃,
        🍀
    \} &\in M \\
    \{
        🦆,
        🖍,
        🍁,
        🍃,
        🍀
    \} &\in M \\
    \{
        🍍,
        🖍,
        🍁,
        🍃,
        🍀
    \} &\in M
\end{align*}
$$
However, we're not done yet. By applying the third rule again, we get even more sets.
$$
\begin{align*}
    \{ 🖍 \} &\in M \\
    \{ 🍍 \} &\in M \\
    \{ 🦆 \} &\in M
\end{align*}
$$
And finally, the union rule gives us the last set that is guaranteed to be measurable.
$$
\begin{align*}
    \{ 🍍, 🖍 \} &\in M
\end{align*}
$$
There you have it, all these sets are measurable and by applying the rules again, we won't get any new sets. We call this the *minimal $\sigma$-algebra* generated by those three sets we started with. Notice how it can't measure each of the leafs individually. Maybe it's because they are too light for the scale. Or because they are actually eldritch lovecraftian monsters waiting to claim our world and eat our souls—

Anyway, this doesn't mean that we can't define a bigger $\sigma$-algebra, one that would also include the individual leaves as measurable sets. In fact, for every space $X$ there exists a so-called *maximal $\sigma$-algebra* which contains each and every subset of $X$ as a measurable set. However, just because we *can* have a maximal $\sigma$-algebra doesn't mean we necessarily want to. Just remember the Banach-Tarski paradox – we certainly don't want the intermediate subsets to be measurable.

<br />

Let's try one more example. This time, let $X$ be a real plane. As the starting measurable sets we'll choose all rectangles. Don't bother rotating them, we'll just use those whose sides are parallel to the $x$ and $y$ axes. Symbolically we can write it like this:
$$
\begin{gather*}
    \big\{ \,
        {[a, b] \times [c, d]} \;\,
        {\big\vert} \;\,
        {a,b,c,d \in \mathbb R,} \;\,
        {a<b,} \;\,
        {c<d} \,
    \big\}
    \subset M
\end{gather*}
$$
As you can see, each rectangle is described by four real numbers. So, there is necessarily an uncountably infinite number of them. Therefore, we won't even bother trying to enumerate all measurable sets. Instead, we'll take a look at a few example sets and try to decide whether they are measurable.


<br />



* any set $M \subset \mathscr{P}(X)$ can be completed to a $\sigma$-algebra

* measure $\mu: M \subset \mathscr{P}(X) \to [0, \infty]$

    * $\mu(\emptyset) = 0$
    * $\mu(A \cup B) = \mu(A) + \mu(B)$ if $A \cap B = \emptyset$
    * $\mu(A_1 \cup A_2 \cup \dots) = \sum_k \mu(A_k)$ if $A_i \cap A_j = \emptyset$

  * measure space
  * measurable function

  * Lebesgue measure on $\mathbb R^n$

