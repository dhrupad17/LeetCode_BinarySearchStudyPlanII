#  H-Index II
---
- ## Question
---
>Given an array of integers citations where citations[i] is the number of citations a researcher received for their ith paper and citations is sorted in an ascending order, return compute the researcher's h-index.
>
>According to the definition of h-index on Wikipedia: A scientist has an index h if h of their n papers have at least h citations each, and the other n − h papers have no more than h citations each.
>
>If there are several possible values for h, the maximum one is taken as the h-index.
>
>You must write an algorithm that runs in logarithmic time.
---
- ## Example
---
>Input: citations = [0,1,3,5,6]
>
>Output: 3
>
>Explanation: [0,1,3,5,6] means the researcher has 5 papers in total and each of them had received 0, 1, 3, 5, 6 citations respectively.
>
>Since the researcher has 3 papers with at least 3 citations each and the remaining two with no more than 3 citations each, their h-index is 3.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int hIndex(int[] citations) {
        int low=0;
        int len=citations.length;
        int high=len-1;
        while(low<=high)
        {
            int mid=(low+high)/2;
            if(citations[mid]== len-mid)
                return len-mid;
            else if(citations[mid]<len-mid)
                low=mid+1;
            else
                high=mid-1;
        }
        return len-low;
    }
}
