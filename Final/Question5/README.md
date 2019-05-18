a.	Part 1 Define the problem/solution recursively – The following is the recursive definition of the problem. We need to find the longest chain that can be formed.  To do this we need to sort the pairs. For this solution I need an array to keep track of longest chain of pair that can be made dp[i] = max(dp[i],dp[j]+1). 

b.	Part 2 Plan – My plan is to first sort every pair of the given set. Once everything is sorted, let dp[i] be the length of the longest chain ending at pairs[i]. When i < j and pairs[i][1] < pairs[j][0], we can extend the chain, and so we have the candidate answer dp[j] = max(dp[j], dp[i] + 1).

6.	def findLongestChain(self, pairs: List[List[int]]) -> int:
7.	        pairs.sort()
8.	        mx,N=1,len(pairs)
9.	        dp=[1]*N
10.	        for i in range(N):
11.	            for j in range(i):
12.	                if pairs[i][0]>pairs[j][1]:
13.	                    dp[i] = max(dp[i],dp[j]+1)
14.	        
15.	        for i in range(N):
16.	            mx = max(mx,dp[i])
