#### [113. 路径总和 II](https://leetcode-cn.com/problems/path-sum-ii/)

# 题目描述
```
给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

说明: 叶子节点是指没有子节点的节点。

示例:
给定如下二叉树，以及目标和 sum = 22，

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
返回:

[
   [5,4,11,2],
   [5,8,4,5]
]
```

# 代码

```python
//dfs
//执行耗时:2 ms,击败了49.57% 的Java用户
//内存消耗:39.2 MB,击败了56.20% 的Java用户
class Solution {
    List<List<Integer>> res = new LinkedList<>();
    Deque<Integer> path = new LinkedList<>();
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        dfs(root,sum);
        return res;
    }

    public void dfs(TreeNode root, int sum) {
        if(root == null){
            return;
        }
        path.offerLast(root.val);
        sum -= root.val;
        if(root.left == null && root.right == null && sum == 0){
            res.add(new LinkedList<Integer>(path));
        }
        dfs(root.left, sum);
        dfs(root.right, sum);
        path.pollLast();
    }
}
//Python3
//执行耗时:52 ms,击败了80.02% 的Python3用户
//内存消耗:14.9 MB,击败了66.33% 的Python3用户
class Solution:
    def pathSum(self, root: TreeNode, total: int) -> List[List[int]]:
        res = list();
        path = list();

        def dfs(root: TreeNode, total: int):
            if not root:
                return
            path.append(root.val)
            total -= root.val
            if not root.left and not root.right and total == 0:
                res.append(path[:])
            dfs(root.left, total)
            dfs(root.right, total)
            path.pop()

        dfs(root, total)
        return res
```