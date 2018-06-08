# Adjacent Elements Product

Code fight problem and its solution which is solved by me - Duy Huynh.

## Problem

Given an array of integers, find the pair of adjacent elements that has the largest product and return that product.

**Example**

For `inputArray = [3, 6, -2, -5, 7, 3]`, the output should be
`adjacentElementsProduct(inputArray) = 21`.

`7` and `3` produce the largest product.

**Input/Output**

* **[execution time limit] 3 seconds (java)**

* **[input] array.integer inputArray**

    An array of integers containing at least two elements.

    Guaranteed constraints:
    `2 ≤ inputArray.length ≤ 10`,
    `-1000 ≤ inputArray[i] ≤ 1000`.

* **[output] integer**

    The largest product of adjacent elements.


## Solution

```Java
int adjacentElementsProduct(int[] inputArray) {
    int max = inputArray[0]* inputArray[1];
    for(int i = 0; i < inputArray.length-1; i++){
        if(inputArray[i]* inputArray[i+1]> max)
            max = inputArray[i]* inputArray[i+1];
    }
    return max;
        
}
```
