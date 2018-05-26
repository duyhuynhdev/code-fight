# firstNotRepeatingCharacter

## Problem

*Note: Write a solution that only iterates over the string once and uses O(1) additional memory, since this is what you would be asked to do during a real interview.*

Given a string `s`, find and return the first instance of a non-repeating character in it. If there is no such character, return `'_'`.

**Example**

* For `s = "abacabad"`, the output should be `firstNotRepeatingCharacter(s) = 'c'`.

  There are `2` non-repeating characters in the string: `'c'` and `'d'`. Return c since it appears in the string first.

* For `s = "abacabaabacaba"`, the output should be `firstNotRepeatingCharacter(s) = '_'`.

  There are no characters in this string that do not repeat.
  
**Input/Output**

* **[execution time limit] 3 seconds (java)**

* **[input] string s**

  A string that contains only lowercase English letters.

  Guaranteed constraints:
  `1 ≤ s.length ≤ 10^5 `.

* **[output] char**

  The first non-repeating character in `s`, or `'_'` if there are no characters that do not repeat.`
  
## First Approach
For solving the problem, we start from our common behavior. That means we will follow the algorithm in our brain. In general, we scan each character `ch` from left to right of string `s` and consider whether this char appeared before or not. If not, we will keep it in mind (mark it) as a new candidate. `The best candidate` is the most left one. If the considered chart `ch` appeared before, we will unmark it (remove from candidate list) and select the next one in candidate list as `the best candidate`. After scanning all char in string `s`, if the candidate list empty `return `'_'`, if not, `return the best candidate`.

For implementation, we know that `s contains only lowercase English letters`. That means `s` contains  `a-z`. In ASCII, we have the range `97-123` stand for `a-z` in ASCII. So we will use an `int[26]` as array for `the flag of appearance`. We also has a `candidate` list. The full solution is shown in the next section.
## Final Solution
  ```Java
  char firstNotRepeatingCharacter(String s) {
    int[] appeareance = new int[26];
    ArrayList<Integer> notrepeat = new ArrayList<>();
    for(char ch: s.toCharArray()){
        int ascii = (int)ch;
        int a_idx = ascii-97;
        if(appeareance[a_idx] == 0){
            notrepeat.add(a_idx+1);
            appeareance[a_idx] = notrepeat.size();
        }else if(appeareance[a_idx] > 0 ){
            if(notrepeat.get(appeareance[a_idx]-1)>=0)
            notrepeat.set(appeareance[a_idx]-1, notrepeat.get(appeareance[a_idx]-1) *-1);
        }
    }
    for(Integer i : notrepeat){
        if(i > 0)
            return (char)((i-1)+97);
    }
    return '_';
  }
```
> **Result:** 22/22 All tests passed<br>
> **Sample tests:** 11/11<br>
> **Hidden tests:** 11/11<br>
> **Score:** 300/300<br>
## Pretty Code
  
 
