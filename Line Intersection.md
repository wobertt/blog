# How far away can two lines intersect?
Oct 6, 2024
********
**Remark:** This issue occurred in Problem C of ICPC ECNA 2023—the authors got this wrong! You can find more details (warning: spoilers) [here](https://codeforces.com/blog/entry/124293) and [here](https://zhtluo.com/cp/rant-on-incorrect-ecna-2023-c-computational-geometry.html).

>[!question] Problem Statement
>You are given four points $P_1$, $P_2$, $Q_1$, $Q_2$, each with integer coordinates bounded by some constant $M$. Suppose the lines $P_1P_2$ and $Q_1Q_2$ intersect (uniquely) at some point $I$. 
>
>**What's the maximum distance $I$ can be from the origin?**

![[Line Intersection.png | center | 400]]
Here are some multiple-choice options. In each case, $|I|$ is the distance from $I$ to the origin.
1. $|I|$ is $\Theta(M)$ in the worst case.
2. $|I|$ is $\Theta(M^2)$ in the worst case.
3. $|I|$ is $\Theta(M^3)$ in the worst case.
4. $|I|$ can be arbitrarily large in the worst case.

Try it for yourself! My answers start on the next page.
##### **Wrong answer 1:** $|I|$ is $\Theta(M)$ in the worst case.
We can construct a counterexample by choosing two lines far apart and with a small slope difference.
$$
\begin{align}
P_1=(0,\,0) &&Q_1&=(0,\,M) \\
P_2=(M,\,0) &&Q_2&=(M,\,M-1)
\end{align}
$$
![[Line Intersection O(M^2).png | center | 300]]

The line $P_1P_2$ is given by the equation $y=0$ and the line $Q_1Q_2$ is given by the equation $y=M-\frac{1}{M}x$.

The two lines have slope difference $\frac{1}{M}$ and are initially $M$ units apart. So, we expect the lines to intersect at some point with distance $M^2$ from the origin. Indeed, we can calculate their intersection point as $I=(M^2,\,0)$.
##### **Wrong answer 2:** $|I|$ is $\Theta(M^2)$ in the worst case.
If you thought this was the correct answer, you're in good company—the problem authors thought so too!

How can we make $|I|$ even larger? We can't do much to worsen the initial distance—no matter what we do, the two lines are at most $2M$ units apart in the initial box around the origin.

But their slopes can differ by a tiny amount—even smaller than $\frac{1}{M}$! Do you see how?

Let's write the two slopes as $\frac{p_y}{p_x}$ and $\frac{q_y}{q_x}$, where $p_x$ is the distance between $P_1$ and $P_2$ in the $x$-direction, and $p_y$ is the distance in the $y$-direction. $q_x$ and $q_y$ are defined similarly.

Then, the difference in slopes is:
$$
\frac{p_y}{p_x}-\frac{q_y}{q_x}=\frac{p_yq_x-p_xq_y}{p_xq_x}.
$$
To make this as small as possible, we want $p_yq_x-p_xq_y$ to be small and $p_xq_x$ to be large.

These values work,
$$
\begin{align}
p_x&=M-1 && q_x=M \\
p_y&=M &&q_y=M+1
\end{align}
$$
because the slope difference becomes
$$
\frac{p_yq_x-p_xq_y}{p_xq_x}=\frac{M^2-(M-1)(M+1)}{(M-1)(M)}=\frac{1}{M(M-1)}.
$$
Woah! We achieved a slope difference of about $\frac{1}{M^2}$, an order of magnitude smaller than $\frac{1}{M}$.

All that's left is to choose points so that the lines are about $M$ apart:
$$
\begin{align}
P_1&=(0,\,-M) &&Q_1=(0,\,-1) \\
P_2&=(M-1,\,0) &&Q_2=(M,\,M)
\end{align}
$$
![[Line Intersection O(M^3).png | center | 400]]
The lines look parallel—but $P_1P_2$ has slope $\frac{M}{M-1}$ and $Q_1Q_2$ has slope $\frac{M+1}{M}$. Since the lines are $M-1$ units vertically apart at $x=0$, they intersect at $$x=\frac{\text{initial $y$-distance}}{\text{slope difference}}=M(M-1)^2.$$
We can also calculate the $y$-coordinate as $(M+1)(M-1)^2-1$, so we have $|I| \in \Theta(M^3)$. 

Great! We've discovered a way to construct pairs of lines that intersect at distance $\Theta(M^3)$ from the origin. But, could there be something even larger?
<div style="page-break-after: always; visibility: hidden"> pagebreak </div>

##### **$\Theta(M^3)$ is the correct worst-case bound.**
Firstly, a crude lower bound for the magnitude of the slope difference is $$\left|\frac{p_yq_x-p_xq_y}{p_xq_x}\right| \ge \frac{1}{4M^2},$$
because the numerator is at least $1$ and each term in the denominator is at most $2M$. We can use this to derive bounds on $|x_I|$ and $|y_I|$ for the intersection point $I=(x_I, y_I)$.

As before, the lines are at most $2M$ units vertically apart at $x=0$, so $|x_I|$ is at most $8M^3$. To obtain the identical bound $|y_I| \le 8M^3$, we can swap $x$ and $y$-coordinates and repeat the same analysis. So, $|I|$ is indeed $\Theta(M^3)$ in the worst case.

**Aside:** You may notice that I've missed some edge cases: I implicitly assumed none of $p_x$, $p_y$, $q_x$, $q_y$, and $p_yq_x-p_xq_y$ are zero. Fortunately, this is not a problem. If any of the first four quantities are zero, then we are dealing with horizontal/vertical lines—these are easy to check separately. If the last quantity is zero, then $P_1P_2$ and $Q_1Q_2$ are parallel. We ignore this case because we want a unique intersection point.
