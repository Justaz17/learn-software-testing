
# Basic Block Example

## Example

```vb
PieEaterA walk (MyGrid)
IF MyGrid pieInsight = True
{
  PieEaterA eatPie(MyGrid)
}
PieEaterA reportStatus()
```

**Lines:**

No need to number blank lines or lines with curly braces.

| # | Code                          |
|---|-------------------------------|
| 1 | `PieEaterA walk (MyGrid)`     |
| 2 | `IF MyGrid pieInsight = True` |
| 3 | `PieEaterA eatPie(MyGrid)`    |
| 4 | `PieEaterA reportStatus()`    |

## Example branch table

- The branch table consists of columns for the Branch number, From Line, To Line and Branch Type
- Branch table for last example

Branch Table

| Branch No. | From Line # | To Line # | Branch Type   | From Line                              | To Line                       |
|:-----------|:------------|:----------|:--------------|:---------------------------------------|:------------------------------|
| 1          | 1           | 2         | Unconditional | `PieEaterA walk (MyGrid)`              | `IF MyGrid pieInsight = True` |
| 2          | 2           | 3         | Conditional   | `IF MyGrid pieInsight = True` is True  | `PieEaterA eatPie(MyGrid)`    |
| 3          | 2           | 4         | Conditional   | `IF MyGrid pieInsight = True` is False | `PieEaterA reportStatus()`    |
| 4          | 3           | 4         | Unconditional | `PieEaterA eatPie(MyGrid)`             | `PieEaterA reportStatus()`    |

## Example Blocks table

- The Block Table consists of Block Number, Start Line and End Line
- Block table for last example

| Block Number | Start Line # | End Line # | From Line                     | To Line                    |
|:-------------|--------------|------------|-------------------------------|----------------------------|
| 1            | 1            | 1          | `PieEaterA walk (MyGrid)`     | `...`                      |
| 2            | 2            | 3          | `IF MyGrid pieInsight = True` | `PieEaterA reportStatus()` |
| 3            | 4            | 4          | `PieEaterA reportStatus()`    | `...`                      |

`...` indicates that the To Line code is the same as the From Line code
