Download Link: https://assignmentchef.com/product/solved-ics-problem-sheet-11
<br>
<strong>Problem 11.1: </strong>fork system call

Consider the following C program:

<h3>1 <em>#include </em><em>&lt;stdio.h&gt; </em>2 <em>#include </em><em>&lt;stdlib.h&gt; </em>3 <em>#include </em><em>&lt;unistd.h&gt;</em></h3>

4

<ul>

 <li>static void action(int m, int n)</li>

 <li>{</li>

 <li>printf(“(%d,%d)
”, m, n);</li>

 <li>if (n &gt; 0) {</li>

 <li>if (fork() == 0) {</li>

 <li>action(m, n-1); 11 exit(0);</li>

 <li>}</li>

 <li>}</li>

 <li>}</li>

</ul>

15

<ul>

 <li>int main(int argc, char *argv[])</li>

 <li>{</li>

 <li>for (int i = 1; i &lt; argc; i++) {</li>

 <li>int a = atoi(argv[i]); 20 action(a, a);</li>

</ul>

21                         }

<h3>22                            return 0;</h3>

23 }

<ol>

 <li>a) Assume the program has been compiled into cnt and that all system calls succeed at runtime. How many child processes are created for the following invocations of the program? Explain how you arrived at your answer</li>

</ol>

<h1><a name="_Toc9583"></a>(1) ./cnt</h1>

<h1><a name="_Toc9584"></a>(2) ./cnt 1</h1>

<ul>

 <li>./cnt 2</li>

 <li>./cnt 1 2 3</li>

</ul>

<ol>

 <li>b) Remove the line exit(0) and compile the program again. What is printed to the terminal and How many child processes are created for the following invocations of the program? Explain how you arrived at your answer.</li>

</ol>

<a href="#_Toc9583">(1) ./cnt                                                                                                                                                                        1</a>

<a href="#_Toc9584">(2) ./cnt                                                                                                                                                                        2</a>

<a href="#_Toc9585">(3) ./cnt 1(4) ./cnt 1 2 3<strong>Problem 11.2: </strong><em>stack frames and tail recursion </em>(1+2 = 3 points)                              2</a>




As discussed in class, function calls require to allocate a stack frame on the call stack. A simple recursive function with a recursion depth <em>n </em>requires the allocation of <em>n </em>stack frames, i.e., the memory complexity grows linear with the recursion depths. In order to improve performance, compilers of high-level programming languages try to optimize the execution of recursive functions.

If a function does a function call as the last action of the function, then this function call can reuse the current stack frame. A recursive function that has this behaviour is called tail recursive. (See also <a href="https://www.youtube.com/watch?v=_JtPhF8MshA">Tail Recursion Explained – Computerphile</a> on YouTube.)

Below is a definition of the function powLin :: Integer -&gt; Integer -&gt; Integer calculating the function <em>powLin</em>(<em>x,n</em>) = <em>x<sup>n</sup></em>.

<ul>

 <li>powLin :: Integer -&gt; Integer -&gt; Integer</li>

 <li>powLin x n</li>

</ul>

<h3>3                              | n == 0            = 1</h3>

4                                       | otherwise = x * powLin x (n-1)

<ol>

 <li>The function powLin has a linear time complexity. Define a recursive function powLog, which has a logarithmic time complexity. You can utilize the following law:</li>

</ol>

if <em>n </em>is even otherwise

<ol>

 <li>Define a tail recursive function powTail with a logarithmic time complexity.</li>

</ol>

Below is a template for your solution providing some test cases.

1 module Main (main) where

2

<h4>3 import Test.HUnit</h4>

4

<ul>

 <li>powLin :: Integer -&gt; Integer -&gt; Integer</li>

 <li>powLin x n</li>

</ul>

<h3>7                                | n == 0 = 1</h3>

8                                       | otherwise = x * powLin x (n-1)

9

<ul>

 <li>powLog :: Integer -&gt; Integer -&gt; Integer</li>

 <li>powLog x n = undefined</li>

</ul>

12

<ul>

 <li>powTail :: Integer -&gt; Integer -&gt; Integer</li>

 <li>powTail x n = undefined</li>

</ul>

15

<ul>

 <li>powLinTests = TestList [ map (powLin 0) [0,1,2,3,10] ~?= [1,0,0,0,0]</li>

 <li>, map (powLin 2) [0,1,2,3,10] ~?= [1,2,4,8,1024]</li>

 <li>, map (powLin 5) [0,1,2,3,10] ~?= [1,5,25,125,9765625]</li>

 <li>]</li>

</ul>

20

<ul>

 <li>powLogTests = TestList [ map (powLog 0) [0,1,2,3,10] ~?= [1,0,0,0,0]</li>

 <li>, map (powLog 2) [0,1,2,3,10] ~?= [1,2,4,8,1024]</li>

 <li>, map (powLog 5) [0,1,2,3,10] ~?= [1,5,25,125,9765625]</li>

 <li>]</li>

</ul>

25

<ul>

 <li>powTailTests = TestList [ map (powLog 0) [0,1,2,3,10] ~?= [1,0,0,0,0]</li>

 <li>, map (powLog 2) [0,1,2,3,10] ~?= [1,2,4,8,1024]</li>

 <li>, map (powLog 5) [0,1,2,3,10] ~?= [1,5,25,125,9765625]</li>

 <li>]</li>

</ul>

30

31 main = runTestTT $ TestList [powLinTests, powLogTests, powTailTests]

Students who prefer to write imperative code in C can solve this problem using the following C template.

<h4>1 #include &lt;assert.h&gt;</h4>

2

<ul>

 <li>static int pow_lin(int x, int n)</li>

 <li>{</li>

 <li>if (n == 0) {</li>

</ul>

<h4>6                                            return 1;</h4>

<ul>

 <li>}</li>

 <li>return x * pow_lin(x, n-1);</li>

 <li>}</li>

</ul>

10

<ul>

 <li>static int pow_log(int x, int n)</li>

 <li>{</li>

</ul>

<h4>13                             return -1;</h4>

14 }

15

<ul>

 <li>static int pow_tail(int x, int n)</li>

 <li>{</li>

</ul>

<h4>18                             return -1;</h4>

19 }

20

<ul>

 <li>int main(void)</li>

 <li>{</li>

 <li>int ns[] = { 0, 1, 2, 3,             10 }; 24       int t0[] = { 1, 0, 0, 0,             0 }; 25          int t2[] = { 1, 2, 4, 8,             1024 };</li>

</ul>

<h3>26                                            int t5[] = { 1, 5, 25, 125, 9765625 };</h3>

27

<ul>

 <li>for (int i = 0; i &lt; sizeof(ns)/sizeof(ns[0]); i++) {</li>

 <li>assert(pow_lin(0, ns[i]) == t0[i]);</li>

 <li>assert(pow_log(0, ns[i]) == t0[i]);</li>

 <li>assert(pow_tail(0, ns[i]) == t0[i]);</li>

 <li>assert(pow_lin(2, ns[i]) == t2[i]);</li>

 <li>assert(pow_log(2, ns[i]) == t2[i]);</li>

 <li>assert(pow_tail(2, ns[i]) == t2[i]);</li>

 <li>assert(pow_lin(5, ns[i]) == t5[i]);</li>

 <li>assert(pow_log(5, ns[i]) == t5[i]);</li>

 <li>assert(pow_tail(5, ns[i]) == t5[i]);</li>

 <li>}</li>

 <li>return 0;</li>

 <li>}</li>

</ul>

<h2><strong>Problem 11.3: </strong>type classes (haskell)                                                                                                     (1+1 = 2 points)</h2>

The following Haskell module defines types for the two-dimensional shapes Rectangle, Circle, and Triangle.

1 module Main (main) where

2

<h3>3 import Test.HUnit</h3>

4

5 data Point = Point { x :: Double, y :: Double } deriving (Show)

6

<h4>7 — Rectangles</h4>

8

9 data Rectangle = Rectangle { p1 :: Point, p2 :: Point } deriving (Show)

10

<h4>11 — Circles</h4>

12

13 data Circle = Circle { m :: Point, r :: Double } deriving (Show)

14

<h4>15 — Triangles</h4>

16

17 data Triangle = Triangle { a :: Point, b :: Point, c :: Point } deriving (Show)

18

<h4>19 — Test cases</h4>

20

<ul>

 <li>pa = Point { x = 0, y = 0 }</li>

 <li>pb = Point { x = 10, y = 10 }</li>

 <li>pc = Point { x = 0, y = 20 }</li>

</ul>

24

<ul>

 <li>rect = Rectangle { p1 = pa, p2 = pb }</li>

 <li>circle = Circle  { m = pa, r = 10 }</li>

 <li>triangle = Triangle { a = pa, b = pb, c = pc }</li>

</ul>

28

<ul>

 <li>tests = TestList [ area rect ~?= 100.0</li>

 <li>, floor (area circle) ~?= 314</li>

 <li>, area triangle ~?= 100.0</li>

 <li>, area (bbox rect) ~?= 100.0</li>

 <li>, area (bbox circle) ~?= 400.0</li>

 <li>, area (bbox triangle) ~?= 200.0</li>

 <li>]</li>

</ul>

36

37 main = runTestTT tests

<ol>

 <li>Define a type class Area declaring a function area, which returns the area covered by a shape type as a Double. The types Rectangle, Circle, and Triangle shall become instances of the Area type class.</li>

 <li>Define a type class BoundingBox extending the Area type class and declaring a function bbox, which returns a Rectangle representing the bounding box of a shape. The types Rectangle, Circle, and Triangle shall become instances of the BoundingBox type class.</li>

</ol>

Your implementation should pass the test cases.