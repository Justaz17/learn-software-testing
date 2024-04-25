
# Control flow graph

## 2022 Summer Exam

1. Develop a control flowgraph for the code shown in Figure 1 below and determine the complexity. Suppose software testing has been employed so that TER1 = 1 and TER2 = 1, would you recommend further testing and explain your answer.  **(11 marks)**
2. Develop the branch table for the code shown in Figure 1 below. **(11 marks)**
3. Develop the block table for the code shown in Figure 1 below. **(11 marks)**

```java
public void walkFirstColOfGridEatingPies(Grid aGrid)
{
    initialize();
    for (int i=1; i <= 2; i++)
    {
        turn ("right");
    }

    for (int j=1; j <= 2; j++)
    {
        if(aGrid.pieInSight (this) == true)
        {
        eatPie (aGrid) ;
        }
        else
        {
            walk (aGrid) ;
        }
    }
}
```

### Answer 1

With the additional context provided regarding Test Effectiveness Ratios (TER) and coverage measures, let's revisit **Question 2** with a deeper understanding:

**1) Control Flowgraph and Complexity:**

To construct a control flow graph and determine complexity for the given code snippet, we'd consider the points where the flow of execution could change, which is the `for` loops and the `if` condition.

Here’s a structured outline of the control flow graph:

```
[start]
    |
[initialise()]
    |
[for i=1 to 2]
    |
[turn("right")]
    |
[end of for-loop i]
    |
[for j=1 to 2]
    |
    +--[if (aGrid.pieInSight(this))]
    |         |
    |         | (true)
    |         V
    |      [eatPie(aGrid)]
    |         |
    |         V
    |      [end of if-else]
    |
    | (false)
    V
   [walk(aGrid)]
       |
   [end of if-else]
       |
   [end of for-loop j]
       |
     [end]
```

For the complexity, we still use cyclomatic complexity. Given the description above, we have:
- 2 for-loops (2 edges each, start and end)
- 1 if-else condition (2 edges, true and false)

The cyclomatic complexity M = E - N + 2P where:
- E = 6 edges (2 for each for-loop + 2 for the if-else)
- N = 4 nodes (initialise, turn, eatPie, walk)
- P = 1 (a single connected component)

So, M = 6 - 4 + 2 = 4.

The recommendation on further testing would now take into account TER1 and TER2. If TER1 and TER2 are both equal to 1, it means every executable statement and every branch has been executed at least once. But "executed at least once" does not guarantee that all possible logical paths were tested, especially in cases of compound conditions, loops, and nested structures. Thus, additional testing might still be recommended for thoroughness, especially using different input data that could lead to different execution paths.

**2) Branch Table:**

With the additional context, we can now fill in the Branch Table with more precision, knowing that TER2 measures the branches:

```
+-------+-----------------+-------------+----------+
|  ID   | Condition       | True Branch | False    |
+-------+-----------------+-------------+----------+
| 1     | i <= 2          | turn("right")| exit loop |
| 2     | j <= 2          | pieInSight check| exit loop |
| 3     | pieInSight(this)| eatPie(aGrid)| walk(aGrid)|
+-------+-----------------+-------------+----------+
```

**3) Block Table:**

The Block Table now reflects TER1 which measures the executable statements:

```
+-------+----------------------+------------------+
| Block | Operation            | Executed (Y/N)   |
+-------+----------------------+------------------+
| 1     | initialise()         | Y                |
| 2     | turn("right") loop   | Y (2 times)      |
| 3     | pieInSight check loop| Y (2 times)      |
| 4     | eatPie(aGrid)        | Y/N (Depends on condition) |
| 5     | walk(aGrid)          | Y/N (Depends on condition) |
+-------+----------------------+------------------+
```

The 'Executed (Y/N)' column now also considers that each statement is to be executed at least once to achieve a TER1 of 1, which means that both the `eatPie(aGrid)` and `walk(aGrid)` statements must be tested at least once, despite the condition.

Given that TER1 and TER2 are 1, the code has achieved complete coverage with respect to executable statements and branches. However, as the excerpt states, complete coverage requires testing all statements and branches, and in practice, it may be challenging to achieve TER1 and TER2 of 1 without structured test planning and comprehensive testing beyond just hitting each line and branch once.

For a thorough examination, you would also want to consider the quality of the test cases (e.g., do they adequately test the functionality?) and the data used in testing (e.g., boundary values, typical values, and atypical values). This is where the concept of LCSAJs and path testing (reflected in TER3 and Ct) becomes relevant. They encourage more extensive testing to ensure robustness and reliability, which might not be fully captured by TER1 and TER2 alone.