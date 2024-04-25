
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

To address **Question 2**, we'll analyze the given code snippet from Figure 1 and develop a control flow graph, a branch table, and a block table.

**1) Control Flowgraph and Complexity:**

The control flow graph for the given code will represent the paths that control can follow during execution. The complexity will be determined using cyclomatic complexity, which is defined by the formula `M = E - N + 2P`, where `E` is the number of edges, `N` is the number of nodes, and `P` is the number of connected components.

In this case, the method consists of sequential execution, two loops, and one decision point inside the second loop. Thus, there are no complex nested structures or exception handling, which makes the graph relatively simple.

Here’s a basic outline of the control flow graph:
``` txt
initialise()
    |
    v
for-loop i (1st iteration)
    |
    v
turn("right")
    |
    v
for-loop i (2nd iteration)
    |
    v
turn("right")
    |
    v
for-loop j (1st iteration)
    |
    +--> if (pieInSight(this) == true)
    |       |
    |       v
    |    eatPie(aGrid)
    |    
    |    
    +--> else
            |
            v
         walk(aGrid)
            |
            v
for-loop j (2nd iteration)
    |
    +--> if (pieInSight(this) == true)
    |       |
    |       v
    |    eatPie(aGrid)
    |    
    |    
    +--> else
            |
            v
         walk(aGrid)
```

Cyclomatic complexity (M) can be counted as follows:

- 4 nodes for function calls (`initialise`, `turn`, `eatPie`, `walk`)
- 1 node for each for-loop condition check (2 total)
- 1 node for the if condition
- 4 edges for the for-loops (2 edges per for-loop, for the start and end)
- 2 edges for the if-else decision
- P is 1 (since the graph is connected)

Using the formula: `M = E - N + 2P`

Where `E = 4 + 4 + 2 = 10`, `N = 4 + 2 + 1 = 7`, `P = 1`

`M = 10 - 7 + 2(1) = 5`

The cyclomatic complexity is 5.

For the recommendation on further testing:
With `TER1` and `TER2` both equal to 1, it suggests that the test cases have covered the main path through each loop once. However, it may not have covered the false condition for `pieInSight`. So, I would recommend further testing to ensure that both the true and false paths of the `if` statement are tested at least once. Also, boundary conditions and error handling (if any) should be tested to ensure full coverage.

**2) Branch Table:**

A branch table would list down all the branches in the code, their outcomes, and the actions taken.

```
+-------+-----------------+-------------+----------+
|  ID   | Condition       | True Branch | False    |
+-------+-----------------+-------------+----------+
| 1     | i <= 2          | loop        | exit     |
| 2     | j <= 2          | loop        | exit     |
| 3     | pieInSight(this)| eatPie      | walk     |
+-------+-----------------+-------------+----------+
```

**3) Block Table:**

A block table would list down all the blocks of code (or statements) and whether they're executed.

```
+-------+----------------------+------------------+
| Block | Operation            | Executed (Y/N)   |
+-------+----------------------+------------------+
| 1     | initialise()         | Y                |
| 2     | turn("right") loop   | Y                |
| 3     | if (pieInSight) check| Y                |
| 4     | eatPie(aGrid)        | Conditional (Y/N)|
| 5     | walk(aGrid)          | Conditional (Y/N)|
+-------+----------------------+------------------+
```

The executed column would be filled in based on the path taken during the execution.

Note: The actual tables would be more detailed and would depend on the implementation details of the methods called (`initialise`, `turn`, `eatPie`, `walk`). These would be considered during a detailed code review or a more thorough static analysis. If you need assistance with the actual development of a detailed graph or table, please let me know, and I can provide a more detailed example.
