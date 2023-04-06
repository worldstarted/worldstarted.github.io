# 二叉树

## 基础

1. [二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)

   > 给定一个二叉树，找出其最大深度。
   >
   > 二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。
   >
   > **说明:** 叶子节点是指没有子节点的节点。
   >
   > `思路`
   >
   > 深度是从上往下，所以用前序遍历。但指针在进入到当前节点后，应该更新深度最大值，因为，之后，指针就会离开当前节点，深度会减一。

2. [二叉树的直径](https://leetcode.cn/problems/diameter-of-binary-tree/)

   > 给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过也可能不穿过根结点。
   >
   > `思路`
   >
   > **每一条二叉树的「直径」长度，就是一个节点的左右子树的最大深度之和**
   >
   > ```java
   > private int ans = 0;
   >     
   > public int diameterOfBinaryTree(TreeNode root) {
   >     depth(root);
   >     return ans;
   > }
   > 
   > public int depth(TreeNode root){
   >     if(root==null)
   >         return 0;
   >     int leftDep = depth(root.left);
   >     int rightDep = depth(root.right);
   >     ans = Math.max(leftDep+rightDep,ans);
   >     return Math.max(leftDep,rightDep)+1;
   > }
   > ```

3. [翻转二叉树](https://leetcode.cn/problems/invert-binary-tree/)

   > 给你一棵二叉树的根节点 `root` ，翻转这棵二叉树，并返回其根节点。
   >
   > `思路`
   >
   > 递归遍历，交换左右子树。

4. [填充每个节点的下一个右侧节点指针](https://leetcode.cn/problems/populating-next-right-pointers-in-each-node/)

   > 给定一个 **完美二叉树** ，其所有叶子节点都在同一层，每个父节点都有两个子节点。二叉树定义如下：
   >
   > ```c++
   > struct Node {
   >     int val;
   >     Node *left;
   >     Node *right;
   >     Node *next;
   > }
   > ```
   >
   >
   > 填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。
   >
   > 初始状态下，所有 next 指针都被设置为 NULL。
   >
   > `思路`
   >
   > <img src="https://labuladong.github.io/algo/images/%e4%ba%8c%e5%8f%89%e6%a0%91%e7%b3%bb%e5%88%97/3.png" alt="img" style="zoom:50%;" />
   >
   > 将二叉树抽象成三叉树。
   >
   > ```java
   > public Node connect(Node root) {
   >     if(root!=null)
   >         traverse(root.left, root.right);
   >     return root;
   > }
   > 
   > public void traverse(Node n1, Node n2){
   >     if(n1==null || n2==null)
   >         return ;
   >     n1.next = n2;
   >     traverse(n1.left, n1.right);
   >     traverse(n2.left, n2.right);
   >     traverse(n1.right, n2.left);
   > }
   > ```

5. [二叉树展开为链表](https://leetcode.cn/problems/flatten-binary-tree-to-linked-list/)

   > 给你二叉树的根结点 root ，请你将它展开为一个单链表：
   >
   > 展开后的单链表应该同样使用 TreeNode ，其中 right 子指针指向链表中下一个结点，而左子指针始终为 null 。展开后的单链表应该与二叉树 先序遍历 顺序相同。
   >
   > `思路`
   >
   > 函数是void，代表希望我们原地操作。可以尝试递归分解问题。
   >
   > 不妨假设已经把左子树全部展平，右子树全部展平，下面就是连接左右子树。
   >
   > ```java
   > public void flatten(TreeNode root) {
   >     if(root==null)
   >         return ;
   >     flatten(root.left);
   >     flatten(root.right);
   > 
   >     TreeNode left = root.left;
   >     TreeNode right = root.right;
   >     root.left = null;
   >     root.right = left;
   >     TreeNode p = root;
   >     while(p.right!=null){
   >         p = p.right;
   >     }
   >     p.right = right;
   > }
   > ```

6. [最大二叉树](https://leetcode.cn/problems/maximum-binary-tree/)

   > 给定一个不重复的整数数组 nums 。 最大二叉树 可以用下面的算法从 nums 递归地构建:
   >
   > 创建一个根节点，其值为 nums 中的最大值。
   > 递归地在最大值 左边 的 子数组前缀上 构建左子树。
   > 递归地在最大值 右边 的 子数组后缀上 构建右子树。
   > 返回 nums 构建的 最大二叉树 
   >
   > `思路`
   >
   > 按照题目模拟过程即可。

7. [从前序与中序遍历序列构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

   > 给定两个整数数组 preorder 和 inorder ，其中 preorder 是二叉树的先序遍历， inorder 是同一棵树的中序遍历，请构造二叉树并返回其根节点。
   >
   > `思路`
   >
   > 模拟即可。

8. [从中序与后序遍历序列构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

   > 给定两个整数数组 inorder 和 postorder ，其中 inorder 是二叉树的中序遍历， postorder 是同一棵树的后序遍历，请你构造并返回这颗 二叉树 。
   >
   > `思路`
   >
   > <img src="C:\Users\ldx\AppData\Roaming\Typora\typora-user-images\image-20230322152958742.png" alt="image-20230322152958742" style="zoom:50%;" />

9. [根据前序和后序遍历构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-preorder-and-postorder-traversal/)

   > 给定两个整数数组，preorder 和 postorder ，其中 preorder 是一个具有 无重复 值的二叉树的前序遍历，postorder 是同一棵树的后序遍历，重构并返回二叉树。
   >
   > 如果存在多个答案，您可以返回其中 任何 一个。
   >
   > `思路`
   >
   > 同上
   >
   > ```java
   > private HashMap<Integer,Integer> pos = new HashMap<>();
   > public TreeNode constructFromPrePost(int[] preorder, int[] 										postorder) {
   >     for(int i=0;i<postorder.length;i++){
   >         pos.put(postorder[i], i);
   >     }
   >     return build(preorder, 0, preorder.length-1,postorder, 				0, postorder.length-1);
   > }
   > 
   > public TreeNode build(int[] preorder, int preL, int preR, 				int[] postorder, int postL, int postR){
   >     if(preL>preR)
   >         return null;
   >     if(preL==preR)
   >         return new TreeNode(preorder[preL]);
   >     TreeNode root = new TreeNode(preorder[preL]);
   >     int idx = pos.get(preorder[preL+1]);
   >     int leftLen  = idx-postL+1;
   >     root.left = build(preorder, preL + 1, preL+leftLen, 				postorder, postL, idx);
   >     root.right = build(preorder, preL+1+leftLen, preR, 					postorder, idx+1, postR-1);
   > 
   >     return root;
   > }
   > ```

10. [二叉树的序列化与反序列化](https://leetcode.cn/problems/serialize-and-deserialize-binary-tree/description/)

    > 序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。
    >
    > 请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。
    >
    > **提示:** 输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅 [LeetCode 序列化二叉树的格式](vscode-webview://15uar6e8nhvujihibfjdu4fqcfb6dqf8ov5ggrm46qv7hrqq6610/faq/#binary-tree)。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。
    >
    > `思路`
    >
    > 序列化：前序遍历分解
    >
    > 反序列化：前序遍历构造，如果使用静态成员变量的话，别忘了重置为0。

11. [寻找重复的子树](https://leetcode.cn/problems/find-duplicate-subtrees/description/)

    > 给你一棵二叉树的根节点 `root` ，返回所有 **重复的子树** 。
    >
    > 对于同一类的重复子树，你只需要返回其中任意 **一棵** 的根结点即可。
    >
    > 如果两棵树具有 **相同的结构** 和 **相同的结点值** ，则认为二者是 **重复** 的。
    >
    > `思路`
    >
    > - 方法一：先知道以自己为根的子树是什么样，再去逐一遍历。
    >
    >   - 序列化
    >
    >   - 遍历找重复
    >
    >     ```java
    >     private HashMap<String,Integer> cnt;
    >     private List<TreeNode> ans;
    >     public List<TreeNode> findDuplicateSubtrees(TreeNode 											root) {
    >         cnt = new HashMap<>();
    >         ans = new ArrayList<>();
    >         serialize(root);
    >         return ans;
    >     }
    >                                                         
    >     public String serialize(TreeNode root){
    >         if(root==null){
    >             return "#";
    >         }
    >         String s = root.val+","+serialize(root.left)+","+serialize(root.right);
    >         if(cnt.getOrDefault(s,0)==1){
    >             ans.add(root);
    >         }
    >         cnt.put(s, cnt.getOrDefault(s, 0) + 1) ;
    >         return s;
    >     } 
    >     ```
    >
    >     
    >
    > - 方法二：基于方法一的优化，使用三元组$(root,left,right)$来唯一确定一棵树，root是根节点值，left与right代表两棵子树的序号——每发现一棵新树，就给予一个编号。
    >
    >   ```java
    >   private HashMap<String, Pair<TreeNode, Integer>> vis;
    >   private HashSet<TreeNode> ans;
    >   private int idx;
    >   public List<TreeNode> findDuplicateSubtrees(TreeNode 											root) {
    >       vis = new HashMap<>();
    >       ans = new HashSet<>();
    >       idx = 0;
    >       dfs(root);
    >       return new ArrayList<TreeNode>(ans);
    >   }
    >                             
    >   public int dfs(TreeNode root){
    >       if(root==null)
    >           return 0;
    >       int []three = new int[]  	  	
    >       {root.val,dfs(root.left),dfs(root.right)};       
    >       String hash = Arrays.toString(three);
    >       if(vis.containsKey(hash)){
    >           Pair<TreeNode,Integer> p = vis.get(hash);
    >           ans.add(p.getKey());
    >           return p.getValue();
    >       }else{
    >           vis.put(hash,new Pair<TreeNode,Integer>(root, 												++idx));
    >           return idx;
    >       }
    >   }
    >   ```
    >
    >   

## 归并排序

> ==算法模板==
>
> ```java
> private int[] tep;
> public int[] getAns(int[] nums){
>     int len = nums.length;
>     tep = new int[len];
>     sort(nums, 0, len-1);
>     return nums;
> }
> 
> public void sort(int[] nums, int low, int high){
>     if(low==high){
>         return ;
>     }
>     int mid = low + (high-low)/2;
>     sort(nums, low, mid);
>     sort(nums, mid+1, high);
>     merge(nums, low, mid, high);
> }
> 
> public void merge(int[] nums, int low, int mid, int high){
>     for(int i=low;i<=high;i++){
>         tep[i] = nums[i];
>     }
>     int i=low, j=mid+1;
>     for(int k=low;k<=high;k++){
>         if(i==mid+1){
>             nums[k] = tep[j++]; 
>         }else if(j==high+1){
>             nums[k]  = tep[i++];
>         }else if(tep[i]>tep[j]){
>             nums[k] = tep[j++];
>         }else {
>             nums[k] = tep[i++];
>         }
>     }
> }
> ```

1. [计算右侧小于当前元素的个数](https://leetcode.cn/problems/count-of-smaller-numbers-after-self/description/)

   > 给你一个整数数组 `nums` ，按要求返回一个新数组 `counts` 。数组 `counts` 有该性质： `counts[i]` 的值是 `nums[i]` 右侧小于 `nums[i]` 的元素的数量。
   >
   > `思路`
   >
   > - 归并排序
   >
   >   在归并排序的过程中，存在这么一个阶段，在合并的过程中，<img src="C:\Users\ldx\AppData\Roaming\Typora\typora-user-images\image-20230330205807349.png" alt="image-20230330205807349" style="zoom:50%;" />
   >
   >   temp[i]<temp[j]，由于两边都是有序的，所以比i对应的元素小的个数是 j-mid-1
   >
   > - 线段树
   >
   >   

2. [翻转对](https://leetcode.cn/problems/reverse-pairs/description/)

   > 给定一个数组 `nums` ，如果 `i < j` 且 `nums[i] > 2*nums[j]` 我们就将 `(i, j)` 称作一个***重要翻转对\***。
   >
   > 你需要返回给定数组中的重要翻转对的数量。
   >
   > `思路`
   >
   > 由于nums[i]>nums[j]*2，所以nums[i]>nums[j]，可以采用归并排序，这样子两边都是有序的，例如递增，这样，只用比较不同组之间的元素，在merge上下功夫。
   >
   > ```java
   > public void merge(int[] nums, int low, int mid, int high){
   >     for(int i=low;i<=high;i++){
   >         tep[i] = nums[i];
   >     }
   >     int j = mid + 1;//关键
   >     for(int i=low;i<=mid;i++){
   >         while(j<=high && (long)nums[i]>(long)nums[j]*2)
   >             j++;
   >         ans += j-mid-1;
   >     }
   >     int i=low;
   >     j = mid+1;
   >     for(int k=low;k<=high;k++){
   >         if(i==mid+1){
   >             nums[k] = tep[j++];
   >         }else if(j==high+1){
   >             nums[k] = tep[i++];
   >         }else if(tep[i]>tep[j]){
   >             nums[k] = tep[j++];
   >         }else{
   >             nums[k] = tep[i++];
   >         }
   >     }
   > }
   > ```
   >

3. [区间和的个数](https://leetcode.cn/problems/count-of-range-sum/description/)

   > 给你一个整数数组 `nums` 以及两个整数 `lower` 和 `upper` 。求数组中，值位于范围 `[lower, upper]` （包含 `lower` 和 `upper`）之内的 **区间和的个数** 。
   >
   > **区间和** `S(i, j)` 表示在 `nums` 中，位置从 `i` 到 `j` 的元素之和，包含 `i` 和 `j` (`i` ≤ `j`)。
   >
   > `思路`
   >
   > 题目条件可以转化为count of {i,j}   lower<=  sum of {i,j} <= upper
   >
   > 由于sum是区间和，不是一个数，所以我们要把它转化为方便求的一个数。
   >
   > 因此，使用前缀和。
   >
   > 前缀和，下标最好从1开始，因为求区间[L,R]的和的公式为$pre[R] - pre[L-1], L>=1$
   >
   > ```java
   > private int ans; 
   > private long[] tep;//用来交换数据的数组
   > private int lb;
   > private int rb;
   > public int countRangeSum(int[] nums, int lower, int upper) {
   >     int len = nums.length;
   >     this.tep = new long[len+1];//前缀和下标从1开始，所以长度+1
   >     ans=0;
   >     long []pre = new long[len+1];
   >     pre[0] = 0;
   >     for(int i=0;i<len;i++){
   >         pre[i+1] = pre[i]+nums[i];
   >     }
   >     this.lb = lower;
   >     this.rb = upper;
   >     sort(pre, 0, len);
   >     
   >     return ans;
   > }
   > 
   > public void sort(long[] pre, int left, int right){
   >     if(left==right)
   >         return ;
   >     int mid = left + (right-left)/2;
   >     sort(pre,left, mid);
   >     sort(pre, mid+1, right);
   >     merge(pre, left, mid, right);
   > }
   > 
   > public void merge(long[] pre, int left, int mid, int right){
   >     for(int i=left;i<=right;i++){
   >         tep[i]=pre[i];
   >     }
   >     int start=mid+1,end=mid+1;
   >     //两个部分都是有序的，递增，
   >     for(int i=left;i<=mid;i++){
   >         while(start<=right && pre[start]-pre[i]<lb)
   >             start++;
   >         //直到end的值超过区间和边界，这样子就可以计算
   >         while(end<=right && pre[end]-pre[i]<=rb)
   >             end++;
   >         ans += end-start;
   >     }
   >     int i = left;
   >     int j = mid+1;
   >     for(int k = left;k<=right;k++){
   >         if(i==mid+1){
   >             pre[k] = tep[j++];
   >         }else if(j==right+1){
   >             pre[k] = tep[i++];
   >         }else if(tep[i]>tep[j]){
   >             pre[k] = tep[j++];
   >         }else{
   >             pre[k] = tep[i++];
   >         }
   >     }
   > }
   > ```

## 快速排序

1. [数组中的第K个最大元素](https://leetcode.cn/problems/kth-largest-element-in-an-array/description/)

   > 给定整数数组 `nums` 和整数 `k`，请返回数组中第 `k` 个最大的元素。
   >
   > 请注意，你需要找的是数组排序后的第 `k` 个最大的元素，而不是第 `k` 个不同的元素。
   >
   > 你必须设计并实现时间复杂度为 `O(n)` 的算法解决此问题。
   >
   > `思路`
   >
   > - 快排，然后找nums[len-k]
   > - 快速选择排序，每一次通过partition得到的p，满足左边都比它小，右边都比它大，所以，看p与len-k的关系。相当于二分。

## 二叉搜索树

### 累加树

1. [把二叉搜索树转换为累加树](https://leetcode.cn/problems/convert-bst-to-greater-tree/description/)

   > 给出二叉 **搜索** 树的根节点，该树的节点值各不相同，请你将其转换为累加树（Greater Sum Tree），使每个节点 `node` 的新值等于原树中大于或等于 `node.val` 的值之和。
   >
   > 提醒一下，二叉搜索树满足下列约束条件：
   >
   > - 节点的左子树仅包含键 **小于** 节点键的节点。
   > - 节点的右子树仅包含键 **大于** 节点键的节点。
   > - 左右子树也必须是二叉搜索树。
   >
   > `思路`
   >
   > 累加树的根节点值 是 大于等于当前节点val的节点的val和,，所以应该用降序，可以用sum维护这个值。

### 基本操作

1. [验证二叉搜索树](https://leetcode.cn/problems/validate-binary-search-tree/description/)

   > 给你一个二叉树的根节点 `root` ，判断其是否是一个有效的二叉搜索树。
   >
   > **有效** 二叉搜索树定义如下：
   >
   > - 节点的左子树只包含 **小于** 当前节点的数。
   > - 节点的右子树只包含 **大于** 当前节点的数。
   > - 所有左子树和右子树自身必须也是二叉搜索树。
   >
   > `思路`
   >
   > ```java
   > public boolean isValidBST(TreeNode root) {
   >     return isValidBST(root, null, null);
   > }
   > 
   > //以 root 为根的子树节点必须满足 max.val > root.val > min.val
   > private boolean isValidBST(TreeNode root, TreeNode max, TreeNode min){
   >     if(root==null)
   >         return true;
   >     //不存在比最小值更小的
   >     if(min!=null && root.val <= min.val)
   >         return false;
   >     //不存在比最大值更大的
   >     if(max != null && root.val >= max.val)
   >         return false;
   >     return isValidBST(root.left, root, min) && isValidBST(root.right, max, root);
   > }
   > ```

2. 删除某个节点值

   ```java
   TreeNode deleteNode(TreeNode root, int key) {
       if (root == null) return null;
       if (root.val == key) {
           // 这两个 if 把情况 1 和 2 都正确处理了
           if (root.left == null) return root.right;
           if (root.right == null) return root.left;
           // 处理情况 3
           // 获得右子树最小的节点
           TreeNode minNode = getMin(root.right);
           // 删除右子树最小的节点
           root.right = deleteNode(root.right, minNode.val);
           // 用右子树最小的节点替换 root 节点
           minNode.left = root.left;
           minNode.right = root.right;
           root = minNode;
       } else if (root.val > key) {
           root.left = deleteNode(root.left, key);
       } else if (root.val < key) {
           root.right = deleteNode(root.right, key);
       }
       return root;
   }
   
   TreeNode getMin(TreeNode node) {
       // BST 最左边的就是最小的
       while (node.left != null) node = node.left;
       return node;
   }
   
   ```

3. 插入某个值

   ```java
   TreeNode insertIntoBST(TreeNode root, int val) {
       // 找到空位置插入新节点
       if (root == null) return new TreeNode(val);
       // if (root.val == val)
       //     BST 中一般不会插入已存在元素
       if (root.val < val) 
           root.right = insertIntoBST(root.right, val);
       if (root.val > val) 
           root.left = insertIntoBST(root.left, val);
       return root;
   }
   ```
   
   个数
   
   - 普通二叉树
   
     ```java
     public int countNodes(TreeNode root) {
         if (root == null) return 0;
         return 1 + countNodes(root.left) + countNodes(root.right);
     }
     ```
   
   - 满二叉树
   
     ```java
     public int countNodes(TreeNode root) {
         int h = 0;
         // 计算树的高度
         while (root != null) {
             root = root.left;
             h++;
         }
         // 节点总数就是 2^h - 1
         return (int)Math.pow(2, h) - 1;
     }
     ```
   
   - 完全二叉树
   
     ```java
     public int countNodes(TreeNode root) {
         TreeNode l = root, r = root;
         // 沿最左侧和最右侧分别计算高度
         int hl = 0, hr = 0;
         while (l != null) {
             l = l.left;
             hl++;
         }
         while (r != null) {
             r = r.right;
             hr++;
         }
         // 如果左右侧计算的高度相同，则是一棵满二叉树
         if (hl == hr) {
             return (int)Math.pow(2, hl) - 1;
         }
         // 如果左右侧的高度不同，则按照普通二叉树的逻辑计算
         return 1 + countNodes(root.left) + countNodes(root.right);
     }
     
     ```
   
     

### 构造



