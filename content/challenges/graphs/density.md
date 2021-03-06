Title: Graph Density
Category: Graphs
Date: 2016-06-26
Position: 60
Summary: Density is a global graph property.
Disqus_identifier: 8675fa49-density-is-a-global-graph-property

{% include "context_header.md" %}

We have seen one property of nodes, the degree, and one property of edges,
whether or not they are directed. These are called local properties,
because they describe the properties of just one element of a network.

We can also study the network as a whole, and describe the properties that
do not depend on just one node or edge, but on a collection of elements
within the network. One of the simplest global measures is the *edge
density*.

Density
: The **density** of a network is the the number of edges present in the
network divided by the total number of possible edges.

Complete graph
: A **complete graph** is a graph that has all possible edges present,
i.e., its density is equal to $1$.

{% from 'img_desc.html' import img_desc %}
{{ img_desc("density.svg", "Graphs with different densities.")}}

{% include "problem_header.md" %}

For this challenge, you need to read a file representing a graph, and
compute the density of the network.

The input is a file where the first line contains two integers, $n$ and
$m$, defining the number of nodes and edges, respectively. The next $m$
lines each contain two integers, representing two nodes that are joined by
an edge. Assume undirected edges.

Output the density of the network as a single floating point number,
rounded to three decimal places,

Hint
: First, you will need to figure out the maximum possible number of edges
in a graph with $n$ nodes. You can compute it in the following way. First,
start with a graph with $n$ nodes and no edges. Pick one arbitrary node and
count all the edges connecting it to all others, and mark that edge as
'done'. Proceed the same way with all other nodes, picking one unmarked
node and connecting it to all other unmarked nodes, until they are all
marked as 'done'. Keep a running count and finally output the total.

{% include "input_header.md" %}

```
4 4
0 1
0 2
1 3
3 0
```

{% include "output_header.md" %}

```
0.667
```


{% include "solutions_header.md" %}

The solution to this challenge is hosted on
[Github](https://github.com/leotrs/erdos/blob/master/solutions/graphs/density.py).


{% include "question_header.md" %}

1. If you followed the hint to solve the problem above, then you might have
   found yourself computing a sum of numbers like the following: $(n - 1) +
   (n - 2) + (n - 3) +\; ...\; + 2 + 1$.  Can you find a formula for this
   sum, without needing to add up all the numbers every time?  This is a
   very important fact that will be used throughout future problem sets.


{% include "answers_header.md" %}

1. If you followed the hint, you might have realized that the first
    unmarked node allows $n - 1$ edges, the second one allows $n - 2$ and so
    on until the last one only allows $1$ more edge. We need the sum of all
    of these nodes, or $(n - 1) +(n - 2) + (n - 3) +\; ...\; + 3 + 2 + 1$.

    The sum of the first $n$ numbers is well-known and was rediscovered by
    Gauss when he was five years old (or so the story goes). The procedure
    involves reordering the terms to find a constant partial sum. Say we are
    trying to compute the sum of the first $n$ natural numbers.  Then we
    have:

    $$\begin{align*}
    s(n) &= n + (n - 1) +(n - 2) + (n - 3) +\; ...\; + 3 + 2 + 1 \\
         &= n + 1 + (n - 1) + 2 + (n - 2) + 3 +\; ... \\
         &= n + 1 + (n + 1)\:\:\:\:\:\:\:\;\! +(n + 1)\quad\quad\;\;\, ... \\
    \end{align*}
    $$

    As you can see, we are adding up $(n + 1)$ repeatedly. Since we took
    two original terms in the sum to form one instance of $n + 1$, it
    appears a number of times equal to half the original number of terms.
    But there were $n$ terms originally, therefore:

    $$\begin{align*}
    s(n) &= n + 1 + (n + 1) + (n + 1)\; ... \\
         &= (n + 1) \times (n/2)
    \end{align*}
    $$

    Now, we were looking for the sum of the first $n - 1$ natural numbers,
    ie, we want $s(n - 1)$. Substituting in our formula gives
    $n\times(n-1)/2$.  This is the maximum number of edges in an undirected
    graph with $n$ nodes.
