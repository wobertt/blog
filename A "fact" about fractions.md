Nov 29, 2024
****
I was checking my work on a problem recently[^1], where I reached the equation
$$
-\frac{1}{8}-\frac{3}{4}-\frac{3}{2}+\frac{1}{24}\stackrel{?}{=} -\frac{7}{3}.
$$
At this point I concluded that I must have made a mistake. Without even calculating, I knew the left side had denominator $24$, but the right side had denominator $3$.

...Or so I thought. Actually, the two sides are equal.

Is it intuitive that the denominator, in lowest terms, can decrease? Maybe—the example
$$
\frac{1}{3} + \frac{1}{6} = \frac{1}{2}
$$
is fairly common.

But I had to ask: why did I make this wrong assumption? Is there some other true statement we can conclude?

##### An Investigation

>[!question] Question.
>Are there integers $a$, $b$, $c$ that make the following equation true?
>$$8a + 4b + 2c + 1 = 56$$

Clearly, the answer is no: taking both sides modulo $2$ gives $0 \equiv 1 \pmod 2$, which is always false. This idea, wrongly applied to the fractional example, caused me to dismiss a correct solution.
<div style="page-break-after: always; visibility: hidden"> pagebreak </div>

But, returning to the original problem, there is something we can say:

>[!info] Valid Denominators.
>Find all possible denominators, in simplest form, of
>$$\frac{a}{8} + \frac{b}{4} + \frac{c}{2} + \frac{d}{24}$$
>where $a, b, c, d \in \mathbb{Z}$.

The answer is **all divisors of $24$.** Notice that
$$
\frac{a}{8} + \frac{b}{4} + \frac{c}{2} + \frac{d}{24} = \frac{3a+6b+12c+d}{24},
$$
and the numerator can be any integer. So, the possible denominators are those that divide $24$.

In general, given an expression $\frac{p_1}{q_1} + \frac{p_2}{q_2} + \dots + \frac{p_n}{q_n}$, all we can say is that the denominator in lowest terms is a divisor of $\operatorname{lcm}(q_1, \dots, q_n)$.

This isn't a very strong statement, but at least it's something. For example, we can quickly show that the following equation has no solutions for $a, b \in \mathbb{Z}$.
$$
\frac{a}{8}+\frac{b}{3}=\frac{1}{48}
$$

[^1]: The problem was finding the partial fraction decomposition of $\frac{1+x+x^{2}}{\left(1-x\right)^{3}\left(1+x\right)}$. I found the correct answer and plugged in $x=2$ to check, leading to the main equation.