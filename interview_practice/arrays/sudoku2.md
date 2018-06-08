# Sudoku 2

Interview question asked by **Apple**, **Uber**

## Problem
Sudoku is a number-placement puzzle. The objective is to fill a `9 × 9` grid with numbers in such a way that each column, each row, and each of the nine `3 × 3` sub-grids that compose the grid all contain all of the numbers from `1` to `9` one time.

Implement an algorithm that will check whether the given grid of numbers represents a valid Sudoku puzzle according to the layout rules described above. Note that the puzzle represented by grid does not have to be solvable.

**Example**

For
```
grid = [['.', '.', '.', '1', '4', '.', '.', '2', '.'],
        ['.', '.', '6', '.', '.', '.', '.', '.', '.'],
        ['.', '.', '.', '.', '.', '.', '.', '.', '.'],
        ['.', '.', '1', '.', '.', '.', '.', '.', '.'],
        ['.', '6', '7', '.', '.', '.', '.', '.', '9'],
        ['.', '.', '.', '.', '.', '.', '8', '1', '.'],
        ['.', '3', '.', '.', '.', '.', '.', '.', '6'],
        ['.', '.', '.', '.', '.', '7', '.', '.', '.'],
        ['.', '.', '.', '5', '.', '.', '.', '7', '.']]
```
the output should be
`sudoku2(grid) = true`;

For

```
grid = [['.', '.', '.', '.', '2', '.', '.', '9', '.'],
        ['.', '.', '.', '.', '6', '.', '.', '.', '.'],
        ['7', '1', '.', '.', '7', '5', '.', '.', '.'],
        ['.', '7', '.', '.', '.', '.', '.', '.', '.'],
        ['.', '.', '.', '.', '8', '3', '.', '.', '.'],
        ['.', '.', '8', '.', '.', '7', '.', '6', '.'],
        ['.', '.', '.', '.', '.', '2', '.', '.', '.'],
        ['.', '1', '.', '2', '.', '.', '.', '.', '.'],
        ['.', '2', '.', '.', '3', '.', '.', '.', '.']]
```
the output should be
`sudoku2(grid) = false`.

The given grid is not correct because there are two 1s in the second column. Each column, each row, and each `3 × 3` subgrid can only contain the numbers `1` through `9` one time.

**Input/Output**

* **[execution time limit] 3 seconds (java)**

* **[input] array.array.char grid**

A `9 × 9` array of characters, in which each character is either a digit from `'1'` to `'9'` or a period `'.'`.

* **[output] boolean**

Return `true` if grid represents a valid Sudoku puzzle, otherwise return `false`.


## Solution
```Java
boolean sudoku2(char[][] grid) {
    for(int i = 0; i < grid.length; i++){
        for(int j =0; j < grid.length; j++){
            if(grid[i][j]== '.')
                continue;
            for(int m = i+1; m < grid.length; m++)
                if(grid[i][j]==grid[m][j])
                    return false;
            for(int n = j+1; n < grid.length; n++)
                if(grid[i][j]==grid[i][n])
                    return false;
            for(int bi=(i/3)*3; bi< (i/3)*3+3; bi++){
                for(int bj=(j/3)*3; bj< (j/3)*3+3; bj++){
                    if((i != bi || j !=bj)&&
                       grid[i][j]==grid[bi][bj])
                    return false;
                }
            }
        }
    }
    return true;
}
```
