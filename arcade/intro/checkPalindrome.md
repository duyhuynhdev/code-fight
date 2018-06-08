# Check Palindrome

Code fight problem and its solution which solved by me - Duy Huynh.

## Problem

Given the string, check if it is a palindrome.

**Example**

* For `inputString = "aabaa"`, the output should be
  `checkPalindrome(inputString) = true`;
* For `inputString = "abac"`, the output should be
  `checkPalindrome(inputString) = false`;
* For `inputString = "a"`, the output should be
  `checkPalindrome(inputString) = true`.

**Input/Output**

* **[execution time limit] 3 seconds (java)**

* **[input] string inputString**

    A non-empty string consisting of lowercase characters.

    Guaranteed constraints:
    `1 ≤ inputString.length ≤ 105`.

* **[output] boolean**

    `true` if `inputString` is a palindrome, `false` otherwise.

## Solution

```Java
boolean checkPalindrome(String inputString) {
    if(inputString.length() == 1)
        return true;
    int i = 0; 
    int j = inputString.length() - 1;
    while( i < j ){
       if(inputString.charAt(i) != inputString.charAt(j))
           return false;
       i++;
       j--;
    }
    return true;
}
```
