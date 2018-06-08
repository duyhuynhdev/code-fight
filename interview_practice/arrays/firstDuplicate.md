# firstDuplicate

## Problem

Given an array a that contains only numbers in the range from 1 to a.length, find the first duplicate number for which the second occurrence has the minimal index. In other words, if there are more than 1 duplicated numbers, return the number for which the second occurrence has a smaller index than the second occurrence of the other number does. If there are no such elements, return -1.

**Example**

* For `a = [2, 1, 3, 5, 3, 2`], the output should be
`firstDuplicate(a) = 3`.

  There are 2 duplicates: numbers `2` and `3`. The second occurrence of `3` has a smaller index than the second occurrence of `2` does, so the answer is `3`.

* For `a = [2, 4, 3, 5, 1]`, the output should be
`firstDuplicate(a) = -1`.

**Input/Output**

* **[execution time limit] 3 seconds (java)**

* **[input] array.integer a**

* **Guaranteed constraints:**
`1 ≤ a.length ≤ 10^5`,
`1 ≤ a[i] ≤ a.length`.

* **[output] integer**

  The element in a that occurs in the array more than once and has the minimal index for its second occurrence. If there are no such elements, return `-1`.

## First approach

```Java
int firstDuplicate(int[] a) {
    int idx = a.length;
    for(int i =0; i < idx; i++){
        for(int j = i+1; j < idx; j++){
            if(a[i]==a[j]) {
                idx = j;
                break;                    
            }
        }
    }
    if(idx != a.length)
        return a[idx];
    return -1;
}
```
> **Result:** 21/22 Execution time limit exceeded on test 22: Program exceeded the execution time limit. Make sure that it completes execution in a few seconds for any possible input.<br>
> **Sample tests:** 11/11<br>
> **Hidden tests:** 10/11<br>
> **Score:** 214/300<br>

## Diagnose the problem

The reason why test case 22 false is the time limit exceeding because we use two for loop in the previous solution. So now we try to find another solution. Generally, our behavior is scanning from left to right of an array and checking whether the value in current index appear before or not. If yes, we will return this value. Otherwise, return `-1`. However, in this solution, we also use one loop for checking the appearance of current value, therefore, it also contains 2 for loops. For decreasing the number of loop, we should use an array for saving the values which appeared before. The critical point is `1 ≤ a[i] ≤ a.length` that means we can use an array has the same length for tracking a value in `a[]`. Hence, we create a `flag[]` which has the value is true if the `index+1` of `flag[]` has been seen before in `a`. For example, if `2` appear before in `a`, `flag[1] = true`.  We scan `a[]` with only one for loop and if `flag[a[i]-1] == true` that means `a[i]` appeared before, so we can `return a[i]`. The full script of this solution is shown in the next section.

## Final solution

```Java
int firstDuplicate(int[] a) {
    boolean[] flag = new boolean[a.length];
    for(int i = 0; i < a.length; i++){
        if(flag[a[i]-1] == true) return a[i];
       flag[a[i]-1] = true;
    }   
    return -1;
}
```
> **Result:** 22/22 All tests passed<br>
> **Sample tests:** 11/11<br>
> **Hidden tests:** 11/11<br>
> **Score:** 300/300<br>

## Optimized solution

In this solution we use  exactly `a[]` as the `flag[]`. Because `a[i] > 0` for all case so we use `-a[i]` as `flag` for the appearance of value `i`. 
```Java
int firstDuplicate(int[] a) {
    for(int i = 0; i < a.length; i++){
        if(a[a[i]-1] < 0) return a[i];
       a[a[i]-1] = -1 * a[a[i]-1] ;
    }   
    return -1;
}
```
