# Is Crypt Solution
Interview question asked by **Palantir Technologies**

## Problem
A *cryptarithm* is a mathematical puzzle for which the goal is to find the correspondence between letters and digits, such that the given arithmetic equation consisting of letters holds true when the letters are converted to digits.

You have an array of strings `crypt`, the cryptarithm, and an an array containing the mapping of letters and digits, `solution`. The array `crypt` will contain three non-empty strings that follow the structure: `[word1, word2, word3]`, which should be interpreted as the `word1 + word2 = word3` cryptarithm.

If `crypt`, when it is decoded by replacing all of the letters in the cryptarithm with digits using the mapping in `solution`, becomes a valid arithmetic equation containing no numbers with leading zeroes, the answer is `true`. If it does not become a valid arithmetic solution, the answer is `false`.

**Example**

For `crypt = ["SEND", "MORE", "MONEY"]` and
```
solution = [['O', '0'],
            ['M', '1'],
            ['Y', '2'],
            ['E', '5'],
            ['N', '6'],
            ['D', '7'],
            ['R', '8'],
            ['S', '9']]
```
the output should be
`isCryptSolution(crypt, solution) = true`.

When you decrypt `"SEND"`, `"MORE"`, and `"MONEY"` using the mapping given in crypt, you get `9567 + 1085 = 10652` which is correct and a valid arithmetic equation.

For crypt = `["TEN", "TWO", "ONE"]` and
```
solution = [['O', '1'],
            ['T', '0'],
            ['W', '9'],
            ['E', '5'],
            ['N', '4']]
```
the output should be
`isCryptSolution(crypt, solution) = false`.

Even though `054 + 091 = 145`, `054` and `091` both contain leading zeroes, meaning that this is not a valid solution.

**Input/Output**

* **[execution time limit] 3 seconds (java)**

* **[input] array.string crypt**

    An array of three non-empty strings containing only uppercase English letters.

    Guaranteed constraints:<br>
    `crypt.length = 3`,<br>
    `1 ≤ crypt[i].length ≤ 14`.<br>

* **[input] array.array.char solution**

  An array consisting of pairs of characters that represent the correspondence between letters and numbers in the cryptarithm. The first character in the pair is an uppercase English letter, and the second one is a digit in the range from `0` to `9`.

  Guaranteed constraints:<br>
  `solution[i].length = 2`,<br>
  `'A' ≤ solution[i][0] ≤ 'Z'`,<br>
  `'0' ≤ solution[i][1] ≤ '9'`,<br>
  `solution[i][0] ≠ solution[j][0], i ≠ j`,<br>
  `solution[i][1] ≠ solution[j][1], i ≠ j`.<br>

  It is guaranteed that `solution` only contains entries for the letters present in `crypt` and that different letters have different values.

* **[output] boolean**
  
  Return `true` if the solution represents the correct solution to the cryptarithm crypt, otherwise return `false`.
## Solution

```Java
boolean isCryptSolution(String[] crypt, char[][] solution) {
    int[] nums = new int[crypt.length];
    int idx = 0;
    for(String s : crypt){
        int num=0;
        for(int i = 0; i < s.length(); i++){
            for(char[] temp : solution){
                if(temp[0] == s.charAt(i)){
                    if(i==0 && temp[1] == '0' && s.length()>1)
                        return false;
                     num = num*10+ Character.getNumericValue(temp[1]);;
                     break;
                }
            }
        }
        nums[idx] = num;
        idx++;
    }
    
    return nums[0] + nums[1] == nums[2];
}
```
