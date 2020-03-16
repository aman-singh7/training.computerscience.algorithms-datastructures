# Algorithms and Data Structures

- My notes from UC San Diego MicroMasters Program, [Algorithms and Data Structures](https://www.edx.org/micromasters/ucsandiegox-algorithms-and-data-structures) and all the readings that I made in parallel (see [references](#references) below)
- My anki flashcards:
    - [Anki flashcards package](https://github.com/hamidgasmi/AlgorithmsDataStructures/blob/master/algorithms-datastructures_ankiflashcard.apkg): 34 cards
    - [Install Anki](https://apps.ankiweb.net/)

## Table of Contents
- [Prerequisites](#prerequisites)
- [Algorithm Design and Techniques](#algorithm-design-and-techniques)
- [Data Structures Fundamentals](#data-structures-fundamentals)
- [Graph Algorithms](#graph-algorithms)
- [NP-Complete Problem](#np-complete-problem)
- [String Processing and Pattern Matching Algorithms](#string-processing-and-pattern-matching-algorithms)
- [Dynamic Programming: Applications In Machine Learning and Genomics](#dynamic-programming-applications-in-machine-learning-and-genomics)
- [Graph Algorithms in Genome Sequencing ](#graph-algorithms-in-genome-sequencing)
- [References](#references)

## Prerequisites

<details>
<summary>Proof by Induction</summary>

- It allows to prove a statement about an arbitrary number n by:
    - 1st proving it's true when n is 1 and then 
    - assuming it's true for n = k and showing it's true for n = k + 1
- [For more details](http://comet.lehman.cuny.edu/sormani/teaching/induction.html)

</details>

<details>
<summary>Proofs by contradiction</summary>

- It allow to prove a proposition is valid (true) by showing that assuming the proposition to be false leads to a contradiction
- [For more details](https://en.wikipedia.org/wiki/Proof_by_contradiction)

</details>

<details>
<summary>Logarithms</summary>

- See [this](https://www.khanalscademy.org/math/algebra2/x2ec2f6f830c9fb89:logs/x2ec2f6f830c9fb89:log-intro/a/intro-to-logarithms)

</details>

<details>
<summary>Iterated logarithm</summary>

- It's symbolized: **log∗(n)**: 
- It's the number of times the logarithm function needs to be applied to n before the result is ≤ 1
-      Log*(n) = 0 if n ≤ 1 = 1 + Log* (Log (n)) if n > 1
-      n                           Log*(n)
       n = 1                        0
       n = 2                        1
       n ∈ {3, 4}                   2
       n ∈ {5,..., 16}              3
       n ∈ {17, ..., 65536}         4
       n ∈ {65537,..., 2^65536}     5

</details>

<details>
<summary>Recursion</summary>

- To [Get Started](https://www.khanacademy.org/computing/computer-science/algorithms/recursive-algorithms/a/recursion)
- Stack optimization and Tail Recursion

</details>

<details>
<summary>T(n)</summary>

- It's the number of lines of code executed by an algorithm

</details>    


## Algorithm Design and Techniques

<details>
<summary>Test Cases</summary>

- **Boundary** values
- **Biased**/**Degenerate** tests cases
    - They're particular in some sense
    - See example for each data structure below
- **Randomly** generated cases and **large** dataset:
    - It's to check random values to catch up cases we didn't think about
    - It's also to check how long it takes to process a large dataset
    - Implement our program as a function **solve(dataset)**
    - Implement an additional procedure **generate()** that produces a random/large dataset 
    - E.g., if an input to a problem is a sequence of integers of length 1 ≤ n ≤ 10^5, then: 
        - Generate a sequence of length 10^5, 
        - Pass it to our solve() function, and 
        - Ensure our algorithm outputs the result quickly: we could measure the duration time
- **Stress** testing:
    - Implement a slow but simple and correct algorithm
    - Check that both programs produce the same result (this is not applicable to problems where the output is not unique) 
    - Generate random test cases as well as biased tests cases
- When dealing with **numbers**:
    - Think about number size: Int. Long, ... ?
    - If there is any division: division by 0; Precision?
    - Integers Biased cases: a **Prime/Composite** number; an **Even/Odd** number
- When dealing with **String**:
    - Biased/Degenerate tests: 
        - Empty string
        - A strings that contains a sequence of a single letter (“aaaaaaa”) or 2 letters ("abbaabaa") as opposed to those composed of all possible Latin letters
    - Encoding (ASCII, UTF-8, UTF-16)?
    - Special characters
- When dealing with **arrays/lists**:
    - Biased/Degenerate tests: 
        - It's empty
        - It contains only small numbers or a small range of large numbers
    - It contains **few** elements: 1, 2
    - It contains **many** elements: 10^6
    - It contains same elements: min value only (0 for integers), max value only (2^32 for integers), any specific value
- When dealing with **Trees**:
    - Biased/Degenerate tests: a tree which consists of a linked list, binary trees, stars
- When dealing with **Graphs**:
    - Biased/Degenerate tests: a graph which consists of a linked list, a tree, a disconnected graph, a complete graph, a bipartite graph

</details>

<details>
<summary>Big O vs. Big-Ω vs. Big-Θ</summary>

- **Big-Ω** (Omega):
    - It's a lower bound of a function
    - A function f(n) = Ω(g(n)), if there're positive constants C and k, such that 0 ≤ C g(n) ≤ f(n) for all n ≥ k
    - E.g., f(n) = n^2 + n = Ω(n) because n ≤ f(n) for n ≥ 1
    - ![Example](https://xlinux.nist.gov/dads/Images/omegaGraph.gif)
    - It's NOT used in the industry
- **Big-O**:
    - It's an upper bound of a function
    - A function f(n) = O(g(n)), if there're positive constants C and k, such that 0 ≤ f(n) ≤ C g(n) for all n ≥ k
    - E.g., f(n) = n^2 = O(n^3) because f(n) ≤ n^3 for k ≥ 1
    - ![Example](https://upload.wikimedia.org/wikipedia/commons/8/89/Big-O-notation.png)
    - It's used in the Industry with a different definition (see below, Big-Theta)
- **Big-Θ** (Theta):
    - A function f grows at same rate as a function g
    - If f = Ω(g) and f = O(g)
    - E.g., f(n) = n^2 + n = Θ(n^2) because n^2 ≤ f(n) ≤ n^2 for k ≥ 1
    - It's used in the industry as Big-O
- **Small-o**:
    - A function f is o(g) if f(n)/g(n) → 0 as n → ∞
    - f grows slower than g
    - It's NOT used in the industry
- [For more details](https://www.khanacademy.org/computing/computer-science/algorithms/asymptotic-notation/a/asymptotic-notation)

</details>

<details>
<summary>Time Complexity</summary>

- It describes the rate of increase of an algorithm
- It describes how an algorithm scales when input grows
- Big-O notation is used
- It's also called **Asymptotic runtime**:
    - It's only asymptotic
    - It tells us about what happens when we put really big inputs into the algorithm
    - It doesn't tell us anything about how long it takes
    - Its hidden constants:
        - They're usually moderately small, and therefore, we have something useful
        - They're could be big
    - Sometimes an algorithm A with worse Big-O runtime than algorithm B:
        - Algorithm A is worse asymptotically on very large inputs than algorithm B does
        - But algorithm A is better for all practical sizes and very large inputs couldn't be stored 
- E.g., O(1), O(n), O(n^2) , O(Log n), O(n log n), O(2^n)
- [Data structure and theirs related algorithms time complexity](https://www.bigocheatsheet.com/)

</details>

<details>
<summary>Space Complexity</summary>

- It describes the amount of memory - or space - required for an algorithm
- It useful to compare the performance of algorithms
    - Input size from which an algorithm will experience unsufficient memory (RAM) and start using Disk lookups
- Big O notation and concept are used 

</details>

<details>
<summary>Big-O Rules</summary>

- **Drop the constants**: we'll use O(n) instead of O(2 n)
- **Drop the Non-Dominant Terms**: we'll use O(n^2) instead of O(n^2 + n) or O(n) instead of O(n + log n) 
- Multi-Part Algorithms - Add: **O(A+B)**
    - When an algorithm is in the form 
    - Do A, 
    - When you're done, Do B
- Multi-Part Algorithms - Multiply: **O(A*B)**
    - When an algorithm is in the form: 
    - Do B for each time you do A
- **Amortized Time**
    - When the worst case happens once a while 
    - But once it happens, it won't happen again for so long that the cost is "amortized" 
    - E.g., insert in a dynamic resizing array (an array list): 
        - It's implemented with an array 
        - When the array hits its capacity, it will create a new array with double the capacity and copy all the elements over to the new array
        - Insert time complexity in expected case (the array isn't full): O(1)
        - Insert time complexity in worst case (the array is full): O(n)
        - Insert time complexity for n inserts: O(n) (for n expected cases) + O(w * n) (w worst cases): O((w+1)n) = O(n)
        - The amortization time for each insertion (the time complexity for n inserts divided by n): O(1)
- **Log n** runtimes: O(log n)
    - It when the number of elements in a problem space is halved each time (or divided by n) 
    - E.g. **Dichotomic search**: search in a sorted array
- The base of Log(n) isn't import
    - E.g. O(Log2 n) = O(Log3 n) = O(Log n) 
- **Recursive Runtimes**, a recursive algorithm usually is defined by:
    - Its **depth**: n and the **number of times each recursive call branches** (itself). 
    - **Time complexity: O(branchesNbr^n)** 
    - **Space complexity: O(n)**
    - E.g., Fibonacci Recursive time complexity: O(2^n)
    - E.g., Fibonacci Space complexity: O(n): because only O(N) nodes exist at any given time 
- The **base of an Exponent**:
    - Log(8^n) is completely different than Log(2^n)
 
</details>

<details>
<summary>Algorithm Design</summary>

- **Reading problem statement**: 
    - The problem statement specifies the input-output format, the constraints for the input data as well as time and memory limits 
    - Our goal is to implement a fast program that solves the problem and works within the time and memory limits
    - Question inputs:
        - **String**: Encoding (ASCII, UTF-8, UTF-16)?, Special characters?
        - **Number**: Size (Int. Long, ...)? Precision, Rounding?
- **Build your intuition**:
    - *In progress*
- **Designing an algorithm**: 
    - When the problem statement is clear, start designing an algorithm and 
    - Don’t forget to **prove that it works correctly**
    - Don't forget to **estimate its expected running time**:
        - E.g.
        -       Time Complexity:     O(n^2)                  O(n log n)
                    Machine ops:      10^9                   10^9
                              n:      10^5                   10^5
                 Estimated Time:      > 10s (10^10/10^9)     < 1 ms (10^5*log(10^5)/10^9)
- **Implementing an algorithm**: 
    - After you developed an algorithm, start implementing it in a programming language
- **Testing and debugging your program** 
    - Testing is the art of revealing bugs
    - 1st start with **simple test cases**: 
        - Small dataset
        - Make sure our program produces correct results
    - 2nd check **degenerate** cases: see test cases section above
    - 3rd check **boundary** values: see test cases section above
    - 4th check **randomly** generated cases
    - 5th check **large** dataset: see test cases section above
    - 6th finish with **stress** testing: see test cases section above

</details>

<details>
<summary>General Approaches</summary>

- **Tournament** approach:
    - To find the kth largest number in an array, compare each paire of 2 elements together
    - compare(elem 0, elem 1), compare(elem 2, elem 3)...
    - O(n + log(n) − 2)
- **Euclidean** Algorithm

</details>

<details>
<summary>Greedy Algorithms</summary>

- **Greedy Strategy**:
    - **1. Make a greedy choice**
    - **2. Prove that it is a safe choice**
    - **3. Reduce to a subproblem**
    - **4. Solve the subproblem (Iterate)**
    - E.g. Problem, Queue of Patients:
        - n patients have come to the doctor’s office at same time
        - Ti is the time needed for treatment of the i-th patient
        - They can be treated in any order 
        - Output: Arrange the patients in such a queue that the total waiting time is minimized
    - E.g. Solution:
        - Make a greedy choice: choose the patient (Pi) with the smallest treatment time (with the minimum Ti)
        - Prove that it's a safe choice
        - Reduce to a smaller problem: remove Pi from the queue
        - Iterate: Treat all the remaining patients in such order as to minimize their total waiting time as if there wasn't 1st patient
- **Subproblem** 
    - It's a similar problem of smaller size
    - Minimum total waiting time for n patients = (n − 1) · T min + minimum total waiting time for n − 1 patients without T min
    - Min total waiting time for n = 4 partients: (15, 10, 25, 20) = (4 - 1) * 10 + Min total waiting time for (15, 25, 20)
- **Safe Choice**:
    - It's a greedy choice which there's an optimal solution consistent with this 1st choice
    - It requires to **prove** that a greedy choice is safe
    - E.g. Queue of Patients: 
        - If we prove that there's an optimal solution that starts with treating a patient with the minimum treatment time
        - Therefore such a choice is a safe choice
        - However, if we choose a patient with the maximum treatment time, there's not an optimal solution that starts with it
        - Therefore such a choice isn't a safe choice
- E.g. Fractional Knapsack (or Backpack) Problem:
    - N items with total weight and total value (Wi, Vi)
    - A Backpack with a capacity W
    - Goal: Maximize value ($) while limiting total weight (kg)
    - It's possible to take fraction of items
    - Item 1: (6, $30), Item 2 (3, $14), Item 3 (4, $16), Item 4 (2, $9)
        - Knapsack capacity: 10
        - Value per Unit: Item 1: $5; Item2: $4.66; Item3: $4; Item4: $4.5
        - Solution: 6 * $5 + 3 * $4.666 + 1 * $4.5 (fraction of item4) = $48.5

</details>

<details>
<summary>Divide and Conquer</summary>

- **Divide**: Break into non-overlapping subproblems of the same type
- **Conquer**:
    - Solve subproblems: each one indepently of the others
    - Combine results
- Implementation: it's often implemented with a **recursive** algorithm
- Calculate its Time Complexity:
    - Define a corresponding **recurrence relation**, **T**
        - It's an equation recursively defining a sequence of values
        - For Linear Search *T(n) = T(n - 1) + c*; *T(0) = c*
        - *c* is the runtime for a constant amount of work: checking high vs. low indexes; if A[low] == key); preparing the parameters for the recursive call
        - *T(0)* is the runtime for the **base case** of the recursion (empty array): checking high vs. low indexes, returning not found
        - For Binary Search *T(n) = T(n/2) + c*; *T(0) = c*
    - Determine **worst-case runtime**, T(n) from the recurrence relation
        - Look at the **recursion tree**
        - For Linear Search T(n) = T(n - 1) + c = T(n - 2) + 2 * c = n * c = T(n) = Θ(n)
        - For Binary Search T(n) = T(n/2) + c = T(n/2^2) + 2 * c = T(n/2^3) + 3 * c = Θ(log2 n) = Θ(log n)
- Optionally, create iterative solution
    - It allows to save space
- For more details:
    - [Binary Search](https://www.khanacademy.org/computing/computer-science/algorithms/binary-search/a/binary-search)
    - **Merge Sort**
        - [Course Material](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/1_algorithm_design_and_techniques/week4_divide_and_conquer/03_divide_and_conquer_4_sorting.pdf)
        - [Merge Sort on khanacademy](https://www.khanacademy.org/computing/computer-science/algorithms#merge-sort)
    - **Quick Sort**
        - It's more efficient in practice than Merge Sort
        - Average Time Complexity: O(n log n)
        - Time Complexity in the worst case: O(n^2)
        - [Course Material](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/1_algorithm_design_and_techniques/week4_divide_and_conquer/03_divide_and_conquer_5_quicksort.pdf)
        - [Quick Sort on khanacademy](https://www.khanacademy.org/computing/computer-science/algorithms#quick-sort)
        - [Deterministic and Randomized Quicksort](http://faculty.cs.tamu.edu/klappi/csce411-f12/csce411-set13.pdf)
        - [3 way partition Quick Sort](https://www.geeksforgeeks.org/3-way-quicksort-dutch-national-flag/)
        - [Quick Sort Recursive Tail Elimination](https://www.geeksforgeeks.org/quicksort-tail-call-optimization-reducing-worst-case-space-log-n/)
        - [Quick Sort wth deterministic pivot selection heuristic]:
            - The pivot could be the median of the 1st, middle, and last element
            - If the recursion depth exceeds a certain threshold ***c log n***, the algorithm switches to heap sort
            - It's a simple but heuristic approach:: it's not guaranteed to be optimal
            - The time complexity is: O(n log n) in the worst case
    - [Counting Sort](https://www.geeksforgeeks.org/counting-sort/)

</details>

<details>
<summary>Dynamic Programming</summary>

- It's a general algorithmic design technique: Approach can be used to solve many kinds of problems
- It's Frequently used for optimization problems: finding best way to do something
- It's typically used when brute-force solution is to enumerate all possibilities:
    - May not know which subproblems to solve, so we solve many or all!
    - Reduce number of possibilities by:
        - Finding optimal solutions to subproblems
        - Avoiding non-optimal subproblems (when possible)
        - Frequently gives a polynomial algorithm for brute force exponential one
- It's like Divide and Conquer:
    - General design technique
    - Uses solutions to subproblems to solve larger problems
    - Difference: Dynamic Programming subproblems typically overlap
- It's an alternative for Recursive algorithms:
    - Recursive algorithms may be not efficient: they could do a compute several times
    - E.g. Money change problem MinCoin(40 cents) in Tanzania:
    - MinCoin(40s) = 1 + Min( MinCoin(40c - 1c), MinCoin(40c - 5c), MinCoin(40c - 10c), MinCoin(40c - 20c), MinCoin(40c - 25c))
    - MinCoin(20c) is computed at least 4 times: MinCoin(40c - 1c), MinCoin(40c - 5c), MinCoin(40c - 10c), MinCoin(40c - 20c)
- It's an alternative for Greedy Algorithms: 
    - When there is not a safe choice
    - E.g.1, Money change problem MinCoin(40 cents) in US:
        - US coins <<< 40c: 1c, 5c, 10c, 25c
        - A Greedy choice: take the max coin such that coin <<< 40c
        - Result: 3 coins: 40c = 1 * 25c + 1 * 10c + 1 * 5c
        - Here this choice is safe
    - E.g.2, Money change problem MinCoin(40 cents) in Tanzania:
        - Tanzanian coins <<< 40c: 1c, 5c, 10c, 20c, 25c
        - A greedy choice: take the max coin such that the coin <<< 40c
        - Result: 3 coins: 40c = 1 * 25c + 1 * 10c + 1 * 5c
        - Here this choice isn't safe: 40c = 2 * 20c
- Steps:
    - Express a solution mathematically
        - **Cut and Paste Trick Dynamic Programming**:
        - Cut and paste proof: optimal solution to problem must use optimal solution to subproblem: otherwise we could remove suboptimal solution to subproblem and replace it with a better solution, which is a contradiction
        - [For more details](https://stackoverflow.com/questions/9553162/what-is-the-cut-and-paste-proof-technique)
    - Express a solution recursively
    - Either develop a **bottom up algorithm**:
        - Find a bottom up algorithm to find the optimal value
        - Find a bottom up algorithm to construct the solution
    - Or develop a **memoized recursive algorithm**
- **Alignment game** (String Comparison):
    - Remove all symbols from 2 strings in such a way that the number of points is maximized:
    - Remove the 1st symbol from **both** strings: 1 point if the symbols match; 0 if they don't
    - Remove the 1st symbol from **one** of the strings: 0 point
    - E.g.,:    
        -       A T G T T A T A  => A T - G T T A T A
                A T C G T C C    => A T C G T - C - C
                                   +1+1  +1+1         = +4
    - **Sequence Alignment**:
        - It's a 2-row matrix
        - 1st row: symbols of the 1st string (in order) interspersed by "-"
        - 2nd row: symbols of the 2nd string (in order) interspersed by "-"
        - E.g.:  
        -        A T - G T T A T C
                 A T C G T - C - C
                     ^-Del ^--Insert.
        - **Alignment score**: 
            - Premium (**+1**) for every **match** 
            - Penalty (**-μ**) for every **mismatch**
            - Penatly (**-σ**) for every **indel** (insertion/deletion)
            - E.g.:
            -  A T - G T T A T A
               A T C G T - C - C
              +1+1-1+1+1-1-0-1+0 = +1
        - **Optimal alignment**:
            - Input: 2 strings, mismatch penatly μ, and indel penalty σ
            - Output: An alignment of the strings maximizing the score
    - **Common Subsequence**: **Matches** in an alignment of 2 strings form their **common subsequence**
        - E.g. 
        -      A T - G T T A T C
               A T C G T - C - C
               AT    G T 
              (ATGT) is a common subsequence
- **Longest common subsequence**:
    - Input: 2 strings
    - Output: A longest common subsequence of these strings
    - It corresponds to **highest alignment score** with **μ = σ = 0** (maximizing the score of an alignment)
- **Edit distance**
    - Input: 2 strings
    - Output: the **minimum number of operations** (insertions, deletions, and substitutions of symbols) **to transform one string into another**
    - It corresponds to the **minimum number of mismatches and indels** in an alignment of 2 strings (among all possible alignments)
    - E.g.: 
    -       E D I - T I N G -
            - D I S T A N C E
            ^-Del ^-Ins.----^
    - **Minimizing edit distance = Maximizing Alignment score**
    - Let ***D(i,j)*** be the edit distance of an *i*-prefix *A*[1... *i*] and a *j*-prefix *B*[1.... *j*]
    - ***D(i,j) = MIN(D(i,j-1) + 1, D(i-1,j) + 1, D(i-1,j-1) + 1) if A[i] <> B[j]*** OR
    - ***D(i,j) = MIN(D(i,j-1) + 1, D(i-1,j) + 1, D(i-1,j-1)) if A[i] = B[j]***
- **Reconstructing an **Optimal Alignment**:
    - It could be done by backtracking pointers that are stored in the edit distance computation matrix
- E.g., Discrete Knapsack problem
    - N items with total weight Wi (Kg) and total value Vi ($)
    - A Backpack with a capacity W
    - Each item is either taken or not
    - Goal: Maximize value ($) while limiting total weight (kg)
    - Discrete Knapsack with unlimited repetitions quantities:
        - Input: Weights (W1,..., Wn) and values (V1,..., Vn) of n items; total weight W (Vi’s, Wi’s, and W are non-negative integers)
        - Output: The maximum value of items whose weight doesn't exceed W 
        - Each item can be used any number of times
        - Item 1 (6, $30), Item 2 (3, $14), Item 3 (4, $16), Item 4 (2, $9)
        - Knapsack capacity: 10
        - Solution: 6 ($30) + 2 ($9) + 2 ($9) = $48
        - Greedy Algorithm doesn't work: 6 ($30) + 
    - Discrete Knapsack without one of each repetitions item:
        - Input: Weights (W1,..., Wn) and values (V1,..., Vn) of n items; total weight W (Vi’s, Wi’s, and W are non-negative integers)
        - Output: The maximum value of items whose weight doesn't exceed W 
        - Each item can be used at most once
        - Item 1 (6, $30), Item 2 (3, $14), Item 3 (4, $16), Item 4 (2, $9)
        - Knapsack capacity: 10
        - Solution: 6 ($30) + 4 ($16) = $46
    - Greedy Algorithm fails:
        - Item1 (6, $30), Item2 (3, $14), Item3 (4, $16), Item4 (2, $9)
        - Value per Unit: Item 1: $5; Item2: $4.66; Item3: $4; Item4: $4.5
        - 6 ($30) + 3 ($14) = 9 items ($44)
        - taking an element of maximum value per unit of weight is not safe!
- For more details:
    - [Course material](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/1_algorithm_design_and_techniques/week5_and_6_dynamic_programming/04_dynamic_programming_2_editdistance.pdf)
    - [Advanced dynamic programming lecture notes]() by Jeff Erickson
    - [How Do We Compare Biological Sequences?](https://www.youtube.com/playlist?list=PLQ-85lQlPqFNmbPEsMoxb5dM5qtRaVShn) by Phillip Compeau and Pavel Pevzner
- For more details:
    - [Money change problem: Greedy vs. Recursive vs. Dynamic Programming](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/1_algorithm_design_and_techniques/week5_and_6_dynamic_programming/04_dynamic_programming_1_changeproblem.pdf)
    - [Dynamic Programming](https://www.geeksforgeeks.org/dynamic-programming/) in geeksforgeeks
    - [Dynamic Programming](https://www.radford.edu/~nokie/classes/360/dynprog.html)

</details>

---

## Data Structures Fundamentals

<details>
<summary>Arrays</summary>

- It's a contiguous area of memory
- It's consisting of equal-size elements indexed by contiguous integers
- **1-D Array**: accessing **array[i]** consists of accessing the memory address: **array_addr + elem_size × (i − first_index)**
- **2-D Array**:
    - It could be laid out in **Row-Major order**:
        - Its 2nd index (column) changes most rapidly
        - Its elements are laid out as follow: (1,1), (1,2), (1,3), ..., (2,1), (2,2),...
        - Accessing **[i][j]** consists of accessing the memory address: **array_addr + elem_size × [row_lenth * (i  − 1st_row_index) + (j − 1st_column_index)]**
    - It could be laid out in **Column-Major order**:
        - Its 1st index (row) changes most rapidly
        - Its elements are laid out as follow: (1,1), (2,1), (2,1), ..., (1,2), (2,2),...
        - Accessing **[i][j]** consists of accessing the memory address: **array_addr + elem_size × [column_lenth * (j  − 1st_column_index) + (i − 1st_row_index)]**
- Time Complexity and Operations:
    -                     Read    Remove   Add
            Beginning:    O(1)     O(n)    O(n) 
                  End:    O(1)     O(1)    O(1)
               Middle:    O(1)     O(n)    O(n)
- Programming Languages:
    - Python: there is no static array data structure
- For more details:
    - [Arrays and Lists Course](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/1_basic_data_structures/01_1_arrays_and_lists.pdf)

</details>

<details>
<summary>Linked Lists</summary>

- Singly-Linked List
    -                APIs                Time (wout tail)   Time (w tail)         Description 
                PushFront(Key):               O(1)                                 Aadd to front
                Key TopFront():               O(1)                                 Return front item
                    PopFront():               O(1)                                 Remove front item
                 PushBack(Key):               O(n)              O(1)               Add to back
                 Key TopBack():               O(n)              O(1)               Return back item
                     PopBack():               O(n)                                 Remove back item
             Boolean Find(Key):               O(n)                                 Is key in list?
                    Erase(Key):               O(n)                                 Remove key from list
               Boolean Empty():               O(1)                                 Empty list?
          AddBefore(Node, Key):               O(n)                                 Adds key before node
           AddAfter(Node, Key):               O(1)                                 Adds key after node 
- **Doubly-Linked List**:
    - Its node consists of a key, a pointer to the next node and a pointer to the previous node
    -                APIs                    Time (wout tail)   Time (w tail)
                PushFront(Key):               O(1)                                 
                Key TopFront():               O(1)                                 
                    PopFront():               O(1)                                 
                 PushBack(Key):               O(n)              O(1)               
                 Key TopBack():               O(n)              O(1)               
                     PopBack():               O(n)              O(1)                 
             Boolean Find(Key):               O(n)                                 
                    Erase(Key):               O(n)                                 
               Boolean Empty():               O(1)                                 
          AddBefore(Node, Key):               O(1)
           AddAfter(Node, Key):               O(1)
- Programming Languages:
    - Python:
- For more details:
    - [Arrays and Lists Course](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/1_basic_data_structures/01_1_arrays_and_lists.pdf)

</details>

<details>
<summary>Stacks</summary>

- LIFO: Last-In First-Out
- It could be implemented with an array:
    - We should keep track of the latestest element pushed index which is different from its capacity `len(array)`
    -           Push(key): 
                    if max-index + 1 <  len(array): 
                        max-index += 1 
                        array[max-index] = key
    -           Top(): 
                    if max-index >= 0: 
                        return array[max-index]
    -           Pop(): 
                    if max-index >= 0: 
                        value = array[max-index]
                        max-index -= 1 
                        return value
    -          Empty(): 
                    return max-index == -1
- It could be implemented with a Singly-Linked-List:
    -           Push(key): list.PushFront(Key)
    -           Top(): return list.TopFront()
    -           Pop(): return list.PopFront()
    -         Empty(): return list.Empty()
-             Time Complexity: Array Imp.     Singly-Linked List      Comment     
                    Push(key):  Θ(1)           Θ(1)   
                    Key Top():  Θ(1)           Θ(1)       
                    Key Pop():  Θ(1)           Θ(1)     
             Space Complexity:  Θ(n)           Θ(2 * n) = O(n)         Linked-List uses more space because of the pointers         
- Programming Languages:
    - Python:
        - `List`
        - `collections.deque`
        - `queue.LifoQueue`
        - [For more details](https://www.geeksforgeeks.org/stack-in-python/)
- Related Problems:
    - [Balanced Brackets](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/issues/21)
- For more details:
    - [UC San Diego Course](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/1_basic_data_structures/01_2_stacks_and_queues.pdf)
    - Visualization: [Implementation with an Array](https://www.cs.usfca.edu/~galles/visualization/StackArray.html)
    - Visualization: [Implementation with a Linked List](https://www.cs.usfca.edu/~galles/visualization/StackLL.html)

</details>

<details>
<summary>Queues</summary>

- It could be implemented with an array:
    - We should have a **circular** array
    - We should keep track of the latestest inserted element index (we'll use it for reads): `read-index`
    - We should keep track of the most recent inserted element index(we'll use it for writes): `write-index`
    - Initially: `read-index == write-index == 0`
    -           Empty(): return (read-index == write-index)
    -           Full(): return (read-index == write-index + 1)
    -           Enqueue(key): 
                    if Not Full(): 
                        array[write-index] = key
                        write-index = write-index + 1 if write-index < len(array) - 1 else 0
    -           Dequeue(): 
                    if Not Empty():
                        value = array[read-index]
                        read-index = read-index + 1 if read-index < len(array) - 1 else 0
                        return value
- It could be implemented with a Doubly-Linked-List with a tail:
    - The list head will be used for reads
    - The list writes will be used for writes
    -           Empty(): return list.Empty()
    -           Enqueue(key): list.PushBack(Key)
    -           Dequeue(): list.PopFront()
-             Time Complexity: Array Imp.     Singly-Linked List      Comment     
                    Push(key):  Θ(1)           Θ(1)   
                    Key Top():  Θ(1)           Θ(1)       
                    Key Pop():  Θ(1)           Θ(1)     
             Space Complexity:  Θ(n)           Θ(2 * n) = O(n)         Linked-List uses more space because of the pointers
- Programming Languages:
    - Python:
        - `List`
        - `collections.deque` class
        - `queue.Queue` class
        - [More details](https://www.geeksforgeeks.org/queue-in-python/)
- Related Problems:
    - 
- For more details:
    - [UC San Diego Course](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/1_basic_data_structures/01_2_stacks_and_queues.pdf)
    - Visualization: [Implementation with an Array](https://www.cs.usfca.edu/~galles/visualization/QueueArray.html)
    - Visualization: [Implementation with a Linked List](https://www.cs.usfca.edu/~galles/visualization/QueueLL.html)

</details>

<details>
<summary>Trees</summary>

- It is empty, or a node with a key, and a list of child trees
- Terminology:
    - A **Root**: top node in the tree
    - A **child** has a line down directly from a **parent**
    - An **Ancestor** is a parent, or a parent of parent, etc.
    - **Descendant** is a child, or a child of child, etc.
    - A **Sibling** is sharing the same parent
    - A **Leaf** is a node without children
    - An **Interior node** is a node that isn't a leaf
    - An **Edge** is a link between two nodes
    - A **Level**: 
        - 1 + number of edges between a tree root and a node
        - E.g., The root node is level 1
    - A **Height**: 
        - It's the maximum depth of subtree node and its farthest leaf
        - It could be calculated by counting the number of nodes or edges
    - A **Forest** is a collection of trees
- Walking a Tree:
    - **Depth-First** (**DFS**): To traverse one sub-tree before exploring a sibling sub-tree
    - **Breadth-First** (**BFS**): To traverse all nodes at one level before progressing to the next level
- A **Binary Tree**: 
    - It's a tree where each node has 0, 1, or 2 children
    - DFS types: 
        - **In Order Traversal** of a node: InOrderTraversal of its Left child; Visit node; InOrderTraversal of its Right child
        - **Pre Order Traversal** of a node: Visit node; PreOrderTraversal of its Left child; PreOrderTraversal of its Right child
        - **Post Order Traversal** of a node: PostOrderTraversal of its Left child; PostOrderTraversal of its Right child; Visit node
    - A **Complete Binary Tree**: 
        - It's a binary tree in which all its levels are filled except possibly the last one which is filled from left to right
        - Its height is **Low**: it's at most **O(log n)** (n is nbr of nodes)
        - It could be **stored effeciently** as an **array**
    - A **Full Binary Tree**:
        - It's also called **Proper Binary Tree** or **2-tree**
        - It's a tree in which every node other than the leaves has 2 children
        - Its height is Low: it's equal to **log n**
        - It could be stored effeciently as an array
- For more details:
    - [UC San Diego Course](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/1_basic_data_structures/01_3_trees.pdf)

</details>

<details>
<summary>Dynamic Arrays</summary>

- It's also known as **Resizable array**
- It's a solution for limitations of **static** arrays and **dynamically-allocated** arrays (see below):
    - It can be resized at runtime
    - It stores (implementation):
        - Arr: dynamically-allocated array
        - Capacity: size of the dynamically-allocated array
        - Size: number of elements currently in the array
    - When an element is added to the end of the array and array's size and capacity are equal:
        - It allocates a new array
        - New Capacity = Previous Capacity x 2
        - Copy all elements from old array to new array
        - Insert new element
        - New Size = Old Size + 1
        - Free old array space
- Time Complexity and Operations:
    -                       Time Complexity
                  Get(i):       O(1) 
             Set(i, val):       O(1)
           PushBack(val):       O(1) or O(n): O(n) when size = capacity; O(1) otherwise (amortized analysis)
               Remove(i):       O(1)
                  Size():       O(1)
- Programming Languages:
    - Python: list (the only kind of array)
    - C++: vector
    - Java: ArrayList
- Static array:
    - it's static!
    - It requires to know its size at compile time
    - Problem: we might not know max size when declaring an array
- Dynamically-allocated arrays:
    - int *my_array = new int[ size ]
    - It requires to know its size at runtime
    - Problem: we might not know max size when allocating an array
- More details:
    - [UC San Diego Course](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/2_dynamic_arrays_and_amortized_complexity/02_1_dynamic_arrays_and_amortized_analysis.pdf)

</details>

<details>
<summary>Amortized Analysis</summary>

- **Amortized cost**: 
    - Given a sequence of n operations, 
    - The amortized cost is: **Cost(n operations) / n**
- Methods to calculate amortized cost:
    - The **Aggregate method**: 
        - It calculates amortized cost based on amortized cost definition
        - E.g. Dynamic Array: n calls to PushBack
        - Let ci = cost of i-th insertion
        -                   _ i - 1 if i - 1 is a power of 2
                          / 
                ci = 1 + |
                          \ _ 0 otherwise
                                  n              ⌊log 2 (n−1)⌋
                Amortized Cost =  ∑ ci / n = (n + ∑ 2^j        ) / n 
                               = O(n)/n = O(1)
    - The **Banker's Method**: it consists of:
        - Charging extra for each cheap operation
        - Saving the extra charge as **tokens** in our data structure (conceptually)
        - Using the tokens to pay for expensive operations
        - It is like an amortizing loan
        - E.g. Dynamic Array: n calls to PushBack:
        - 1. Charge 3 for each insertion: 
            - Use 1 token to pay the cost for insertion;
            - Place 1 token on the newly-inserted element
            - Plase 1 token on the capacity / 2 elements prior
        - 2. When Resize is needed: 
            - Use 1 token To pay for moving the existing elements (all token in the array will dispear)
            - When all old array elements are moved to the new array, insert new element (go to 1)
    - The **Physicist's Method**: it consists of:
        - Defining a **potential function*, **Φ** which maps states of the data structure to integers:
            - `Φ(h0 ) = 0`
            - `Φ(ht ) ≥ 0`
    - Amortized cost for operation t: `ct + Φ(ht) − Φ(ht−1)`
    - Choose Φ so that:
        - if ct is small, the potential increases
        - if ct is large, the potential decreases by the same scale
    - The sum of the amortized costs is: 
    -                           n       n
                Φ(hn) − Φ(h0) + ∑ ci ≥  ∑ ci
                               i=0     i=0                
    - E.g. Dynamic Array: n calls to PushBack:
    - Let `Φ(h) = 2 × size − capacity`
        - `Φ(h0) = 2 × 0 − 0 = 0`
        - `Φ(hi) = 2 × size − capacity > 0` (since size > capacity/2)
    - Calculating Amortized cost for operation i (adding element i): `ci + Φ(hi) − Φ(hi−1)`:
        - Without resize:    
        -           ci = 1; 
                    Φ(hi) = 2 * (k + 1) - c 
                    Φ(hi-1) = 2 * k - 2 - c 
                    ci + Φ(hi) − Φ(hi−1) = 1 + 2 * k - c - 2 * k + 2 + c = +3
        - With resize:
        -           ci = k + 1; 
                    Φ(hi) = 2 * (k + 1) - 2 * k = 2 since there is a resize, the array capacity is doubled
                    Φ(hi-1) = 2 * k - k = k since before the resize, the array capacity is equal to the array size
                    ci + Φ(hi) − Φ(hi−1) = k + 1 + 2 - k = +3
- Related Problems:
    - [Dynamic Array with a Popback Operation I](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/issues/24)
    - [Dynamic Array with a Popback Operation II](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/issues/25)
    - [Dynamic Array with a Popback Operation III](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/issues/26)
    - [Dynamic Array with a PopMany Operation](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/issues/27)
- More details:
    - [Amortized Analysis](https://youtu.be/U5XKyIVy2Vc) 
    - [UC San Diego](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/2_dynamic_arrays_and_amortized_complexity/02_1_dynamic_arrays_and_amortized_analysis.pdf)

</details>

<details>
<summary>Priority Queues: Max/Min Heap</summary>

- **Max Heap**:
    - It's a binary tree where the value of each node is at least the values of its children
    - For each edge of the tree, the value of the parent is at least the value of the child
- **Min Heap**:
    - It's a binary tree where the value of each node is at most the values of its children
- Implementation, Time Complexity and Operations:
    - An efficient implementation is a **Complete Binary Tree** in an **Array**
    -            Operations        0-based index      1-based index array
                  Parent(i):          ⌊ i / 2 ⌋         ⌊ i / 2 ⌋
               Leftchild(i):          2 * i + 1         2 * i
              Rightchild(i):          2 * i + 2         2 * i + 1
    -                               Time Complexity     Comment
                   GetMax():             O(1)            or GetMin()
               ExtractMax():           O(log n)        n is the nodes # (or ExtractMin)
                  Insert(i):           O(log n)
                  SiftUp(i):           O(log n)
                SiftDown(i):           O(log n)
          ChangePriority(i):           O(log n)
                  Remove(i):           O(log n)
- Programming Languages:
    - Python:
        - Lib/heapq.py
        - [Description](https://docs.python.org/2/library/heapq.html)
        - [Git](https://github.com/python/cpython/blob/2.7/Lib/heapq.py)
    - C++:
    - Java:
- For more details:
    - UC San Diego Course: [Overview & Naive Implementations](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/3_priority_queues_and_disjoint_sets/03_1_priority_queues_intro.pdf)
    - UC San Diego Course: [Binary Heaps](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/3_priority_queues_and_disjoint_sets/03_2_priority_queues_heaps.pdf)

</details>

<details>
<summary>Priority Queues: Heap Sort</summary>

- Not-In place algorithm to sort an Array (A) with a Heap Sort:
    -       Create an empty priority queue MaxHeap
            for i from 1 to n:
                MaxHeap.Insert(A[i])
            for i from n downto 1:
                A[i] = MaxHeap.ExtractMax()
    - Time Complexity:  O(n log n)
    - **Space Complexity: O(n)** (It's not an in place algorithm)
    - It's a natural generalization of selection sort:
        - Instead of simply scanning the rest of the array to find the maximum value,
        - It uses a smart data structure
- In place algorithm to sort an array (A) with a Heap Sort:
    - Step 1: Turn the array A[] into a heap by permuting its elements
        - We repair the heap property going from bottom to top
        - Initially, the heap property is satisfied in all the leaves (i.e., subtrees of depth 0)
        - We then start repairing the heap property in all subtrees of depth 1
        - When we reach the root, the heap property is satisfied in the whole tree
    -       BuildHeap(A[1 ... n])
                for i from ⌊n/2⌋ downto 1:
                    SiftDown(i)
        - Space Complexity: O(1) (In place algorithm)
        - Time Complexity:
                Height          Nodes #    T(SiftDown)       T(BuildHeap)
                log_2(n)          1         log_2(n)          1 * log_2(n) 
                log_2(n) - 1      2         log_2(n) - 1      2 * [ log_2(n) - 1]
                  ...            ...         ...                 ...
                   2            ≤ n/4        2                n/4 * 2
                   1            ≤ n/2        1                n/2 * 1
                T(BuildHeap) = n/2 * 1 + n/4 * 2 + ... + 1 * log_2(n) 
                             = n/2 * 1 + n/4 * 2 + ... + n / 2^log_2(n) * log_2(n)
                             = n [1/2 + 2/4 + 2/8 + ... log_2(n)/2^log_2(n)] < n * 2
                             = **O(n)**
    - Step 2: Sort the Heap
    -       HeapSort(A[1 . . . n])
                BuildHeap(A)
                repeat (n − 1) times:
                    swap A[1] and A[size]
                    size = size − 1
                    SiftDown(1)
        - Space Complexity: O(1) (In place algorithm)
        - Time Complexity: O(n long n)
- Use cases:
    - It's used for external sort when we need to sort huge files that don’t fit into memory of our computer 
        - In opposite of QuickSort which is usually used in practice because typically it is faster
    - **IntraSort** algorithm:
        - It's a sorting algorithm
        - It 1st runs QuickSort algorithm (Avergae Running time: O(n log n); Worst Running time: O(n^2))
        - If it turns out to be slow (the recursion depths exceed c log n, for some constant c),
        - Then it stops the current call to QuickSort algorithm and switches to HeapSort algorithm (Guaranteed Running time: O(n log n))
        - It's a QuickSort algorithm with worst running time: O(n log n)
    - **Partial Sorting**:
        - Input: An array A[1 . . . n], an integer k: 1 ≤ k ≤ n
        - Output: The last k elements of a sorted version of A
        -       PartialSort(A[1 . . . n], k)
                BuildHeap(A)
                for i from 1 to k:
                    print(A.ExtractMax())
        - BuildHeap Running Time: O(n)
        - Printing: the last k elements of a sorted version of A: O(k * log n)
        - Running time: O(n + k log n)
        - if k = O(n / log n) => **Running time = O(n)**
        - E.g. Printing the last 102 elements of a sorted version of an array of 1024 elements:
            - It takes a linear time
            - if n = 1024 = 2^10 then k = 2^10 / log 2^10 = 1024 / 10 = 102
- For more details:
    - UC San Diego Course: [Overview & Naive Implementations](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/3_priority_queues_and_disjoint_sets/03_1_priority_queues_intro.pdf)
    - UC San Diego Course: [Binary Heaps](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/3_priority_queues_and_disjoint_sets/03_2_priority_queues_heaps.pdf)

</details>

<details>
<summary>Priority Queues: d-ary Heap</summary>

- In a **d-ary heap** nodes on all levels have exactly **d children** except for possibly the last one
- Its height is about: ***Log_d n***
- Implementation, Time Complexity and Operations:
    - An efficient implementation is a **Complete D-ary Tree** in an **Array**
    -            Operations:    0-based index     1-based index array
                  Parent(i):     ⌊ i / d ⌋         ⌊ i / d ⌋
               1st child(i):     d * i + 1         d * i
               2nd child(i):     d * i + 2         d * i + 1
                    ...             ...               ...
              d-th child(i):     d * i + d         d * i + d - 1
    -                           Time Complexity   Comment
                   GetMax():     O(1)              or GetMin()
               ExtractMax():     O(d * Log_d n)    See running time of SiftDown
                  Insert(i):     O(Log_d n)
                  SiftUp(i):     O(Log_d n)        On each level, there is only 1 comparison: child vs. parent
                SiftDown(i):     O(d * Log_d n)    On each level, there are d comparisons among d children
          ChangePriority(i):     O(d * Log_d n)
                  Remove(i):     O(d * Log_d n)

</details>

<details>
<summary>Disjoint Sets</summary>

- It's also called **Union-Find data structure**
- It's a data structure that keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets
- A 1st efficient implementation is **Union by Rank Heuristic**: 
    - It consists of a **Tree** in **2 Arrays**
    - Each set is a rooted tree
    - The ID of a set is the root of the tree
    - Array 1: **Parent**[1 ... n], Parent[i] is the parent of i, or i if it is the root
    - Array 2: **Rank**[1 ... n], Rank[i] = height of subtree which root is i, rank of the tree's root = 0
    - MakeSet(i):
        - It creates a singleton set {i}
        - It consists of a tree with a single node: parent[i] = i
    - Find(i):
        - It returns the ID of the set that is containing i
        - It consists of the root of the tree where i belongs
    - Union(i, j):
        - It merges 2 sets containing i and j
        - It consists of merging 2 trees
        - For effenciency purposes, it must keep the resulting tree as shallow as possible
        - It hang the shorter tree under the root of the longer one (we'll use **rank** array here)
        - The resulted tree height = the longer tree height if the 2 trees height are different
        - The resulted tree height = the height of one of the trees + 1 if the 2 trees height are equal:
        -                       Time Complexity
                MakeSet(x):      O(1)
                   Find(x):      O(tree height) = O(log n) 
               Union(x, y):      O(tree height) = O(log n) 
- A 2nd more efficient implementation is **Path Compression Heuristic**:
    - We keep the same data structure as the Union by rank heuristic implementation
    - When finding the root of a tree for a particular node i, reattach each node from the traversed path to the root
    - From an initially empty disjoint set, we make a sequence of m operations including n calls to MakeSet:
        - The total running time is O(m log∗(n))
        - The **Amortized time** of a single operation is: **O(log∗(n))**
        -                       Time Complexity
                MakeSet(x):      O(1)
                   Find(x):      O(log*(n)) = O(1) if n ≤ 2^65536
               Union(x, y):      O(log*(n)) = O(1) if n ≤ 2^65536
        - For more details about log*(n), see [Prerequisites](#prerequisites)
- Programming Languages:
    - Python:
    - C++:
    - Java:
- Use Cases:
    - Keep track of the connected compoents of an undirected graph
        - To determine whether 2 vertices belong to the same component
        - To determine whether adding an edge between 2 vertices would result in a cycle
    - **Kruskal's algorithm**:
        - It's used to find the minimum spanning tree of a graph
        - [For more details](#graph-algorithms)
    - In a maze (a grid with walls): Is a given cell B reachable from another given cell A?
        - Build disjoint sets where each non-wall cell represent a singleton set
            for each cell c in maze:
                if c isn't a wall MakeSet(c)
        - Modify disjoint sets above so that if a path between A and B exists, then A and B are in the same set
            for each cell c in maze:
                for each neighbor n of c:
                    Union(c, n)
        - Check is a path between A and B exists:
            IsReachable(A, B)
                return Find(A) = Find(B)
    - Building a Network:
- Related Problems:
    - [Find whether individual x is a friend of individual y](https://github.com/hamidgasmi/algorithms-datastructures/issues/33)
    - [Finding an Exit from a Maze](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/issues/87)
    - [Dish Owner](https://github.com/hamidgasmi/algorithms-datastructures/issues/35)
    - [Galactik Football](https://github.com/hamidgasmi/algorithms-datastructures/issues/36)
    - [Merging tables](https://github.com/hamidgasmi/algorithms-datastructures/issues/32)
    - [Jam Board](https://github.com/hamidgasmi/algorithms-datastructures/issues/37)
    - [The Last Droid](https://github.com/hamidgasmi/algorithms-datastructures/issues/40)
    - [Substrings and Repetitions](https://github.com/hamidgasmi/algorithms-datastructures/issues/38)
    - [Tiptoe through the tulips](https://github.com/hamidgasmi/algorithms-datastructures/issues/39)
    - [Ada Farm](https://github.com/hamidgasmi/algorithms-datastructures/issues/34)
- For more details:
    - UC San Diego Course: [Overview & Naive Implementations](https://github.com/hamidgasmi/algorithms-datastructures/tree/master/2-data-sructures-fundamentals/3_priority_queues_and_disjoint_sets)
    - UC San Diego Course: [Efficient Implementations](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/3_priority_queues_and_disjoint_sets/03_4_disjoint_sets_efficient.pdf)
    - [Tutorial](https://www.topcoder.com/community/competitive-programming/tutorials/disjoint-set-data-structures/)

</details>

<details>
<summary>Hashing: Introduction</summary>

- A **Hash Function**:
    - It's a function that maps a set of keys from *U* to a set of integers: *0, 1, ..., m − 1*
    - In other words, it's a function such that for any key *k* from *U* and any integer *m > 0*, a function `h(k) : U → {0, 1, ... , m − 1}`
    - A key **Universe**, ***U***
        - It's the set *U* of all possible keys
        - `|U|` is the universe size
    - A hash **Cardinality**:
        - It's `m`
        - It's the # of different values of the hash function
        - It's also the size of the table where keys will be stored
    - A **Collision** 
        - It happens when `h(k1) = h(k2)` and `k1 != k2`
- **Direct Addressing**:
    - It's the simplest form of hashing
    - It's a data structure that has the capability of mapping records to their corresponding keys using arrays
    - Its records are placed using their key values directly as indexes
    - ![Hash Map](https://www.geeksforgeeks.org/wp-content/uploads/hmap.png)
    - It doesn't use a Hashing Function:
        -                                   Time Complexity
                     GetDate(key):              O(1)
                Insert(key, data):              O(1)
                      Delete(key):              O(1)
        -                                   Space Complexity
                Direct Addressing Table:        O(|U|) even if |U| <<< actual size
    - Limitations:
        - It requires to know the maximum key value (*|U|*) of the direct addressing table
        - It's practically useful only if the key maximum value is very less
        - It causes a waste of memory space if there is a significant difference between the key maximum value and records #
    - E.g., Phone Book:
        - Problem: Retrieving a name by phone number
        - Key: Phone number
        - Data: Name
        - Local phone #: 10 digits
        - Maximum key value: 999-999-9999 = 10^10
        - It requires to store the phone book as an array of size 10^10
            - Each cell store a phone number as a long data type: 8 bytes + a name of 12 size long (12 bytes): 20 bytes
            - The size of the array will be then: 20 * 10^10 = 2 * 10^11 = 2 * 2^36.541209044 = 2^30 * 2^8.541209044 = 373 GB
            - It requires 373 GB of memory!
        - What about international #: 15 digits
            - It would require a huge array size
            - It would take 7 PB to store one phone book
- **Chaining**:
    - It's an implementation technique used to solve collision issues:
        - It uses an array
        - Each value of the hash function maps a **Slot** in the array
        - Each element of the array is a **doubly-linked** list of pairs (key, value)
        - In case of a collision for 2 different keys, their pairs are stored in a linked list of the corresponding slot
    - `n` is the number of keys stored in the array: `n ≤ |U|`
    - `c` is the length of the longest chain in the array:
        - `c ≥ n / m`
        - The question is how to come up with a hash function so that the space is optimized (m is small) and the running time is efficient (c is small)
        - Space worst case: `c = n`: all values are stored in the same slot
        - Space best case: `c = n / m`: keys are evenly distributed among all the array cells
        - See Universal Familly
    - **Load Factor**, **α**:
        - `α = n / m`
        - If α is too small (`α <<< 1`), there isn't lot of collisions but the cells of the array are empty: we're wasting space
        - If α > 1, there is at least 1 collision
        - If α is too big, there are a lot of collisions, *c* is too long and the operations will be too slow
    - ![Hash Chaining](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2015/07/hashChaining1.png)
- **Open Addressing**:
    - It's an implementation technique used to solve collisions issue
- For more details:
    - UC San Diego Course: [Introduction to Hashing](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/4_hashing/04_1_hashing_intro.pdf)
    - UC San Diego Course: [Hash Function](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/4_hashing/04_2_hashing_hashfunctions.pdf)
    - Geeks for Geeks: [Hashing: Introduction](https://www.geeksforgeeks.org/hashing-set-1-introduction/)
    - Geeks for Geeks: [Direct Address Table](https://www.geeksforgeeks.org/direct-address-table/)
    - Geeks for Geeks: [Hashing: Chaining](https://www.geeksforgeeks.org/hashing-set-2-separate-chaining/)
    - Geeks for Geeks: [Hashing: Open Addressing](https://www.geeksforgeeks.org/hashing-set-3-open-addressing/)
    - Geeks for Geeks: [Address Calculation Sort using Hashing](https://www.geeksforgeeks.org/address-calculation-sort-using-hashing/)

</details>

<details>
<summary>Hashing: Universal Family</summary>

- It's a collection of hash functions such that:
    - `H = { h : U → {0, 1, 2, ... , m − 1} }`
    - For any 2 keys `x, y ∈ U, x != y` the **probability of collision** `Pr[h(x) = h(y)] ≤ 1 / m`
    - It means that a collision for any fixed pair of different keys happens for no more than **1 / m** of all hash functions h ∈ H
    - All hash functions in H are deterministic
- How Randomization works:
    - To Select a random function h from the family H: 
        - It's the only place where we use randomization
        - This randomly chosen function is deterministic  
    - To use this **Fixed** *h* function throughout the algorithm: 
        - to put keys into the hash table,
        - to search for keys in the hash table, and 
        - to remove the keys from the hash table
    - Then, the average length of the longest chain `c = O(1 + α)`
    - Then, the average running time of hash table operations is `O(1 + α)`
- Choosing Hash Table Size:
    - Ideally, load factor **0.5 < α < 1**:
        - if α is very small (α ≤ 0.5), a lot of the cells of the hash table are empty (at least a half)
        - If α > 1, there is at least one collision
        - If α is too big, there're a lot of collisions, *c* is too long and the hash table operations are too slow
    - To Use **O(m) = O(n/α) = O(n)** memory to store n keys
    - Operations will run in time O(1 + α) = **O(1) on average**
- For more details:
    - UC San Diego Course: [Hash Function](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/4_hashing/04_2_hashing_hashfunctions.pdf)

</details>

<details>
<summary>Hashing: Dynamic Hash table</summary>

- **Dynamic Hash table**:
    - It's good when the number of keys n is unknown in advance
    - It resizes the hash table when α becomes too large (same idea as dynamic arrays)
    - It chooses new hash function and rehash all the objects
    - Let's choose to Keep the load factor below 0.9 (`α ≤ 0.9`);
        -       Rehash(T):
                    loadFactor = T.numberOfKeys / T.size
                    if loadFactor > 0.9:
                        Create Tnew of size 2 × T.size
                        Choose hnew with cardinality Tnew.size
                        For each object in T:
                            Insert object in Tnew using hnew
                            T = Tnew, h = hnew
        - The result of the rehash method is a new hash table wit an α == 0.5
        - We should call Rehash after each operation with the hash table
        - Single rehashing takes **O(n)** time, 
        - Amortized running time of each operation with hash table is: **O(1)** on average, because rehashing will be rare
- For more details:
    - UC San Diego Course: [Hash Function](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/4_hashing/04_2_hashing_hashfunctions.pdf)

</details>

<details>
<summary>Hashing: Universal Family for integers</summary>

- It's defined as follow:
-       Hp = { hab(x) = [(a * x + b) mod p] mod m } for all a, b 
               p is a fixed prime > |U|, 
               1 ≤ a ≤ p − 1, 
               0 ≤ b ≤ p − 1
- Question: How to choose p so that mod p operation = O(1)
- H is a universal family for the set of integers between 0 and p − 1:
    - `|H| = p * (p - 1)`: 
    - There're (p - 1) possible values for a 
    - There're p possible values for b
- **Collision Probability**:
    - if for any 2 keys x, y ∈ U, x != y: `Pr[h(x) = h(y)] ≤ 1 / m`
- How to choose a hashing function for integers:
    - Identify the universe size: |U|
    - Choose a prime number p > |U|
    - Choose hash table size:
        - Choose m = O(n)
        - So that 0.5 < α < 1
        - See Universal Family description
    - Choose random hash function from universal family Hp:
        - Choose random a ∈ [1, p − 1]
        - Choose random b ∈ [0, p − 1]
- For more details:
    - UC San Diego Course: [Hash Function](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/4_hashing/04_2_hashing_hashfunctions.pdf)

</details>

<details>
<summary>Hashing: Polynomial Hashing for string</summary>

- It convert all its character S[i] to integer:
    - It uses ASCII, Unicode
    - It uses all the characters in the hash function because otherwise there will be many collisions
    - E.g., if S[0] is not used, then h(“aa”) = h(“ba”) = ··· = h(“za”)
- It uses Polynomial Hashing:
-                          |S|
            Pp = { hx(S) =  ∑ S[i] * x^i mod p } for all x
                          i = 0
                    p a fixed prime, 
                    |S| the length of the string S 
                    x (the multiplier) is fixed: 1 ≤ x ≤ p − 1
- *Pp* is a universal family:
    - `|Pp| = p - 1`: 
    - There're (p - 1) possible values for x
-           PolyHash(S, p, x)
                hash = 0
                for i from |S| − 1 down to 0:
                    hash = (hash * x + S[i]) mod p
                return hash

            E.g. |S| = 3
            hash = 0
            hash = S[2] mod p
            hash = S[1] + S[2] * x mod p
            hash = S[0] + S[1] * x + S[2] * x^2 mod p
- How to store strings in a hash table:
    - 1st, apply random *hx* from *Pp*
    - 2nd, hash the resulting value again using universal family for integers, *hab* from *Hp*
    - `hm(S) = hab(hx(S)) mod m`
    - **Collision Probability**:
        - For any 2 different strings s1 and s2 of length at most L + 1, 
        - if we choose h from *Pp* at random (by selecting a random x ∈ [1, p − 1]), 
        - The probability of collision: `Pr[h(s1) = h(s2)] ≤ 1/m + L/p`
        - If p > m * L, `Pr[h(s1) = h(s2)] ≤ O(1/m)`
    - How to choose a hashing function for strings:
        - Identify the max length of the strings: L + 1
        - Choose a hash table size:
            - Choose m = O(n)
            - So that 0.5 < α < 1
            - See Universal Family description
        - Choose a prime number such that `p > m * L`
        - Choose a random hash function for integers from universal family *Hp*:
            - Choose a random a ∈ [1, p − 1]
            - Choose a random b ∈ [0, p − 1]
        - Choose a random hash function for strings from universal family *Pp*
            - Choose a random x ∈ [1, p − 1]
- E.g., Phone Book 2:
    - Problem: Design a data structure to store phone book contacts: names of people along with their phone numbers
    - The following operation must be fast: Call person by name
    - Solution: To implement Map from names to phone numbers
- Use Cases:
    - [Rabin-Karp's Algorithm](https://brilliant.org/wiki/rabin-karp-algorithm/) uses **Polynomial Hashing** to find patterns in strings
    - Java class String method hashCode:
        - It uses Polynomial Hashing
        - It uses x = 31
        - It avoids the (mod *p*) operator for technical reasons
- For more details:
    - UC San Diego Course: [Hash Function](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/4_hashing/04_2_hashing_hashfunctions.pdf)

</details>

<details>
<summary>Hashing: Maps</summary>

- It's a data structure that maps **keys** from set S of objects to set V of **values**:
    - It's implemented with chaining technique
    - `chain (key, value) ← Array[hash(key)]`
- It has the following methods:
    -                            Time Complexity       Comment
                    HasKey(key):  Θ(c + 1) = O(1 + α)   Return if object exists in the map   
                       Get(key):  Θ(c + 1) = O(1 + α)   Return object if it exists else null
                Set(key, value):  Θ(c + 1) = O(1 + α)   Update object's value if object exists else insert new pair (object, value)
                                                               If n = 0:  Θ(c + 1) = Θ(1)
                                                               If n != 0: Θ(c + 1) = Θ(c)
                                                               Maps hash function is universal: c = n/m = α
                                 Space Complexity
                                  Θ(m + n)              Array size (m) + n pairs (object, value)                 
- E.g., Phone Book:
    - Problem: Retrieving a name by phone number
    - Hash Function:
        - Select hash function h of cardinality m, let say, 1 000 (small enough)
        - For any set of phone # P, a function h : P → {0, 1, . . . , 999}
        - h(phoneNumber)
    - A Map:
        - Create an array Chains of size m, 1000
        - Chains[i] is a doubly-linked list of pairs (name, phoneNumber)
        - Pair(name, phoneNumber) goes into a chain at position h(phoneNumber) in the array Chains
    - To look up name by phone number, go to the chain corresponding to phone number and look through all pairs
    - To add a contact, create a pair (name, phoneNumber) and insert it into the corresponding chain
    - To remove a contact, go to the corresponding chain, find the pair (name, phoneNumber) and remove it from the chain
- Programming Languages:
    - Python: **dict**
    - C++: **unordered_map**
    - Java: **HashMap**
- For more details:
    - UC San Diego Course: [Hash Function](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/4_hashing/04_2_hashing_hashfunctions.pdf)

</details>

<details>
<summary>Hashing: Sets</summary>

- It's a data structure that implements the mathematical concept of a **finite Set**:
    - It's usually used to test whether elements belong to set of values (see methods below)
    - It's implemented with chaining technique:
        - It could be implemented with a map from S to V = {true}; the chain pair: (object, true); It's costly: "true" value doesn't add any information
        - It's actually implemented To store just objects instead of pairs in the chains
- It has the following methods:
    -                            Time Complexity       Comment
                     Add(object): Θ(c + 1) = O(1 + α)   Add object to the set if it does exit else nothing   
                  Remove(object): Θ(c + 1) = O(1 + α)   Remove object from the set if it does exist else nothing
                    Find(object): Θ(c + 1) = O(1 + α)   Return True if object does exist in the set else False
                                                               If n = 0:  Θ(c + 1) = Θ(1)
                                                               If n != 0: Θ(c + 1) = Θ(c)
                                                               Sets hash function is universal: c = n/m = α 
                                 Space Complexity
                                  Θ(m + n)              Array size (m) + n objects        
- Programming Languages:
    - Python: **set**
    - C++: **unordered_set**
    - Java: **HashSet**
- For more details:
    - UC San Diego Course: [Hash Function](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/4_hashing/04_2_hashing_hashfunctions.pdf)

</details>

<details>
<summary>Binary Search Tree (BST)</summary>

- It's a binary tree data stucture with the property below:
    - Let's X a node in the tree
    - X’s key is larger than the key of any descendent of its left child, and 
    - X's key is smaller than the key of any descendent of its right child
- Implementation, Time Complexity and Operations:
    - Time Complexity: O(height)
    -               Operations:     Description:
                      Find(k, R):    Return the node with key k in the tree R, if exists
                                            the place in the tree where k would fit, otherwise
                         Next(N):    Return the node in the tree with the next largest key
                                            the LeftDescendant(N.Right), if N has a right child
                                            the RightAncestor(N), otherwise
               LeftDescendant(N):
                RightAncestor(N):
          RangeSearch(k1, k2, R):    Return a list of nodes with key between k1 and k2
                    Insert(k, R):    Insert node with key k to the tree
                       Delete(N):    Removes node N from the tree:
                                             It finds N
                                             N.Parent = N.Left, if N.Right is Null, 
                                             Replace N by X, promote X.Right otherwise
- **Balanced** BST:
    - The **height** of a balanced BST is at most: **O(log n)**
    - Each subtree is half the size of its parent
    - Insertion and deletion operations can destroy balance
    - Insertion and deletion operations need to rebalance
- For more details:
    - UC San Diego Course: [BST Basic Operations](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/5_binary_search_trees/05_1_3_binary_search_trees_basic_operations.pdf)
    - UC San Diego Course: [Balance](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/5_binary_search_trees/05_1_4_binary_search_trees_balance.pdf)

</details>

<details>
<summary>AVL Tree</summary>

- It's a **Balanced** BST:
    - It keeps balanced by maintaining the following **AVL property**:
        - For all nodes N,
        - `|N.Left.Height − N.Right.Height| ≤ 1`
- Implementation, Time Complexity and Operations:
    - Time Complexity: **O(log n)**
    - Insertion and deletion operations can destroy balance:
        - They can modify height of nodes on insertion/deletion path
        - They need to rebalance the tree in order to maintain the AVL property
    - Steps to follow for an **insertion**:
        - 1- Perform standard BST insert
        - 2- Starting from w, travel up and find the first unbalanced node 
        - 3- Re-balance the tree by performing appropriate rotations on the subtree rooted with z 
        -           Let w be the newly inserted node
                        z be the first unbalanced node, 
                        y be the child of z that comes on the path from w to z
                        x be the grandchild of z that comes on the path from w to z     
        - There can be 4 possible cases that needs to be handled as x, y and z can be arranged in 4 ways:
        -      Cas 1: Left Left Case:
                     z                                     y 
                    / \                                  /   \
                   y   T4      Right Rotate (z)         x      z
                  / \         - - - - - - - - ->      /  \    /  \ 
                 x   T3                              T1  T2  T3  T4
                / \
              T1   T2
        -      Cas 2: Left Right Case:
                     z                               z                              x
                    / \                            /   \                          /   \ 
                   y   T4   Left Rotate (y)        x    T4    Right Rotate(z)    y      z
                  / \      - - - - - - - - ->    /  \        - - - - - - - ->   / \    / \
                T1   x                          y    T3                       T1  T2 T3  T4
               / \                             / \
              T2   T3                         T1   T2

        -      Cas 3: Right Right Case:
                      z                               y
                    /  \                            /   \ 
                  T1   y    Left Rotate(z)         z      x
                 /  \      - - - - - - - ->       / \    / \
                T2   x                           T1  T2 T3  T4
               / \
              T3  T4

        -      Cas 4: Right Left Case:
                      z                              z                               x
                     / \                            / \                            /   \ 
                   T1   y   Right Rotate (y)       T1   x     Left Rotate(z)      z      y
                  / \      - - - - - - - - ->     /  \       - - - - - - - ->    / \    / \
                 x   T4                         T2   y                          T1  T2  T3 T4
                / \                            /  \
              T2   T3                         T3   T4
    - Steps to follow for a **Deletion**:
        - (1) Perform standard BST delete
        - (2) Travel up and find the 1st unbalanced node
        - (3) Re-balance the tree by performing appropriate rotations
        -           Let w be the newly inserted node
                        z be the 1st unbalanced node
                        y be the larger height child of z 
                        x be the larger height child of y
                    Note that the definitions of x and y are different from insertion 
        - There can be 4 possible cases:
        -      Cas 1: Left Left Case:
                     z                                      y 
                    / \                                   /   \
                   y   T4      Right Rotate (z)          x      z
                  / \          - - - - - - - - ->      /  \    /  \ 
                 x   T3                               T1  T2  T3  T4
                / \
              T1   T2
        -      Cas 2: Left Right Case:
                     z                               z                            x
                    / \                            /   \                         /  \ 
                   y   T4   Left Rotate (y)       x    T4   Right Rotate(z)     y      z
                  / \      - - - - - - - - ->    /  \      - - - - - - - ->    / \    / \
                T1   x                          y    T3                      T1  T2 T3  T4
                    / \                        / \
                  T2   T3                    T1   T2

        -      Cas 3: Right Right Case:
                     z                                y
                    /  \                            /   \ 
                   T1   y     Left Rotate(z)       z      x
                  /  \       - - - - - - - ->     / \    / \
                 T2   x                          T1  T2 T3  T4
                / \
              T3  T4
        -      Cas 4: Right Left Case:
                     z                            z                            x
                    / \                          / \                          /  \ 
                  T1   y   Right Rotate (y)    T1   x      Left Rotate(z)   z      y
                 / \      - - - - - - - - ->      /  \   - - - - - - - ->  / \    /  \
                x   T4                           T2   y                   T1  T2  T3  T4
               / \                              /  \
              T2  T3                           T3   T4
    - Steps to follow for a **Merge** operation:
        - Input: Roots R1 and R2 of trees with all keys in R1’s tree smaller than those in R2’s
        - Output: The root of a new tree with all the elements of both trees
        - (1) Go down side of the tree with the bigger height until reaching the subtree with height equal to slowest height
        - (2) Merge the trees
        - (2.a) Get new root Ri by removing largest element of left subtree (Ri)
        - There can be 3 possible cases:
        -       Cas 1: R1.Height = R2.Height = h
                     R1          R2                   R1'    z     R2                   z(h+1)
                    / \         /  \                 /  \         /  \                 /     \
                  T3   T4 (+) T5  T6   Delete(z)   T3'  T4' (+) T5   T6   Merge      R1'(h-1)  R2(h)
                  / \                 - - - - - ->                      - - - - ->   /  \       /  \
                T1  ...                Rebalance                                    T3'  T4'    T5   T6
                    / \          h-1 ≤ R1'.height ≤ h                            AVL property maintained
                   T2  z
        -       Cas 2: R1.Height (h1) < R2.Height (h2):
                    R1          R2                           R1(h1)       R2'(h1)
                    / \         /  \                        /  \         /  \
                  T3   T4 (+) T5   T6  Find R2' in T5     T3   T4 (+)  T7   T8     Merge
                                      - - - - - - - ->                          - - - - -> Go to Case 1
                                      R2'.height = h1
        -       Cas 3: R1.Height (h1) > R2.Height (h2):
                    R1           R2                          R1'(h2)      R2(h1)
                    / \         /  \                        /  \         /  \
                  T3   T4 (+) T5   T6  Find R1' in T4     T1   T2 (+)  T5   T6     Merge
                                      - - - - - - - ->                          - - - - -> Go to Case 1
                                      R1'.height = h2
    - Steps to follow for a **Split**:
- Related Problems:
    - 
- Use Cases:
    - 
- For more details:
    - UC San Diego Course: [AVL tree](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/5_binary_search_trees/05_2_1_binary_search_trees_avl_trees.pdf)
    - UC San Diego Course: [AVL Tree implementation](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/5_binary_search_trees/05_2_2_binary_search_trees_avl_tree_implementation.pdf)
    - UC San Diego Course: [Split and Merge](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/5_binary_search_trees/05_2_3_binary_search_trees_split_merge.pdf) operations
    - Geeks for Geeks: [AVL tree insertion](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)
    - Geeks for Geeks: [AVL tree deletion](https://www.geeksforgeeks.org/avl-tree-set-2-deletion/)
    - Visualization: [AVL Tree](https://www.cs.usfca.edu/~galles/visualization/AVLtree.html)

</details>

<details>
<summary>Splay Tree</summary>

- 
- For more details:
    - UC San Diego Course: [Splay Trees Introduction](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/5_binary_search_trees/06_2_1_binary_search_trees_splay_trees_introduction.pdf)
    - UC San Diego Course: [Splay Tree Implementation](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/5_binary_search_trees/06_2_2_binary_search_trees_splay_tree_implementation.pdf)
    - UC San Diego Course: [Splay Tree Analysis](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/2-data-sructures-fundamentals/5_binary_search_trees/06_2_3_binary_search_trees_splay_tree_analysis.pdf)
    - Visualization: [Splay Tree](https://www.cs.usfca.edu/~galles/visualization/SplayTree.html)

</details>

---

## Graph Algorithms

<details>
<summary>Graphs: Basics</summary>

- It's a collection of 
    - **V** **vertices**, and 
    - **E** **edges** 
    - Each edge connects a pair of vertices
    - A collection of undirected edges forms an **Undirected graph**
    - A collection of directed edges forms an **Directed graph** 
- A **Loop** connect a vertex to itself
- Multiple edges between same vertices
- A **Simple** graph 
    - It's a graph
    - It doesn't have loops 
    - It doesn't have multiple edges between same vertices
- The **degree** a vertex:
    - It's also called **valency** of a vertex
    - It's the number of edges that are incident to the vertex
- Implementation, Time Complexity and Operations:
    - **Edge List**: 
        - It consists of storing the graph as a list of edges
        - Each edge is a pair of vertices,
        - E.g., Edges List: (A, B) --> (A, C ) --> (A, D) --> (C , D)
    - **Adjacency Matrix**:
        - Matrix[i,j] = 1 if there is an edge, 0 if there is not
        - E.g.      Undirected              Directed
                    A   B   C   D           A   B   C   D
                A   0   1   1   1       A   0   1   1   1
                B   1   0   0   0       B   0   0   0   0
                C   1   0   0   1       C   0   1   0   1
                D   1   0   1   0       D   0   1   0   0
    - **Adjacency List**:
        - Each vertex keeps a list of adjacent vertices (neighbors)
        - E.g.
            Vertices:  Neighbors (Undirected)   Neighbors (Directed)
             A          B -> C -> D              B -> C -> D
             B          A                        
             C          A -> D                   B
             D          A -> C                   B
    -       Time Complexity         Edge List   Adjacency Matrix    Adjacency List
                  IsEdge(v1, v2):       O(|E|)         O(1)              O(deg)
                     ListAllEdge:       O(|E|)         O(|V|^2)          O(|E|)
                ListNeighbors(v):       O(|E|)         O(|V|)            O(deg)
- **Density**:
    - A **Dense Graph**:
        - It's a graph where a large fraction of pairs of vertices are connected by edges
        - |E | ≈ |V|^2
        - E.g., Routes between cities:
        - It could be represented as a dense graph
        - There is actually some transportation option that will get you between basically any pair of cities on the map
        - What matter is not whether or not it's possible to get between 2 cities, but how hard it is to get between these cities
    - A **Sparse Graph**:
        - It's a graph where each vertex has only a few edges
        - |E| ≈ |V|
        - E.g. 1, we could represent the internet as a sparse graph,
        - There are billions of web pages on the internet, but any given web page is only gonna have links to a few dozen others
        - E.g. 2. social networks
    - **Asymptotique analysis depends on the Density of the graph**
- **Connected Components**:
    - A Graph vertices can be partitioned into Connected Components 
    - So that v is reachable from w if and only if they are in the same connected component
- A **Cycle** in a graph:
    - It's a sequence of vertices v1,..., vn so that 
    - (v1, v2 ),..., (vn−1, vn), (vn, v1) are all edges
    - Cycle graphs cannot be linearly ordered (typologically ordered)
- E.g.
    - Directed Graph:
        - Streets with one-way roads
        - Links between webpages
        - Followers on social network
        - Dependencies between tasks
- For more details:
    - UC San Diego Course: [Basics](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/3-graph-algorithms/1_graph_decomposition/09_graph_decomposition_1_basics.pdf)
    - UC San Diego Course: [Representation](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/3-graph-algorithms/1_graph_decomposition/09_graph_decomposition_2_representations.pdf)
    - Khanacademy [Introduction to Graphs](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/describing-graphs)

</details>

<details>
<summary>Depth-First Search (DFS)</summary>

- We will explore new edges in Depth First order
- We will follow a long path forward, only backtracking when we hit a dead end
- It doesn't matter if the graph is directed or undirected
- Loop on all virtices:
        def DFS(G):
            mark unvisited all vertices v ∈ G.V

            for v ∈ G.V:
                if not visited (v):
                    Explore(v)

- Explore 1 path until hitting a dead end:      
        def Explore (v ):
            visited (v ) = true
            for (v , w) ∈ E:
                if not visited (w):
                    Explore (w)
- Time complexity:
    -            Implementation:    Explore()        DFS
                  Adjacency List:    O(degre)       O(|V| + ∑ degre for all v) = O(|V| + |E|)
                Adjacency Matrix:    O(|V|)         O(|V|^2)
    - Number of calls to explore:
        - Each explored vertex is marked visited
        - No vertex is explored after visited once
        - Each vertex is explored exactly once
    - Checking for neighbors: O(|E|)
        - Each vertex checks each neighbor.
        - Total number of neighbors over all vertices is O(|E|)
    - We prefer adjacency list representation!
- Space Complexity:
- DFS **Previsit** and **Postvisit** Functions:
    - Plain DFS just marks all vertices as visited
    - We need to keep track of other data to be useful
    - Augment functions to store additional information
    -     def Explore (v ):
            visited(v) = true
            previsit (v)
            for (v , w) ∈ E:
                if not visited (w):
                    Explore (w)
            postvisit (v)
    - E.g., **Clock**:
        - Keep track of order of visits
        - Clock ticks at each pre-/post- visit
        - Records previsit and postvisit times for each v
        -       previsit (v )
                    pre (v) ← clock
                    clock ← clock + 1
        -       postvisit (v )
                    post (v ) ← clock
                    clock ← clock + 1
        - It tells us about the execution of DFS
        - For any u, v the intervals [ pre(u), post(u)] and [ pre (v), post (v)] are either nested or disjoint
        - Nested: u: [ 1, 6 ], v [ 3, 4 ]: v is reachable from u
        - Disjoint: u [ 1, 6 ], v [ 9, 11 ]: v isn't reachable from u
        - Interleaved (isn't possible)  u [ 1, 6 ], v [ 3, 8 ]
- Related problems:
    - Detect there is a cycle in a graph:
        - [Checking Consistency of CS Curriculum](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/issues/95)
- For more details:
    - UC San Diego Course: [Exploring Graphs](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/3-graph-algorithms/1_graph_decomposition/09_graph_decomposition_3_explore.pdf)
    - Visualization: [DFS](https://www.cs.usfca.edu/~galles/visualization/DFS.html)

</details>

<details>
<summary>DAGs: Topological Sort</summary>

- A **DAG**:
    - **Directed Acyclic Graph**
    - It's a directed graph G without any cycle
- A **source** vertex is a vertex with no incoming edges
- A **sink** vertex is a vertex with no outgoing edges
- A Topological Sort:
    - Find sink; Put at end of order; Remove from graph; Repeat
    - It's the DFS algorithm
    -       TopologicalSort (G )
                DFS (G)
                Sort vertices by reverse post-order
- Related problems:
    - [Determining an Order of Courses](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/issues/96)
- For more details:
    - UC San Diego Course: [DAGs](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/3-graph-algorithms/1_graph_decomposition/09_graph_decomposition_6_dags.pdf)
    - UC San Diego Course: [Topological Sort](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/3-graph-algorithms/1_graph_decomposition/09_graph_decomposition_7_topological-sort.pdf)
    - Geeks for Geeks: [topological sort with In-degree](https://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/)
    - Visualization: [Topological Sort using DFS](https://www.cs.usfca.edu/~galles/visualization/TopoSortDFS.html)
    - Visualization: [Topological sort using indegree array](https://www.cs.usfca.edu/~galles/visualization/TopoSortIndegree.html)

</details>

<details>
<summary>Strongly Connected Components</summary>

- **Connected vertices**:
    - 2 vertices v, w in a directed graph are connected:
    - if you can reach v from w and can reach w from v
- **Strongly connected graph**: is a directed graph where every vertex is reachable from every other vertex
- **Strongly connected components**, **SCC**: It's a collection of subgraphs of an arbitrary directed graph that are strongly connected
- **Metagraph**:
    - It's formed from all strongly connected components
    - Each stromgly connected components is represented by a vertice
    - **The metagraph of a directed graph is always a DAG**
- **Sink Components** 
    - It's a subgrph of a directed graph with no outgoing edges
    - If v is in a sink SCC, `explore (v)` finds this SCC
- **Source Components** 
    - It's a subgrph of a directed graph with no incoming edges
    - The vertex with the largest postorder number is in a source component
- **Reverse Graph**, **G^R** 
    - It's a directed graph obtained from G by reversing the direction of all of its edges
    - G^R and G have same SCCs
    - Source components of G^R are sink components of G
    - **The vertex with largest postorder in G^R is in a sink SCC of G**
- Find all SCCs of a directed graph G:
    -       SCCs (G, Gr):
                Run DFS(Gr):
                for v ∈ V in reverse postorder:
                    if v isn't visited:
                        Explore(v, G): vertices found are first SCC
                        Mark visited vertices as new SCC
    - Time Complexity: O(|V| + |E|)
        - It's essentially DFS on Gr and then on G
- Related Problems:
    - [Checking Whether Any Intersection in a City is Reachable from Any Other](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/issues/97)
- For more details:
    - UC San Diego Course: [Strongly Connected Components I](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/3-graph-algorithms/1_graph_decomposition/09_graph_decomposition_8_strongly-connected-components.pdf)
    - UC San Diego Course: [Strongly Connected Components II](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/3-graph-algorithms/1_graph_decomposition/09_graph_decomposition_9_computing-sccs.pdf)
    - Visualization: [Strongly connected components](https://www.cs.usfca.edu/~galles/visualization/ConnectedComponent.html)

</details>

<details>
<summary>Paths in Graphs: Path and Distance (Basic)</summary>

- A **Path**:
    - It's a collection of edges that connects 2 vertices u, v
    - It could exist multiple paths linking same vertices
- **Path length**:
    - L(P)
    - It's the number of edges of a path
- **Distance**
    - It's between 2 nodes in a graph
    - It's the length of the shortest possible path between these nodes  
    - For any any pair of vertices u, v: **Distance(u, v) in a directed graph is >= Distance(u, v) in the corresponding undirected graph**
- **Distance Layers**:
    - For a given vertex v in  a graph, it's a way of representing the graph by repositioning all its nodes from top to bottom with increasing distance from v
    - Layer 0: contains the vertex v
    - Layer 1: contains all vertices which distance to v is: 1
    - ...
    - E.g.:     G:       Layers    Distance Layers from A       Distance Layers from C
            A -- B -- C    0           A                               C
                      |                |                             /   \
                      D    1           B                            B     D
                                       |                            |
                           2           C                            A
                                       |
                           3           D
    - In a Undirected graph, **Edges are possible between same layer nodes or adjacent layers nodes** 
        - In other words, there is no edge between nodes of a layer l and nodes of layers < l - 1 and layers > l + 1 
        - E.g. From example above:
        -       Distance Layers from C:
                0       C                                                  C
                      /   \                                              / | \
                1    B     D => there is no edge => if there an edge => B  A  D
                     |          between A and C     between A and C
                2    A
    - In an Directed graph, **Edges are possible between same layer nodes, adjacent layers nodes and to all previous layers**
    - E.g. 
        - Edges between layer 3 and any previous layer 2, 1, 0 are possible: this doesn't change the distance between D and A
        - Edges between layer 0 or 1 and layer 3 are still not possible: this does change the distance between D and A
        -       Distance Layers from C:
                0       D                                                  D
                      /   \                                              /   \
                     ↓     ↓                                            ↓     ↓
                1    C     E => there is no edge => if an edge =>       C_    E
                     ↓          from C to A          from C to A        ↓ ↓
                2    B                                                  B  A (A would be in layer 2)
                     ↓
                3    A
- For more details:
    - UC San Diego Course: [Path and Distance](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/3-graph-algorithms/10_shortest_paths_in_graphs_1_bfs.pdf)

</details>

<details>
<summary>Breadth-First Search (BFS)</summary>

- Implementation, Time Complexity:
    - Time Complexity: O(|V| + |E|)
    -           BFS(G , S):
                    for all u ∈ V:
                        dist [u] ← ∞
                        dist [S] ← 0
                    Q ← {S} { queue containing just S}
                    while Q is not empty:
                        u ← Dequeue (Q)
                        for all (u, v) ∈ u.E:
                            if dist [v ] = ∞ :
                                Enqueue (Q, v)
                                dist [v] ← dist [u] + 1
- A node is **discovered** when it's found for the 1st time and enqueued
- A node is **processed** when it's dequeued from the BFS queue: all its unvisited neighbors are discovered (enqueued) 
- By the time a node u at distance d from S is dequeued, all the nodes at distance at most d have already been discovered (enqueued)
- **BSF Queue property**:
    - At any moment, if the 1st node in the queue is at distance d from S, then all the nodes in the queue are either at distance d or d + 1 from S
    - All the nodes in the queue at distance d go before (if any) all the nodes at distance d + 1
    - Nodes at distance > d + 1 will be discovered when d + 1 are processed => all d are gone
- Related problems:
    - [Computing the Minimum Number of Flight Segments](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/issues/131)
    - A **bipartite** graph:
        - It's a graph which vertices can be split into 2 parts such that each edge of the graph joins to vertices from different parts 
        - It arises naturally in applications where a graph is used to model connections between objects of two different types 
            - E.g. 1, Boys and Girls
            - E.g. 2, Students and Dormitories
        - An alternative definition: 
            - It's a graph which vertices can be colored with two colors (say, black and white) 
            - Such that the endpoints of each edge have different colors
        - Problem: [Check if a graph is bipartite](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/issues/132)
- For more details:
    - UC San Diego Course: [BFS](https://github.com/hamidgasmi/training.computerscience.algorithms-datastructures/blob/master/3-graph-algorithms/10_shortest_paths_in_graphs_1_bfs.pdf)
    - Khanacademy [BFS](https://www.khanacademy.org/computing/computer-science/algorithms/breadth-first-search/a/breadth-first-search-and-its-uses)
    - Visualization: [BFS](https://www.cs.usfca.edu/~galles/visualization/BFS.html)

</details>



<details>
<summary>Minimum Spanning Trees</summary>

- Implementation, Time Complexity and Operations:

- Programming Languages:
    - Python:
    - C++:
    - Java:
- Related Problems:
    - 
- Use Cases:
    - 
- For more details:
    - UC San Diego Course: []()

</details>

---

## NP-Complete Problem

---

## String Processing and Pattern Matching Algorithms

---

## Dynamic Programming: Applications In Machine Learning and Genomics 

---

## Graph Algorithms in Genome Sequencing

---

## References

<details>
<summary>Whitepapers & Books</summary>

- [The Algorithm Design Manual](http://mimoza.marmara.edu.tr/~msakalli/cse706_12/SkienaTheAlgorithmDesignManual.pdf) by Steven S. Skiena

- [Algorithm](http://algorithmics.lsi.upc.edu/docs/Dasgupta-Papadimitriou-Vazirani.pdf) by S. Dasgupta,C. H.Papadimitriou,andU. V. Vazirani

</details>

<details>
<summary>Talks & Courses</summary>

- [UC San Diego MicroMasters Program](https://www.edx.org/micromasters/ucsandiegox-algorithms-and-data-structures)
- Princeton University Coursera Courses:
    - [Algorithms, Part I](https://www.coursera.org/learn/algorithms-part1/home/welcome)
    - [Algorithms, Part II](https://www.coursera.org/learn/algorithms-part2/home/welcome)
- [Grokking the Coding Interview: Patterns for Coding Questions](https://www.educative.io/courses/grokking-the-coding-interview)

</details>

<details>
<summary>Articles</summary>

- [14 Patterns to Ace Any Coding Interview Question](https://hackernoon.com/14-patterns-to-ace-any-coding-interview-question-c5bb3357f6ed)
- [Solving Coding Problems With PEDAC](https://medium.com/launch-school/solving-coding-problems-with-pedac-29141331f93f)
- [Interview Questions (and answers)](http://readyforsoftwareinterview.blogspot.com/)
- [How To Approach Any Algorithm Interview Without Panicking](https://www.freecodecamp.org/news/how-to-approach-any-algorithm-interview-without-panicking-b6d7ae5c050/)
- [Top 10 Algorithms for Coding Interview](https://www.programcreek.com/2012/11/top-10-algorithms-for-coding-interview/)

</details>

---
