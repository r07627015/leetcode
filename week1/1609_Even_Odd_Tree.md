
## Python
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isEvenOddTree(self, root: Optional[TreeNode]) -> bool:
        queue = deque([root])
        level = 0

        while queue:
            size = len(queue)

            # 初始化這一層的前一個值
            prev = -inf if level % 2 == 0 else inf

            for _ in range(size):
                node = queue.popleft()
                v = node.val

                if level % 2 == 0:
                    # 偶數層：奇數 + 嚴格遞增
                    if v % 2 == 0 or v <= prev:
                        return False
                else:
                    # 奇數層：偶數 + 嚴格遞減
                    if v % 2 == 1 or v >= prev:
                        return False

                prev = v

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            level += 1

        return True
```

- Time Complexity: `O(n)`
- Space Complexity: `O(w)`，其中 w 是樹某一層的最大節點數，也就是樹的最大寬度，worst case 為 `O(n)`
