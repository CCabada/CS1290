a.	Part 1 Define the problem/solution recursively – The recursive definition for the Palindromic Substrings is the following. What this question is asking is that we need to find all the possible palindromes in a string. Let's assume boolean array dp[i][j] represents if substring from ith to jth characters is a palindrome or not. Then we can get the transition function: dp[i][j] = dp[i + 1][j - 1], when (i < 3 || dp[i - 2][j + 1]) && (s.charAt(j) == s.charAt(j + i)), it is also valid. We simply count the palindromes and return the final number.


•	Part 2 Plan –I plan on using a double Boolean array dp, in which we store if they are palindromes.  Basically, we look for all length 1 palindromes, then all length 2 palindromes, then 3, … n. We try to build odd length palindromes off of previous odd length palindromes and even length palindromes off of previous even length palindromes, thus for a palindrome candidate of length i, we want to check the palindrome of length i - 2 (everything but the end characters), yielding a formula of dp[i - 2][j + 1].


class Solution {
    public int countSubstrings(String s) {
        int res = 0;
        int len =  s.length();
        boolean[][] dp = new boolean[len][len];
        
        for(int i = 0; i < len; i++){
            for(int j = 0; j < len - i; j++){
                dp[i][j] = (i < 3 || dp[i - 2][j + 1]) && (s.charAt(j) == s.charAt(j + i));
                if(dp[i][j]) res++;
            }
        }
        
        return res;
    }
}
