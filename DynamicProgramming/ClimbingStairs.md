[Leetcode](https://leetcode.com/problems/climbing-stairs/description/)

You are climbing a staircase. It takes n steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?


```
class Solution {
public:

    //Memoised
    void climbStairsDp(int n, vector<int> &dp){
        if(n<=0) {
            dp[0]=0;
            return;
        }
        if(n<=2) {
            dp[n]=n;
            return;
        }

        if(dp[n-1]==-1){
            climbStairsDp(n-1, dp);
        }
        if(dp[n-2]==-1){
            climbStairsDp(n-2, dp);
        }

        if(dp[n]==-1)
            dp[n] = dp[n-1] + dp[n-2];
    }

    int climbStairs(int n) {
        vector<int> dp(n+1, -1);
        climbStairsDp(n, dp);
        return dp[n];
    }
};

/*
//DP, done earlier
    int climbStairs(int n) {
        
        //Since recursion relation will be f(n-1) + f(n-2)
        //which is like fibonacci, do bottom up fibonacci computing
        
        //base case
        if(n<=2) return n;
        
        //1 way to reach 1st stair, 2 ways for 2nd stair
        int prev1=2, prev2=1, curr_ways=0;
        
        //Loop for remaining stairs
        for(int i=3; i<=n; i++){
            //current n ways is sum of previous two
            curr_ways = prev1 + prev2;
            //update previous two
            prev2 = prev1;
            prev1 = curr_ways;
        }
        
        return curr_ways;
    }
*/


/*
//Recursion, TLE:

    int climbStairs(int n) {
        if(n<=0) return 0;
        if(n<=2) return n;
        
        int oneStepPrev = climbStairs(n-1);
        int twoStepPrev = climbStairs(n-2);

        return oneStepPrev + twoStepPrev;
    }
*/
```


 0 | 1 | 2 | 3 | 4 | 5
 
 0 | 1 | 2 | 3 | 5 | 8 

 
FULL: 13 21 34 55 89 144 233 377 610 987 1597 2584 4181 6765 10946 17711 28657 46368 75025 121393 196418 317811 514229 832040 1346269 2178309 3524578 5702887 9227465 14930352 24157817 39088169 63245986 102334155 165580141 267914296 433494437 701408733 1134903170 1836311903 
