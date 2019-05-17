a.	Part 1 Define the problem/solution recursively - The recursive definition of the stone game problem is the following. Initially we have an array representing the piles of stones, let’s give Alex the total number of stones. Then we subtract Alex’s score every time Lee scores points. If we think about dp(I, j ) as the largest score Alex can score with the piles remaining. The piles remaining will be piles[i], piles[i+1], …, piles[j]. By using dp(i+1, j) and dp(I , j-1) we can formulate the recursion so we wont repeat the work we already have done. This problem is a variation of the Min-Max set of problems.

b.	Part 2 Plan – We can determine who’s turn it is by comparing j-I to N % 2. N being the number of piles. If it’s Alex turn, we want to find the maximum score possible with the number of stones. he/she can either take piles[i] or piles[j], we find the max by adding piles[i] plus dp(i+1, j) or piles[j] + dp(I, j-1). If its Lee, we want to find the minimum number of stones. He could either take piles[i] or piles [j]. The total score is either -piles[i] + dp(i+1, j) or -piles[j] + dp(I, j-1). 


public static boolean stoneGame(int[] piles) {
    int N = piles.length;

    // dp[i+1][j+1] = the value of the game [piles[i], ..., piles[j]].
    int[][] dp = new int[N+2][N+2];
    for (int size = 1; size <= N; ++size)
        for (int i = 0; i + size <= N; ++i) {
            int j = i + size - 1;
            int parity = (j + i + N) % 2;  // j - i - N; but +x = -x (mod 2)
            if (parity == 1)
                dp[i+1][j+1] = Math.max(piles[i] + dp[i+2][j+1], piles[j] + dp[i+1][j]);
            else
                dp[i+1][j+1] = Math.min(-piles[i] + dp[i+2][j+1], -piles[j] + dp[i+1][j]);
        }

    return dp[1][N] > 0;
}
