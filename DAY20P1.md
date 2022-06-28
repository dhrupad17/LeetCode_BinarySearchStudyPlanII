# Ugly Number III
---
- ## Question:
> An ugly number is a positive integer that is divisible by a, b, or c.
> 
> Given four integers n, a, b, and c, return the nth ugly number.
---
- ## Example:
> Input: n = 3, a = 2, b = 3, c = 5
> 
> Output: 4
> 
> Explanation: The ugly numbers are 2, 3, 4, 5, 6, 8, 9, 10... The 3rd is 4.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int nthUglyNumber(int n, int a, int b, int c) {
        int MAX_ANS=(int)(2e9);
        int left=0;
        int right=MAX_ANS;
        int res=0;
        while(left<=right)
        {
            int mid=left+(right-left)/2;
            if(count(mid,a,b,c)>=n)
            {
                res=mid;
                right=mid-1;
            }
            else
            {
                left=mid+1;
            }
        }
        return res;
    }
    public int count(long num,long a,long b,long c)
    {
        return (int) (num/a +num/b+ num/c - num/lcm(a,b) - num/lcm(b,c) - num/lcm(a,c) + num/lcm(a,lcm(b,c)));
    }
    long gcd(long a,long b)
    {
        if(a==0)
            return b;
        return gcd(b%a,a);
    }
    long lcm(long a,long b)
    {
        return a*b/gcd(a,b);
    }
}
