---
title: "matrix application in current calculation"
tags: "Linear_Algebra"
layout: "article"
article_header:
  type: cover
  image:
    src: /linear_algebra_cover.jpg
---

{:toc}

# Transform to matrices

Suppose we have a current graph like this:

<img src="{{site.baseurl}}/assets/images/linear_algebra/post1-pic1.png">

Arrows stand for the direction of current flow. If we encode all information in this graph into a matrix, we will get the matrix P:


$$
P=\left[\begin{matrix} -1&1&0&0 \\0&-1&1&0\\-1&0&1&0\\-1&0&0&1\\0&0&-1&1     \end{matrix}\right]
$$


In matrix P, column 1~4 symbolizes the node 1~4 in the current graph, while row 1~5 symbolizes the edges numbered 1~5. A "-1" means this node in this column has an edge pointing outside. Similarly, a "1" means an edge pointing inside to the node. 

There's some interesting characters for matrix P. For instance, node 1,2, and 3 form a "short cut"-the edge 1->3 is a substitute for edge 1->2 plus edge 2->3. Consequently, the rank of the first three rows is lower than 3. It can be proofed as a theorm that every graph containing a "short cut" like this, will cause the rank of the matrix of the graph lower than the number of its nodes.

# Electric potential 

So far, we can extract the information in a current graph as a matrix. When it comes to the calculating current intensity, a concept termed electric potential kicks in. In short, this concept represents the voltage difference between a node and the ground. Assume the potential of each node is $$x_1, x_2, x_3, x_4$$ respectively. If the current is stable-no current flow in the circuit, equations below can be implicated:


$$
Px=0\\\\\left[\begin{matrix} -1&1&0&0 \\0&-1&1&0\\-1&0&1&0\\-1&0&0&1\\0&0&-1&1     \end{matrix}\right]·\left[\begin{matrix} x_1 \\x_2\\x_3\\x_4     \end{matrix}\right]=\left[\begin{matrix} 0 \\0\\0\\0     \end{matrix}\right]
$$


A general solution is derived by solving this equation:


$$
x=c\left[\begin{matrix}1 \\1\\1\\1     \end{matrix}\right]
$$


According to the result, there is only one case that allows no current in the graph-all nodes are at the same potential. Let's broaden this case generally. If the initial current is not zero, the equation and the solution mentioned above will be changed:


$$
Px=b\\
\\x=x^*+c\left[\begin{matrix} 1 \\1\\1\\1     \end{matrix}\right]
$$


$$x^*$$ stands for any certain solution for $$Px=b$$. However, multiple solutions is not expected. In practice, we assume node 4 is on the ground, which means it at 0 potential in physics. This assumption reveals that we usually expect a 0-potential point in the circuit, in order to analyze real voltage on every part of the circuit. In terms of matrix theory, that is to set $$x_4$$ as zero for making the equation $$Px=0$$ have single analytic solution. Because of this, for all vector b, a common equation $$Px=b$$ only has one solution, which is the state of circuit we want.

# Solving current intensity 

As mentioned above, the matrix P plays a significant role in calculating electric potentials. Furthermore, it is also useful to solve for current intensity. Firstly, we apply a transposition on matrix P, solving for the homogeneous solution:


$$
P^Ty=0
\\\left[\begin{matrix} -1&0&-1&-1&0\\1 &-1& 0& 0 &0\\0& 1 &1 &0 &-1\\0&0&0&1&1     \end{matrix}\right]\left[\begin{matrix} y_1 \\y_2\\y_3\\y_4 \\y_5    \end{matrix}\right] = \left[\begin{matrix} 0\\0\\0\\0\\0     \end{matrix}\right]
$$


$$y_i$$ stands for the intensity on edge i in the circuit graph. If we write this matrix equation as a simpler form, it could be as this:


$$
\left\{\begin{aligned}
-y_1-y_3-y_4 & = & 0 \\
y_1-y_2 & = & 0 \\
y_2+y_3-y_5 & = & 0\\
y_4+y_5 & = & 0
\end{aligned}    \right.
$$


If you are fimilar with physics, these are exactly the expressions called [Kirchhoff's Law](https://www.google.com/search?q=Kirchhoff%27s+law&oq=Kirhhoff%27s+law&aqs=chrome..69i57j0i13l9.302j0j7&sourceid=chrome&ie=UTF-8). Fortuantely, these equations are easy to solve. By simply analyzing the dimention of solution, including some basic linear algebra knowledge, we can get the basic solutions as above:


$$
\left[\begin{matrix} 1 \\1\\-1\\0 \\0    \end{matrix}\right],\left[\begin{matrix} 0 \\0\\1\\-1 \\1    \end{matrix}\right]
$$


Most interestingly, these two solutions occasionally  match two "short cuts"--①②③ and ③④⑤. Generally speaking, including "short cuts", each kind of undirected cycle will add a solution to the linear equations. But why does the "short cut" ①②④⑤ disappear? Because this "short cut" can be composed by ①②③ and ③④⑤-in another word, it's a combination of other solutions instead of a basic solution. 

In a word, one more solution in the linear algebra equations, means one more undirected cycle in the current graph. Linear algebra can bring us a novel insight towards the laws in electricity and current. 

# References

[MIT linear algebra class, Gilbert Strang](https://www.tjupt.org)

