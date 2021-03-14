# 二叉树的广度优先搜索BFS

## 解题思路：

题目要求的二叉树的 从上至下打印（即按层打印），又称为二叉树的 广度优先搜索（BFS）。
BFS 通常借助 队列 的先入先出特性来实现。

![Picture0.png](https://pic.leetcode-cn.com/f824fdd8052ae4ee657365c98633480caf03c60e42e4661797618e318baf8664-Picture0.png)

## 算法流程：

特例处理： 当树的根节点为空，则直接返回空列表 [] ；
初始化： 打印结果列表 res = [] ，包含根节点的队列 queue = [root] ；
BFS 循环： 当队列 queue 为空时跳出；
出队： 队首元素出队，记为 node；
打印： 将 node.val 添加至列表 tmp 尾部；
添加子节点： 若 node 的左（右）子节点不为空，则将左（右）子节点加入队列 queue ；
返回值： 返回打印结果列表 res 即可。



## 复杂度分析：

时间复杂度 $$O(N)$$ ： N为二叉树的节点数量，即 BFS 需循环 N 次。
空间复杂度 $$O(N)$$ ： 最差情况下，即当树为平衡二叉树时，最多有 N/2个树节点同时在 queue 中，使用 $$O(N)$$大小的额外空间。

```java
//Java
class Solution {
    public int[] levelOrder(TreeNode root) {
        if(root == null) return new int[0];
        Queue<TreeNode> queue = new LinkedList<>(){{ add(root); }};
        ArrayList<Integer> ans = new ArrayList<>();
        while(!queue.isEmpty()) {
            TreeNode node = queue.poll();
            ans.add(node.val);
            if(node.left != null) queue.add(node.left);
            if(node.right != null) queue.add(node.right);
        }
        int[] res = new int[ans.size()];
        for(int i = 0; i < ans.size(); i++)
            res[i] = ans.get(i);
        return res;
    }
}
```

```python
#Python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[int]:
        if not root: return []
        res, queue = [], collections.deque()
        queue.append(root)
        while queue:
            node = queue.popleft()
            res.append(node.val)
            if node.left: queue.append(node.left)
            if node.right: queue.append(node.right)
        return res
```

