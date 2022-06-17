# Maximum Number of Removable Characters
---
- ## Question
---
>You are given two strings s and p where p is a subsequence of s. You are also given a distinct 0-indexed integer array removable containing a subset of indices of s (s is also 0-indexed).
>
>You want to choose an integer k (0 <= k <= removable.length) such that, after removing k characters from s using the first k indices in removable, p is still a subsequence of s. More formally, you will mark the character at s[removable[i]] for each 0 <= i < k, then remove all marked characters and check if p is still a subsequence.
>
>Return the maximum k you can choose such that p is still a subsequence of s after the removals.
>
>A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.
---
- ## Example
---
>Input: s = "abcacb", p = "ab", removable = [3,1,0]
>
>Output: 2
>
>Explanation: After removing the characters at indices 3 and 1, "abcacb" becomes "accb".
"ab" is a subsequence of "accb".
If we remove the characters at indices 3, 1, and 0, "abcacb" becomes "ccb", and "ab" is no longer a subsequence.
>
>Hence, the maximum k is 2.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int maximumRemovals(String s, String p, int[] removable) {
        char letters[]=s.toCharArray();
        int low=0;
        int high=removable.length;
        while(low<=high)
        {
            int mid=(low+high)/2;
            for(int i=0;i<mid;i++)
            {
                letters[removable[i]]='/';
            }
            if(check(letters,p))
            {
                low=mid+1;
            }
            else
            {
                for(int i=0;i<mid;i++)
                {
                    letters[removable[i]]=s.charAt(removable[i]);
                }
                high=mid-1;
            }
        }
        return high;
    }
    public boolean check(char[] letters, String p)
    {
        int i1=0;
        int i2=0;
        while(i1<letters.length && i2 <p.length())
        {
            char c1=letters[i1];
            char c2=p.charAt(i2);
            if(c1!='/' && c1==c2)
            {
                i2++;
            }
            i1++;
        }
        if(i2==p.length())
            return true;
        else
            return false;
    }
}
