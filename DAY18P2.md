# Avoid Flood in The City
---
- ## Question:
>Your country has an infinite number of lakes. Initially, all the lakes are empty, but when it rains over the nth lake, the nth lake becomes full of water. If it rains over a lake that is full of water, there will be a flood. Your goal is to avoid floods in any lake.
>Given an integer array rains where:

>- rains[i] > 0 means there will be rains over the rains[i] lake.
>- rains[i] == 0 means there are no rains this day and you can choose one lake this day and dry it.
>
>Return an array ans where:

>- ans.length == rains.length
>- ans[i] == -1 if rains[i] > 0.
>- ans[i] is the lake you choose to dry in the ith day if rains[i] == 0.
>
>If there are multiple valid answers return any of them. If it is impossible to avoid flood return an empty array.
>
>Notice that if you chose to dry a full lake, it becomes empty, but if you chose to dry an empty lake, nothing changes.
---
- ## Example:
>Input: rains = [1,2,3,4]
>
>Output: [-1,-1,-1,-1]
>
>Explanation: After the first day full lakes are [1]
>
>After the second day full lakes are [1,2]
>
>After the third day full lakes are [1,2,3]
>
>After the fourth day full lakes are [1,2,3,4]
>
>There's no day to dry any lake and there is no flood in any lake.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int[] avoidFlood(int[] rains) {
        // the previous appeared idx of rains[i]
        Map<Integer, Integer> map = new HashMap<>();
        TreeSet<Integer> zeros = new TreeSet<>();
        int[] res = new int[rains.length];
        for (int i = 0; i < rains.length; i++) {
            if (rains[i] == 0) {
                zeros.add(i);
            } else {
                if (map.containsKey(rains[i])) {
                    // find the location of zero that can be used to empty rains[i]
                    Integer next = zeros.ceiling(map.get(rains[i]));
                    if (next == null) return new int[0];
                    res[next] = rains[i];
                    zeros.remove(next);
                }
                res[i] = -1;
				map.put(rains[i], i);
            }
        }
        for (int i : zeros) res[i] = 1;
        return res;
    }
}
