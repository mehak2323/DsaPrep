[Problem link leetcode](https://leetcode.com/problems/min-cost-climbing-stairs/description/) \
[Problem Link coding ninjas](https://www.codingninjas.com/codestudio/problems/frog-jump_3621012?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos) \
[Video Link](https://www.youtube.com/watch?v=EgG3jsGoPvQ&list=PLgUwDviBIf0pwFf-BnpkXxs0Ra0eU2sJY&index=2)

Minimum total energy used for frog to reach from 1st stair to Nth stair.

You are given an integer array cost where cost[i] is the cost of ith step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index 0, or the step with index 1.

Return the minimum cost to reach the top of the floor.


DP, java: 
```
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int n = cost.length;
        int[] dp = new int[n];

        for(int i=0; i<n; i++){
            if(i<=1) dp[i] = cost[i];
            else dp[i] = cost[i] + Math.min(dp[i-1], dp[i-2]);
        }

        return Math.min(dp[n-1],dp[n-2]);
    }
}
```

//Memoisation, C++

```
class Solution {
public:
    void minCostDp(vector<int>& cost, int i, vector<int> &dp) {
        if(i<=1 || dp[i]!=-1) return;

        if(dp[i-1]==-1) minCostDp(cost, i-1, dp);
        if(dp[i-2]==-1) minCostDp(cost, i-2, dp);

        dp[i] = cost[i] + min(dp[i-1], dp[i-2]);
    }

    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size();
        vector<int> dp(n,-1);
        dp[0] = cost[0];
        dp[1] = cost[1];
        minCostDp(cost,n-1,dp);

        cout<<"Final dp: ";
        for(auto itr: dp)
            cout<<itr<<" ";

        return min(dp[n-1],dp[n-2]);
    }
};
```

Example 1:

Input: cost = [10,15,20]
Output: 15
Explanation: You will start at index 1.
- Pay 15 and climb two steps to reach the top.
The total cost is 15.


Example 2:

Input: cost = [1,100,1,1,1,100,1,1,100,1]
Output: 6
Explanation: You will start at index 0.
- Pay 1 and climb two steps to reach index 2.
- Pay 1 and climb two steps to reach index 4.
- Pay 1 and climb two steps to reach index 6.
- Pay 1 and climb one step to reach index 7.
- Pay 1 and climb two steps to reach index 9.
- Pay 1 and climb one step to reach the top.
The total cost is 6.


Starting from the end, only returning dp[n-1] won't work, even though I was trying from nth index going back 1 or 2 steps. For bottom up memoistion we'll need to call recursive function once starting from 0th index and once from 1st.

`Time complexity: O(n)` \
`Space Complexity: O(n)`
