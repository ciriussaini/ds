**What is recursion/memoization(top-down)/bottom up ? Optimal Sub-Structure and Overlapping Sub-Problems**
https://medium.com/swlh/understanding-recursion-memoization-and-dynamic-programming-3-sides-of-the-same-coin-8c1f57ee5604 </br>
**Recursion** : simple solution : base condition always there </br>
**Memoized** : recursion but we store previous values </br> (top/down)
**DP** : via for loops we can say or bottom up</br> 

**HouseStolen problem
So there are two cases:

    If an element is selected then the next element cannot be selected.
    if an element is not selected then the next element can be selected.
    bottom up
```
int maxLoot(int* hval, int n) 
{ 
    if (n == 0) 
        return 0; 
    if (n == 1) 
        return hval[0]; 
    if (n == 2) 
        return max(hval[0], hval[1]); 
  
    // dp[i] represent the maximum value stolen 
    // so far after reaching house i. 
    int dp[n]; 
  
    // Initialize the dp[0] and dp[1] 
    dp[0] = hval[0]; 
    dp[1] = max(hval[0], hval[1]); 
  
    // Fill remaining positions 
    for (int i = 2; i < n; i++) 
        dp[i] = max(hval[i] + dp[i - 2], dp[i - 1]); 
  
    return dp[n - 1]; 
} 
```

edit distance
***Choosing Correct size of Table: <br>
The size of the 2D table will be equal to the total number of different subproblems, which is equal to (m + 1)*(n + 1). As both m and n are decreasing by 1 during the recursive calls and reaching the value 0. So m + 1 possibilities for the first parameter and n + 1 possibilities for the second parameter. Total number of possible subproblems = (m + 1)*(n + 1).
<br>
***3. Filling the table: <br> It consist of two stages, table initialization and building the solution from the smaller subproblems:
<br>
    Table initialization: Before building the solution, we need to initialize the table with the smaller version of the solution i.e. base case. Here m = 0 and n = 0 is the situation of the base case, so we initialize first-column dp[i][0] with i and first-row dp[0][j] with j.
    <br>Building the solution of larger problems from the smaller subproblems: We can easily define the iterative structure by using the recursive structure of the above recursive solution.
<br>
```
int editDistDP(string str1, string str2, int m, int n)
{
    // Create a table to store results of subproblems
    int dp[m + 1][n + 1];
 
    // Fill d[][] in bottom up manner
    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            // If first string is empty, only option is to
            // insert all characters of second string
            if (i == 0)
                dp[i][j] = j; // Min. operations = j
 
            // If second string is empty, only option is to
            // remove all characters of second string
            else if (j == 0)
                dp[i][j] = i; // Min. operations = i
 
            // If last characters are same, ignore last char
            // and recur for remaining string
            else if (str1[i - 1] == str2[j - 1])
                dp[i][j] = dp[i - 1][j - 1];
 
            // If the last character is different, consider
            // all possibilities and find the minimum
            else
                dp[i][j]
                    = 1
                      + min(dp[i][j - 1], // Insert
                            dp[i - 1][j], // Remove
                            dp[i - 1][j - 1]); // Replace
        }
    }
 
    return dp[m][n];
}
```
