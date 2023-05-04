Download Link: https://assignmentchef.com/product/solved-cs721-advanced-algorithms-and-analysis-programming-assignment-maxima
<br>
Let <em>x</em>, <em>y</em>, and <em>z </em>denote the three coordinate axes in the three dimensional space <em>R</em><sup>3</sup>. A point <em>p </em>∈ <em>R</em><sup>3 </sup>is specified by its coordinates along the three axes: <em>p </em>= (<em>x</em>(<em>p</em>)<em>,y</em>(<em>p</em>)<em>,z</em>(<em>p</em>)).

For <em>p,q </em>∈ <em>R</em><sup>3</sup>, we say that <em>p </em>is <em>dominated </em>by <em>q</em>, if <em>x</em>(<em>p</em>) ≤ <em>x</em>(<em>q</em>), <em>y</em>(<em>p</em>) ≤ <em>y</em>(<em>q</em>) and <em>z</em>(<em>p</em>) ≤ <em>z</em>(<em>q</em>).

Let <em>S </em>= {<em>p</em><sub>0</sub><em>,p</em><sub>1</sub><em>,…,p<sub>n</sub></em><sub>−1</sub>} be a set of <em>n </em>points in <em>R</em><sup>3</sup>. <em>p<sub>i </sub></em>∈ <em>S </em>is called a <em>maximal element </em>of <em>S</em>, if <em>p<sub>i </sub></em>is not dominated by any other element of <em>S</em>. The set of all maximal elements of <em>S </em>is denoted by <em>maxima</em>(<em>S</em>). The <em>maxima problem </em>is: Given <em>S</em>, find <em>maxima</em>(<em>S</em>).

You will write an efficient program to solve this problem, using the C++ or Java Standard Library functions.

One brute-force algorithm to solve this problem is as follows: Compare each point <em>p<sub>i </sub></em>∈ <em>S </em>against all the other points in <em>S </em>to determine if <em>p<sub>i </sub></em>is dominated by any of those points; if <em>p<sub>i </sub></em>is not dominated by any of them, add it to the output set <em>maxima</em>(<em>S</em>). This algorithm takes Θ(<em>n</em>) time for each point <em>p<sub>i</sub></em>, for a total of Θ(<em>n</em><sup>2</sup>) time.

You will implement an efficient algorithm that is expected to run in Θ(<em>n </em>log <em>n</em>) time. The program must be in C++ or Java only. This handout discusses the implementation in C++, using the Standard Template Library (STL). The algorithm consists of three steps.

<ol>

 <li><strong>Input: </strong>The point set <em>S </em>is in an input file. The first line contains the value of <em>n </em>(the number of points). Following that, there will be <em>n </em>lines, each line containing the <em>x</em>, <em>y </em>and <em>z </em>coordinates of one point.</li>

</ol>

The points must be read and stored in an array <em>POINTS</em>[0<em>..</em>(<em>n </em>− 1)] of POINT objects. The <em>POINTS</em>[<em>i</em>] object corresponds to point <em>p<sub>i</sub></em>, and has four fields: the <em>x</em>, <em>y </em>and <em>z</em>-coordinates (all double); the boolean field <em>maximal </em>indicating whether or not the point is maximal.

<ol>

 <li><strong>Sorting: </strong>Sort the points (i.e., the array <em>POINTS</em>) according to their <em>z</em>-coordinates, and reindex them such that <em>z</em>(<em>p</em><sub>0</sub>) ≤ <em>z</em>(<em>p</em><sub>1</sub>) ≤ <em>… </em>≤ <em>z</em>(<em>p<sub>n</sub></em><sub>−1</sub>).</li>

</ol>

The sorting must be done using the sort library function: sort(POINTS, POINTS+n); this requires that you implement the operator&lt;.

<em>p &lt; q </em>if: <em>z</em>(<em>p</em>) <em>&lt; z</em>(<em>q</em>),       or <em>z</em>(<em>p</em>) = <em>z</em>(<em>q</em>) and <em>y</em>(<em>p</em>) <em>&lt; y</em>(<em>q</em>), or <em>z</em>(<em>p</em>) = <em>z</em>(<em>q</em>) and <em>y</em>(<em>p</em>) = <em>y</em>(<em>q</em>) and <em>x</em>(<em>p</em>) <em>&lt; x</em>(<em>q</em>).

<strong>III. Finding the Maxima: </strong>Process the points, one-by-one, in decreasing order of <em>z</em>-coordinates.

Suppose that, at some instant, you have processed the points <em>p<sub>n</sub></em><sub>−1</sub><em>,p<sub>n</sub></em><sub>−2</sub><em>,…,p<sub>i</sub></em><sub>+1</sub>. You must maintain the 2-dimensional maxima of these points in the (<em>x,y</em>)-plane; this will be called <em>maxima</em><sub>2</sub>[(<em>i </em>+ 1)<em>..</em>(<em>n </em>− 1)]. It forms a staircase in the (<em>x,y</em>)-plane.

<strong>CONSIDER </strong>maintaining <em>maxima</em><sub>2</sub>[(<em>i</em>+1)<em>..</em>(<em>n</em>−1)] in a Binary Search Tree (BST) keyed on the <em>y</em>-coordinate; each node of BST corresponds to a point in <em>maxima</em><sub>2</sub>[<em>i</em>+1<em>..n</em>]. As we traverse these nodes in decreasing order of <em>y</em>-coordinate, their <em>x</em>-coordinates increase (thus forming a staircase).

Now we want to process <em>p<sub>i</sub></em>. <em>p<sub>i </sub></em>has a smaller <em>z</em>-coordinate than the points processed so far (namely, <em>p<sub>n</sub></em><sub>−1</sub><em>,p<sub>n</sub></em><sub>−2</sub><em>,…,p<sub>i</sub></em><sub>+1</sub>). So, <em>p<sub>i </sub></em>∈ <em>maxima</em>(<em>S</em>) iff it is not dominated in the (<em>x,y</em>)-plane by any of the points in <em>maxima</em><sub>2</sub>[<em>i </em>+ 1<em>..n</em>]; i.e., <em>p<sub>i </sub></em>is not under the staircase.

The test of whether <em>p<sub>i </sub></em>is dominated by any of these points (in the (<em>x,y</em>)-plane) is performed as follows: Find the point <em>q </em>in BST such that <em>y</em>(<em>q</em>) is just above (or equal to) <em>y</em>(<em>p<sub>i</sub></em>); then <em>p<sub>i </sub></em>∈ <em>maxima</em>(<em>S</em>) iff <em>x</em>(<em>p<sub>i</sub></em>) <em>&gt; x</em>(<em>q</em>).

If <em>x</em>(<em>p<sub>i</sub></em>) <em>&gt; x</em>(<em>q</em>), add <em>p<sub>i </sub></em>to <em>maxima</em>(<em>S</em>); also, we need to update the BST so that it represents <em>maxima</em><sub>2</sub>[<em>i..n</em>]. The update of the BST is done as follows: First, consider the nodes in the BST whose <em>y</em>-coordinates are less than <em>y</em>(<em>p<sub>i</sub></em>), in decreasing order of their <em>y</em>-coordinates; delete them one-by-one, until you come across a point <em>p </em>with <em>x</em>(<em>p</em>) <em>&gt; x</em>(<em>p<sub>i</sub></em>). Finally, insert <em>p<sub>i </sub></em>into the BST.

Each insertion or deletion in a BST takes time Θ(height of the tree). To achieve the Θ(<em>n</em>log<em>n</em>) runtime, the above BST must be a height-balanced binary search tree: At any istant, the height of the tree is Θ(logof number nodes in the tree). One example of such a tree is Red-Black Tree (see Chapter 13 in the text book). You will use the STL data structure map. It is implemented as a Red-Black Tree. In the class, I will explain how to use map.

Variable <em>MaxNum </em>has the number of elements in <em>Maxima</em>(<em>S</em>). Print out <em>MaxNum </em>and <em>Maxima</em>(<em>S</em>). For each point in <em>Maxima</em>(<em>S</em>), also print out its array index (i.e., the index of the point in <em>POINTS </em>array).

Your program should be modular, and contain appropriate procedures/functions. No comments or other documentation is needed. Use meaningful names for all variables.

You will run your program on 10 different sets of points; your program should have a loop for this. All the point sets are in the input file infile.txt.

The name of your program file must be maxima.[cpp or java] (corresponding to C++ or Java programs, respectively); the name of your output file must be outfile.txt.


