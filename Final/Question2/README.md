a.	Part 1 Define the problem/solution recursively – The recursive definition for the Minimum Falling Path sum is the following. Dynamic programming is the best candidate to solve this problem, since the subproblems can be used to solve larger instances of this problem. What this problem is asking of us is to find the minimum sum from the first row to last. So, what we want to do is to store the minimum sum of each possible path to that index. That way we would not have to do the sum of each index over and over again.
b.	Part 2 Plan – I plan to use a double int array(dp[i][j]), and in which we would be storing each min sum into.  I will be using the grid to store the first row of the given double array, this would be our first instance of the problem and we don’t need to find any sums since there is no integers above it (dp[o][i] = A[0][i]). I will be storing the rest of the indexes by using dp(i, j) = A[i][j] + min(dp(i+1,j-1), dp(i+1, j), dp(i+1, j+1)).


    public int minFallingPathSum(int[][] A) {
             int m = A.length; int n = A[0].length;
        int[][] dp = new int[m][n];    
        for(int i = 0; i < n; i++){
            dp[0][i] = A[0][i];
        }
        int min = Integer.MAX_VALUE;
        for(int i = 1; i < m; i++){
            for(int j = 0; j < n; j++){
                if(j == 0){
                    dp[i][j] = A[i][j] + Math.min(dp[i-1][j], dp[i-1][j+1]);
                }
                else if(j == n-1){
                    dp[i][j] = A[i][j] + Math.min(dp[i-1][j], dp[i-1][j-1]);
                }
                else if(j > 0 && j < n-1 ) {
                    dp[i][j] = A[i][j] + Math.min(dp[i-1][j-1],Math.min(dp[i-1][j], dp[i-1][j+1]));
                }                
            }
        }
        for(int i : dp[m-1]){
            min = Math.min(min, i);
        }
        return min;

    }
