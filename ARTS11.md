# 第10周

## Algorithm

### LeetCode 200. 岛屿数量

给定一个由 '1'（陆地）和 '0'（水）组成的的二维网格，计算岛屿的数量。一个岛被水包围，并且它是通过水平方向或垂直方向上相邻的陆地连接而成的。你可以假设网格的四个边均被水包围。

示例 1：

```
输入:
11110
11010
11000
00000

输出: 1
```

示例 2：

```
输入:
11000
11000
00100
00011

输出: 3
```


#### Solution 1: DFS	

耗时: 28ms
内存: 11MB

```cpp
class Solution {
public:
    void dfs(vector<vector<char>>& grid, int x, int y) {
		if (x < 0 || x >= grid.size()) return;
		if (y < 0 || y >= grid[0].size()) return;
		if (grid[x][y] == '0') return;
		grid[x][y] = '0';
		dfs(grid, x + 1, y);
		dfs(grid, x - 1, y);
		dfs(grid, x, y + 1);
		dfs(grid, x, y - 1);
	}
    
	int numIslands(vector<vector<char>>& grid) {
		if (grid.empty() || grid[0].empty()) return 0;
		int N = grid.size(), M = grid[0].size();
		int cnt = 0;
		for (int i = 0; i < N; i++) {
			for (int j = 0; j < M; j++) {
				if (grid[i][j] == '1') {
					dfs(grid, i, j);
					cnt++;
				}
			}
		}
		return cnt;
	}
};
```

#### Solution 2: Union find	

耗时: 20ms
内存: 10.9MB

```cpp
class Solution {
public:
    int findFather(vector<int> &father,int a){
        int f = a;
        while(father[f] != f){
            f = father[f];
        }
        while(father[a] != a){
            int z = a;
            a = father[z];
            father[a] = f;
 
        }
        return f;
    }
    void unionFather(vector<int> &father, int a,int b){
        int fa = findFather(father,a);
        int fb = findFather(father,b);
        if(fa != fb){
            father[fa] = fb;
        }
    }
 
    int numIslands(vector<vector<char>>& grid) {
        if(grid.size() == 0|| grid[0].size() == 0) return 0;
        int n = grid.size(), m = grid[0].size(), k = n*m;
        vector<int> father(k,-1);
        for(int i=0; i<k; i++){
            father[i] = i;
        }
        for(int i=0; i<n; i++){
            for(int j=0; j<m; j++){
                int t1 = i*m+j;
                int t2 = t1+1, t3 = t1+m;
                if(j+1<m && grid[i][j] == grid[i][j+1]) unionFather(father, t1, t2);
                if(i+1<n && grid[i][j] == grid[i+1][j]) unionFather(father, t1, t3);
            }
        }
        int res = 0;
        for(int i=0;i<k;i++){
            if(father[i] == i && grid[i/m][i%m] == '1'){
                res+=1;
            }
        }
        return res;
    }
};
```


## Review

[Extracting view controller actions in Swift](https://www.swiftbysundell.com/posts/extracting-view-controller-actions-in-swift)
作者介绍了Swift中分离controller的actions，明确controller责任的一些原则。

## Tip

`Storyboard`中选中`ViewController`点击 `Editor` 选择`Refactor to Storyboard`可以将固有界面进行分割，多人开发中避免冲突，也能减少`Storyboard`加载速度。

## Share

本周分享 [从 Auto Layout 的布局算法谈性能](https://draveness.me/layout-performance) 灯塔大神详实的介绍Auto Layout的布局算法及其性能影响。


