# Random Pick with Weight
---
- ## Question:
> You are given a 0-indexed array of positive integers w where w[i] describes the weight of the ith index.
> You need to implement the function pickIndex(), which randomly picks an index in the range [0, w.length - 1] (inclusive) and returns it. The probability of picking an index i is w[i] / sum(w).
> - For example, if w = [1, 3], the probability of picking index 0 is 1 / (1 + 3) = 0.25 (i.e., 25%), and the probability of picking index 1 is 3 / (1 + 3) = 0.75 (i.e., 75%).
---
- ## Example:
>Input
["Solution","pickIndex"]
[[[1]],[]]

>Output
[null,0]

>Explanation
Solution solution = new Solution([1]);
solution.pickIndex(); // return 0. The only option is to return 0 since there is only one element in w.
---
- ## Solution:
**Code :**
```java
class Solution {
    private final TreeMap<Integer, Integer> map;
    private final Random random = new Random(System.currentTimeMillis());
    private int sum = 0;
    public Solution(int[] w) {
         map = new TreeMap<>();
        for (int i = 0; i < w.length; i++) {
            sum += w[i];
            map.put(sum, i);
        }
    }
    
    public int pickIndex() {
        return map.get(map.higherKey(random.nextInt(sum)));
    }
}
