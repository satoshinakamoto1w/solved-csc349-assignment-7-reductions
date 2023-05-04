Download Link: https://assignmentchef.com/product/solved-csc349-assignment-7-reductions
<br>
We can show that a problem <em><sub>B </sub></em>is at least as hard as a problem <em><sub>A </sub></em>by showing that an algorithm that solves <em><sub>B </sub></em>can be used to solve <em><sub>A</sub></em>. In this assignment, you’ll develop programs that use each other to solve <sub>NP</sub>-Complete problems.

<strong>Deliverables:</strong>

<strong>GitHub Classroom: </strong><a href="https://classroom.github.com/a/m2Xn4Y9f">https://classroom.github.com/a/m2Xn4Y9f</a>

<strong>Required Files:                   </strong>compile.sh, run.sh

<strong>Optional Files:                           </strong>*.py, *.java, *.clj, *.kt, *.js, *.sh

<h1>Part 1: Subgraph Isomorphism</h1>

Recall that two graphs, <em>G </em>= (<em>V<sub>G</sub>,E<sub>G</sub></em>) and <em>H </em>= (<em>V<sub>H</sub>,E<sub>H</sub></em>), are <em>isomorphic </em>if there exists a bijection <em>f </em><sub>: <em>V</em></sub><em><sub>G </sub></em>→ <em><sub>V</sub></em><em><sub>H </sub></em>such that two vertices <em><sub>u,v </sub></em>∈ <em><sub>V</sub></em><em><sub>G </sub></em>are adjacent if and only if the corresponding vertices <em>f</em><sub>(<em>u</em>)<em>,f</em>(<em>v</em>) ∈ <em>V</em></sub><em><sub>H </sub></em>are also adjacent. In other words, two graphs are isomorphic if they have the same shape<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>, even if their vertices are named differently.

The Subgraph Isomorphism problem asks whether, given two graphs <em><sub>G </sub></em>and <em><sub>H</sub></em>, <em><sub>G </sub></em>contains a subgraph isomorphic to <em><sub>H</sub></em>. For example, given:

<em>G</em>:<em>H</em>:

Here, <em><sub>G </sub></em>contains a subgraph isomorphic to <em><sub>H</sub></em>. Note that the reverse is not necessarily true: <em><sub>H </sub></em>does not contain a subgraph isomorphic to <em><sub>G</sub></em>. Further note that every graph contains a subgraph isomorphic to itself. The Subgraph Isomorphism problem is known to be <sub>NP</sub>-Complete; it is among the hardest problems to solve for which a solution can still be verified efficiently. The given subgraph_isomorphism.py implements a naïve, brute force algorithm<sup>2 </sup>to solve this problem.

This implementation can be invoked from the command line, given two files containing edge lists:

&gt;$ python3 subgraph_isomorphism.py graph_g.txt graph_h.txt Isomorphic vertices:

0, 1, 2, 3 &gt;$ echo $?

0

…if <em><sub>G </sub></em>contains a subgraph isomorphic to <em><sub>H</sub></em>, subgraph_isomorphism.py prints the vertices of that subgraph and terminates with exit status 0. If not, it terminates with exit status 1:

&gt;$ python3 subgraph_isomorphism.py graph_g.txt graph_h.txt No isomorphic vertices.

&gt;$ echo $?

1

<sup>1</sup>“isomorphic”, from Greek, “<sub>ι</sub><em>́</em><sub>σο</sub><em>́µ</em><sub>ορφος</sub>”, meaning “of equal form”

<sup>2</sup>It’s not the most efficient known approach, but it is straightforward to read.

Alternatively, both the Subgraph Isomorphism implementation and its associated graph data structure can be imported like any other Python module:

1import graph

2import subgraph_isomorphism as si

3

4graph_g = graph.Graph()

5graph_h = graph.Graph()

6

7subgraph = si.isomorphic_subgraph(graph_g, graph_h)

…if <em><sub>G </sub></em>contains a subgraph isomorphic to <em><sub>H</sub></em>, subgraph_isomorphism.isomorphic_subgraph returns such a subgraph. If not, it returns None.

<h1>Part 2: Clique to Subgraph Isomorphism</h1>

A <em>clique </em>is a subgraph within which every vertex is connected to every other vertex. The Clique problem asks whether, given a graph <em><sub>G </sub></em>and an integer <em><sub>k</sub></em>, <em><sub>G </sub></em>contains a clique on <em><sub>k </sub></em>vertices. For example, recall the following graph from above:

This graph contains cliques on <em><sub>k </sub></em><sub>= 1</sub>, <em><sub>k </sub></em><sub>= 2</sub>, and <em><sub>k </sub></em><sub>= 3 </sub>vertices, but not any cliques on <em><sub>k </sub></em><sub>= 4 </sub>vertices.

In your programming assignment of choice per Assignment 1, implement an algorithm that, given a graph <em><sub>G </sub></em>and a natural number <em><sub>k</sub></em>, uses the given Subgraph Isomorphism implementation to determine whether or not <em>G </em>contains a clique on <em><sub>k </sub></em>vertices.

The specific input and output format of this implementation is up to you, as your code is the only code that will make use of it. The only requirement is that you <em>must </em>use the given Subgraph Isomorphism implementation; that is, your pseudocode should look something like:

Clique(<em>G </em>← (<em>V,E</em>)<em>,k</em>)

<strong>Input: </strong>A graph <em><sub>G </sub></em>and a natural number <em><sub>k</sub></em>

<strong>Output: </strong>Whether or not <em><sub>G </sub></em>contains a clique on <em><sub>k </sub></em>vertices

…

SubgraphIsomorphism<sub>(<em>…</em>)</sub>

…

…thereby reducing Clique to Subgraph Isomorphism, demonstrating that Subgraph Isomorphism is at least as hard as Clique is.

<h1>Part 3: <sub>3</sub>-SAT to Clique</h1>

The <em>boolean satisfiability problem</em>, or “SAT”, asks whether, given a proposition, there exists an assignment of truth values to propositional variables that satisfies the proposition. The variation known as “<sub>3</sub>-SAT” restricts the given propositions to conjunctive normal form with exactly <sub>3 </sub>literals per clause.

2 of 4

3-SAT can be reduced to Clique by representing the proposition as a graph, where:

<ul>

 <li>A vertex <em><sub>p</sub></em><em><sub>i </sub></em>represents a literal <em><sub>p </sub></em>in clause <em><sub>i</sub></em>.</li>

 <li>Two vertices <em><sub>m</sub></em><em><sub>i </sub></em>and <em><sub>n</sub></em><em><sub>j </sub></em>are connected by an edge if and only if <em><sub>i </sub></em>6<sub>= <em>j </em></sub>and <em><sub>m</sub></em><em><sub>i </sub></em>6≡¬<em><sub>n</sub></em><em><sub>j </sub></em>(<em><sub>m </sub></em>and <em><sub>n </sub></em>may or may not be the same literal).</li>

</ul>

In other words, the edges of this graph indicate potential non-conflicting assignments of truth values between different clauses. For example, given:

(<em>p </em>∨ <em>q </em>∨ <em>r</em>) ∧ (¬<em>p </em>∨ <em>r </em>∨¬<em>p</em>) ∧ (¬<em>r </em>∨¬<em>r </em>∨¬<em>r</em>)

…this proposition is represented by:

<table width="433">

 <tbody>

  <tr>

   <td width="34"><em>p</em></td>

   <td width="26"><em>q</em></td>

   <td width="19"><em>r</em></td>

   <td width="83">(<em>p </em>∨ <em>q </em>∨ <em>r</em>)</td>

   <td width="93">(¬<em>p </em>∨ <em>r </em>∨¬<em>p</em>)</td>

   <td width="101">(¬<em>r </em>∨¬<em>r </em>∨¬<em>r</em>)</td>

   <td width="76"> </td>

  </tr>

  <tr>

   <td width="34"><em>T</em></td>

   <td width="26"><em>T</em></td>

   <td width="19"><em>T</em></td>

   <td width="83"><em>T</em></td>

   <td width="93"><em>T</em></td>

   <td width="101"><em>F</em></td>

   <td width="76"><strong>F</strong></td>

  </tr>

  <tr>

   <td width="34"><em>T</em></td>

   <td width="26"><em>T</em></td>

   <td width="19"><em>F</em></td>

   <td width="83"><em>T</em></td>

   <td width="93"><em>F</em></td>

   <td width="101"><em>T</em></td>

   <td width="76"><strong>F</strong></td>

  </tr>

  <tr>

   <td width="34"><em>T</em></td>

   <td width="26"><em>F</em></td>

   <td width="19"><em>T</em></td>

   <td width="83"><em>T</em></td>

   <td width="93"><em>T</em></td>

   <td width="101"><em>F</em></td>

   <td width="76"><strong>F</strong></td>

  </tr>

  <tr>

   <td width="34"><em>T</em></td>

   <td width="26"><em>F</em></td>

   <td width="19"><em>F</em></td>

   <td width="83"><em>T</em></td>

   <td width="93"><em>F</em></td>

   <td width="101"><em>T</em></td>

   <td width="76"><strong>F</strong></td>

  </tr>

  <tr>

   <td width="34"><em>F</em></td>

   <td width="26"><em>T</em></td>

   <td width="19"><em>T</em></td>

   <td width="83"><em>T</em></td>

   <td width="93"><em>T</em></td>

   <td width="101"><em>F</em></td>

   <td width="76"><strong>F</strong></td>

  </tr>

  <tr>

   <td width="34"><em>F</em></td>

   <td width="26"><em>T</em></td>

   <td width="19"><em>F</em></td>

   <td width="83"><em>T</em></td>

   <td width="93"><em>T</em></td>

   <td width="101"><em>T</em></td>

   <td width="76"><strong>T</strong></td>

  </tr>

  <tr>

   <td width="34"><em>F</em></td>

   <td width="26"><em>F</em></td>

   <td width="19"><em>T</em></td>

   <td width="83"><em>T</em></td>

   <td width="93"><em>T</em></td>

   <td width="101"><em>F</em></td>

   <td width="76"><strong>F</strong></td>

  </tr>

  <tr>

   <td width="34"><em>F</em></td>

   <td width="26"><em>F</em></td>

   <td width="19"><em>F</em></td>

   <td width="83"><em>F</em></td>

   <td width="93"><em>T</em></td>

   <td width="101"><em>T</em></td>

   <td width="76"><strong>F</strong></td>

  </tr>

 </tbody>

</table>

Since edges represent non-conflicting, inter-clause assignments, and we must make a set of assignments such that at least one literal in every clause is true, and none of our assignments can conflict with each other, we need to find a clique on <em><sub>k </sub></em>vertices within this graph, where <em><sub>k </sub></em>is the number of clauses in the given proposition. The vertices of that clique then indicate the satisfying assignments; if no such clique can be found, then no satisfying assignment exists. In the example above, finding a clique on <em><sub>k </sub></em><sub>= 3 </sub>vertices yields that <em><sub>p </sub></em><sub>≡ <em>F</em></sub>, <em>q </em><sub>≡ <em>T</em></sub>, and <em><sub>r </sub></em><sub>≡ <em>F </em></sub>will satisfy the given proposition, a fact that is verified by the corresponding truth table: <em>conjunction</em>

In your programming language of choice per Assignment 1, implement an algorithm that, given a proposition in CNF with exactly <a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a> literals per clause, uses your Clique implementation to determine whether or not the proposition is satisfiable.

You <em>must </em>make use of your Clique implementation to solve <sub>3</sub>-SAT, and, by extension, you <em>must </em>make use of the given Subgraph Isomorphism implementation. By doing so, you have demonstrated that:

<ul>

 <li>Subgraph Isomorphism is at least as hard as Clique.</li>

 <li>Clique is at least as hard as <sub>3</sub>-SAT.</li>

</ul>

Additionally, we have that:

<ul>

 <li><sub>3</sub>-SAT is known to be <sub>NP</sub>-Complete, and both Clique and Subgraph Isomorphism are in <sub>NP</sub>.</li>

</ul>

…therefore, both Subgraph Isomorphism and Clique are also <sub>NP</sub>-Complete.

You may assume that the proposition will be well-formed, using ‘~’ to indicate negation, ‘&amp;’ to indicate conjunction, and ‘|’ to indicate disjunction<sup>3</sup>. You may also assume that all propositional variables will be one of the <sub>26 </sub>lowercase English letters, and that a single space will appear between all literals and operators. For example, the above proposition would be represented as:

( p | q | r ) &amp; ( ~p | r | ~p ) &amp; ( ~r | ~r | ~r )

Your program must accept as a command line argument the name of a file containing a proposition as described above, then print to stdout its satisfiability according to the following format:

<ul>

 <li>If the proposition is satisfiable, the satisfying assignments must appear on a single line, sorted in alphabetical order by their propositional variables.</li>

 <li>If the proposition is unsatisfiable, a message must indicate as such. For example:</li>

</ul>

&gt;$ ./compile.sh

&gt;$ ./run.sh in1.txt Satisfying assignment:

~p, q, ~r

You may further assume that the satisfying assignment, if one exists, will be unique<a href="#_ftn3" name="_ftnref3"><sup>[3]</sup></a>. Your program will be tested using diff, so its printed output must match <em>exactly</em>.


