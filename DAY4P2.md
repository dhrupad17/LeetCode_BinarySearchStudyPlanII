# Magnetic Force Between Two Balls
---
- ## Question
---
>In the universe Earth C-137, Rick discovered a special form of magnetic force between two balls if they are put in his new invented basket. Rick has n empty baskets, the ith basket is at position[i], Morty has m balls and needs to distribute the balls into the baskets such that the minimum magnetic force between any two balls is maximum.
>
>Rick stated that magnetic force between two different balls at positions x and y is |x - y|.
>
>Given the integer array position and the integer m. Return the required force.
---
- ## Example
---
![alt text](https://assets.leetcode.com/uploads/2020/08/11/q3v1.jpg)
>Input: position = [1,2,3,4,7], m = 3
>
>Output: 3
>
>Explanation: Distributing the 3 balls into baskets 1, 4 and 7 will make the magnetic force between ball pairs [3, 3, 6]. The minimum magnetic force is 3. We cannot achieve a larger minimum magnetic force than 3.
---
- ## Solution:
**Code :**
```java
class Solution {
      public int maxDistance(int[] position, int m) {
        Arrays.sort(position);
        int low=1;
        int high=position[position.length-1]-position[0];
        
        int ans=0;
        while(low<=high){
            int mid=low+(high-low)/2;
            
            if(validate(position, mid, m)){
                ans=mid;
                low=mid+1;
            }
            else{
                high=mid-1;
            }
        }
        
        return ans;
        
    }
    
    public boolean validate(int position[], int x, int count){
        
        int prev=position[0];
        count--;
        for(int i=1;i<position.length;i++){
            if(position[i]-prev >=x){
                count--;
                if(count==0){
                    return true;
                }
                prev=position[i];
            }
        }
        
        return count==0;
    }
}
