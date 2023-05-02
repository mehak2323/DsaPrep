#### Question
[Problem Link](https://atcoder.jp/contests/dp/tasks/dp_b) /
[Video Link](https://www.youtube.com/watch?v=Kmh3rhyEtB8&list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY&index=5&pp=iAQB)

There are N stones, numbered 1,2,…,N. For each i (1 ≤ i ≤N), the height of Stone i is h<sub>i</sub>.

There is a frog who is initially on Stone 1. He will repeat the following action some number of times to reach Stone N:
- If the frog is currently on Stone i, jump to one of the following: Stone i+1,i+2,…,i+K. Here, a cost of ∣ h <sub>i</sub> − h <sub>j</sub> ∣ is incurred, where j is the stone to land on.

Find the minimum possible total cost incurred before the frog reaches Stone N.

#### Solution
Recurrence: fn(n) = abs(cost\[n]-cost\[n-k]) + min(fn(n-1), fn(n-2), ..., fn(n-k))

- Memoization (rough, not code):
```
int funDp(cost[], dp[], i){
    if(n==0) return 0; //base case, no cost to reach first place
    if(dp[i]!=-1) return dp[i]; // if dp exist, return

    int curr_min, curr_cost;
    //for curr step, check min cost of jumping from last k steps
    for(int j=1; j<=k; j++){
        //check if less than k step exist before current one
        if(i-j>=0){
            curr_cost = funDp(i-j) + abs(cost[i] - cost[i-j]);
        }
        //Update minimum of last k jumps
        if(curr_cost < curr_min) curr_min = curr_cost;
    }
    dp[i] = curr_min;
    return dp[i];
}
```
`Time: O(n*k)` / 
`Space: O(n) + O(n) (recursion stack)`

- DP:
```
fun(cost[]){
    int[] dp = new int[n];
    dp[0] = 0;
    for(int i=1; i<n; i++){
        int curr_min, curr_cost;
        for(int j=1; j<=k; j++){
            if(i-j>=0)
                curr_cost = dp[i-j] + abs(cost[i] - cost[i-j]);
            curr_min = min(curr_min, curr_cost);
        }
        dp[i] = curr_min;
    }
    return dp[n-1];
}
```

`Time: O(n*k)` / 
`Space: O(n) ` 

Can space optimize O(n) to O(k), by only storing last k costs. But worst case is O(n) if k=n.
