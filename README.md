Download Link: https://assignmentchef.com/product/solved-cs372-lab-1-using-r-to-visualize-the-runtime-of-fibonacci-algorithms
<br>






In this lab, we will evaluate and visualize empirical runtime of Fibonacci algorithms. Then we will examine if the runtime growth is consistent with theoretical analysis.

<h1>1        Setup the environment</h1>

We will setup the R environment to run C++ programs conveniently to take advantage of the powerful plotting functions in R.

<h2>1.1      Install R, Rstudio, and R package Rcpp</h2>

All software packages are free to download. You can skip the following steps if you use CS Linux computers, as they are already installed on CS computers.

For your home computers, you need to install them:

<ol>

 <li>Install R from www.r­project.org</li>

 <li>Install Rstudio from www.rstudio.com</li>

 <li>Install package Rcpp within R</li>

</ol>

<h2>1.2      Configuration of the search path to R</h2>

Configure the search path to include the R directory on CS Linux computers. Insert the following R configuration line to the end of the .cshrc file in your home directory:

source /home/unsupported/linux64/config/cshrc.R

<h1>2        Evaluate and visualize the runtime of a C++ program in R</h1>

The purpose of running C++ program within R is to utilize the powerful visualization and timing functions in R to conduct quick performance evaluation on the C++ program with minimal amount of programming.

The following are required steps to integrate R part into the C++ program and run it in R or Rstudio. You can do all the steps within the Rstudio integrated development environment:

<ol>

 <li>Develop your C++ program (”fib.cpp”) as normal</li>

 <li>Test and debug your C++ code</li>

 <li>Insert a comment line right before the function you want to run in R:</li>

</ol>

// [[Rcpp::export]] int fib1(int n)

{ …

}

<ol start="4">

 <li>Insert R code to measure the runtime of your C++ code

  <ul>

   <li>Use R function time() to accurately count time charged to your program, not other concurrent processes on the same computer.</li>

  </ul></li>

 <li>Insert R code to visualize the result of your C++ code

  <ul>

   <li>Use R function plot() to visualize the result as a curve.</li>

  </ul></li>

 <li>Invoke R or Rstudio</li>

 <li>If your code uses C++11 features, type in the following command in R: R command to enable c++11 features</li>

</ol>

&gt; Sys.setenv(”PKG_CXXFLAGS”=”-std=c++11”)

If you copy and paste from the above line, the double quote may have to be re­entered as this document code them differently from R.

<ol start="8">

 <li>Run the R code portion within your C++ code using</li>

</ol>

R command to run the R portion of fib.cpp

&gt; Rcpp::sourceCpp(”fib.cpp”)

or equivalently, you can push the “source” button within Rstudio without typing in the command.

<h1>3        Example: computing Fibonacci numbers</h1>

See example fib.cpp fib.cpp

<ul>

 <li>#include &lt;iostream&gt;</li>

 <li>using namespace std;</li>

</ul>

3

<ul>

 <li>// [[Rcpp::export]]</li>

 <li>int fib1(int n)</li>

 <li>{</li>

 <li>if(n == 0) return 0;</li>

 <li>if(n == 1) return 1;</li>

</ul>

9

<ul>

 <li>return fib1(n-1) + fib1(n-2);</li>

 <li>}</li>

</ul>

12

13 // [[Rcpp::export]] 14 bool test_fib1()

<ul>

 <li>{</li>

 <li>bool passed = true;</li>

 <li>int ns[] = {0, 1, 2, 3, 4, 5, 6};</li>

 <li>int Fs[] = {0, 1, 1, 2, 3, 5, 8};</li>

 <li>for(int i=0; i&lt;7; i++) {</li>

 <li>if(fib1(ns[i]) != Fs[i]) {</li>

 <li>passed = false;</li>

 <li>break;</li>

 <li>}</li>

 <li>}</li>

</ul>

<table width="571">

 <tbody>

  <tr>

   <td width="571">if(passed) { cout &lt;&lt; ”test_fib1() passed. Congratulations!” &lt;&lt; endl;} else { cout &lt;&lt; ”test_fib1() failed!” &lt;&lt; endl;}return passed;}int main(){ test_fib1(); return 0;}// Above is regular C++ portion// —————————————————–// Below is the R portion to visualize the performance// You can include R code blocks in C++ files processed // with sourceCpp (useful for testing and development). // The R code will be automatically run after C/C++ // compilation. /*** Rk &lt;- 10 ns &lt;- 34+(1:k)runtime &lt;- vector(length=k)for(i in 1:k) {n &lt;- ns[i]runtime[i] &lt;- system.time(fib1(n))[”user.self”]}plot(ns, runtime, type=”b”, xlab=”n”, ylab=”runtime (second)”)grid(col=”blue”)*/</td>

  </tr>

 </tbody>

</table>

25

26

27

28

29

30

31

32

33

34

35

36

37

38

39

40

41

42

43

44

45

46

47

48

49

50

51

52

53

54

55

56

57

58

59

60

61

62

<h1>4        Implement and evaluate linear time Fibonacci algorithm</h1>

<ol>

 <li>Implement the linear time Fibonacci algorithm int fib2(int) from the lecture notes in C++. Name the C++ file fib-linear.cpp.</li>

 <li>Write a test function in C++ to check the results when <em>n </em>=0<em>,</em>1<em>,</em>2<em>,</em>3<em>,</em>4<em>,</em>5<em>,</em>6<em>,</em>7<em>,</em>8<em>,</em>9</li>

 <li>Create a main function in the C++ file to call the test function you just devel­oped. Make sure the test is passed.</li>

 <li>Develop R code to visualize the runtime in the same C++ source code filefib-linear.cpp.</li>

 <li>Does the runtime grow linearly as input number <em>n </em>increases?</li>

 <li>How many times is the linear algorithm faster than the exponential algorithmin cpp on the same input?</li>

 <li>Write a lab report that describes your work done in the following sections:

  <ul>

   <li>Introduction (define the background and the problem),</li>

   <li>Methods (provide the solutions),</li>

   <li>Results (show the numbers and figures),</li>

   <li>Discussions (implications and issues),</li>

   <li>Conclusions (summarize the lab and point to a future direction).</li>

  </ul></li>

 <li>Submit the program and your report online.</li>

</ol>