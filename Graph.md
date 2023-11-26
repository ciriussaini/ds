##Toplogical Sort
https://leetcode.com/problems/parallel-courses-iii/
<br>
```
int minimumTime(int n, vector<vector<int>>& relations, vector<int>& time) {
        vector<int> inDegree(n);
        vector<vector<int>> graph(n, vector<int>());
        for (auto& edge : relations) {
            int prev = edge[0] - 1, next = edge[1] - 1;
            graph[prev].push_back(next);
            inDegree[next]++;
        }
        
        vector<int> dist(n);
        queue<int> q;
        for (int u = 0; u < n; ++u) {
            if (inDegree[u] == 0) {
                q.push(u);
                dist[u] = time[u];
            }
        }
        while (!q.empty()) {
            int u = q.front(); q.pop();
            for (int v : graph[u]) {
                dist[v] = max(dist[v], dist[u] + time[v]); // Update `dist[v]` using the maximum dist of the predecessor nodes
                if (--inDegree[v] == 0) 
                    q.push(v);
            }
        }
        return *max_element(dist.begin(), dist.end());
    }
};
```

<br>
https://leetcode.com/problems/number-of-islands/solutions/56338/Java-DFS-and-BFS-solution/
<br>
BFS
```
public int numIslands(char[][] grid) {
    int count=0;
    for(int i=0;i<grid.length;i++)
        for(int j=0;j<grid[0].length;j++){
            if(grid[i][j]=='1'){
                bfsFill(grid,i,j);
                count++;
            }
        }
    return count;
}
private void bfsFill(char[][] grid,int x, int y){
    grid[x][y]='0';
    int n = grid.length;
    int m = grid[0].length;
    LinkedList<Integer> queue = new LinkedList<Integer>();  
    int code = x*m+y;  
    queue.offer(code);  
    while(!queue.isEmpty())  
    {  
        code = queue.poll();  
        int i = code/m;  
        int j = code%m;  
        if(i>0 && grid[i-1][j]=='1')    //search upward and mark adjacent '1's as '0'.
        {  
            queue.offer((i-1)*m+j);  
            grid[i-1][j]='0';  
        }  
        if(i<n-1 && grid[i+1][j]=='1')  //down
        {  
            queue.offer((i+1)*m+j);  
            grid[i+1][j]='0';  
        }  
        if(j>0 && grid[i][j-1]=='1')  //left
        {  
            queue.offer(i*m+j-1);  
            grid[i][j-1]='0';  
        }  
        if(j<m-1 && grid[i][j+1]=='1')  //right
        {  
            queue.offer(i*m+j+1);  
            grid[i][j+1]='0';  
        }
    } 
}
```
dfs
```
          void dfs(int x,int y,vector<vector<char>> &grid, vector<vector<int>> &vis) {
        vis[x][y] = 1;
        vector<int> Row = {0,1,0,-1};
        vector<int> Col = {1,0,-1,0};
        for(int i=0;i<4;i++) {
            if(isValid(x+Row[i],y+Col[i]) && !vis[x+Row[i]][y+Col[i]] && grid[x+Row[i]][y+Col[i]] == '1' ) {
                dfs(x+Row[i],y+Col[i],grid,vis);
            }
        }
    }
    int numIslands(vector<vector<char>>& grid) {
        n = grid.size();
        m = grid[0].size();
        vector<vector<int>> vis(n,vector<int> (m,0));
        int ans = 0;
        for(int i=0;i<n;i++) {
            for(int j=0;j<m;j++) {
                if ( !vis[i][j] && grid[i][j] == '1' ) {
                    dfs(i, j, grid, vis);
                    ans++;
                }
            }
        }
        return ans;
    }
```
