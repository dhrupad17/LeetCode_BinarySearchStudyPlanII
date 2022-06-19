# Most Profit Assigning Work
---
- ## Question
>You have n jobs and m workers. You are given three arrays: difficulty, profit, and worker where:
>
>- difficulty[i] and profit[i] are the difficulty and the profit of the ith job, and
>
>- worker[j] is the ability of jth worker (i.e., the jth worker can only complete a job with difficulty at most worker[j]).
>
>Every worker can be assigned at most one job, but one job can be completed multiple times.
>
>- For example, if three workers attempt the same job that pays $1, then the total profit will be $3. If a worker cannot complete any job, their profit is $0.
>
>Return the maximum profit we can achieve after assigning the workers to the jobs.
---
- ## Example 
>Input: difficulty = [2,4,6,8,10], profit = [10,20,30,40,50], worker = [4,5,6,7]
>
>Output: 100
>
>Explanation: Workers are assigned jobs of difficulty [4,4,6,6] and they get a profit of [20,20,30,30] separately.
---
- ## Solution:
**Code :**
```java
class Solution {
    public int maxProfitAssignment(int[] difficulty, int[] profit, int[] worker) {
        int worksLength = profit.length;
        int[][] works = new int[worksLength][2];
        for(int i =0;i<worksLength;i++){
            works[i][0]=difficulty[i];
            works[i][1]=profit[i];
        }
        Arrays.sort(works,(a,b)-> a[0]-b[0]);

        int res = 0;
        for(int i =0;i<worker.length;i++){
            int ability =worker[i];
            int index = search(works,ability,worksLength);
            if(works[index][0]<=ability) index++;
            int best = 0;
            for(int j =0;j<index;j++){
                best=Math.max(best,works[j][1]);
            }
            res+=best;
        }
        return res;
    }
    
    public int search(int[][] works,int ability,int worksLength){
        int left = 0;
        int right = worksLength-1;
        while(left<right){
            int mid = left+(right-left)/2;
            int workDifficulty = works[mid][0];
            if(workDifficulty>ability) right = mid;
            else left = mid+1;
        }
        return left;
    }
}
