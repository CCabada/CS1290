a.	Part 1 Define the problem/solution recursively – The recursive definition of the problem is the following.  We are being asked to look for all possible integer breaks to decide the one that maximizes the product. Let’s make n=10, we can divide it into pairs (4,6),(3,7),(5,5) etc, which can further be divided like (4,6) -> ((2,2),(3,3)) . Thus, this problem is a very good candidate for Dynamic programming. Also since (4,6) -> ((2,2), (3,3)) and (2,8)->(2,(2,(3,3))) hence we are solving repeatedly for (2) and (3) hence it has an overlapping subproblem property too. To avoid this, we save the solutions into an index of dp[] respectively.



b.	Part 2 Plan – My plan is to use an array to save all the work done, and eventually return the max. We can start of by defining what is the easiest instance is, that’s when dp[1] = 1. We also know that our terminating condition when n<= 0. Our recursive definition is k=1..n/2 dp [n] = Max of all the values for Max(n-kk), n-integerBreak(k), integerBreak(n-k)*k.



    int[] dp;
    
    public int helper(int n){
        if(n <= 0)
            return 1;
        
        if(dp[n] > 0)
            return dp[n];
        
        int max = 0;
        for(int i=1;i<n;i++){
            int val = Math.max((n-i)*i,Math.max((n-i)*helper(i),Math.max(helper(n-i)*i,helper(n-i)*helper(i))));
            if(val > max)
                max = val;
        }
        
        dp[n] = max;
        return max;
    }
    public int integerBreak(int n) {
        
        if(n == 0)
            return 1;
        
        dp = new int[n+1];
        dp[1] = 1;
        dp[0] = 0;
        return helper(n);
    }
