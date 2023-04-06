# 难一点的算法

## **Zobrist Hash**

### 模板

> ==Zobrist Hash==
>
> 一种快速计算棋盘状态的哈希算法。
>
> 比如，有个2*2的五子棋盘。
>
> ```java
> b*
> **
> // b代表黑棋，*代表空，w代表白棋  
> ```
>
> 先生成一个同样大小（2*2）的随机数组
>
> ```java
> 0x0123 0x0589
> 0x0875 0x0438
> ```
>
> 然后，可以计算棋盘上每个位置的哈希值，用棋盘上的位置的值与随机数组相应的哈希值做异或，即为该位置的状态，将所有非空位置的状态异或，就是整个棋盘的状态。

### 题目

1. [**D - Three Days Ago**](https://atcoder.jp/contests/abc295/tasks/abc295_d) 

   > 
   >
   > `本题思路`
   >
   > 逆向思维，既然满足happy，那么重排后，一定可以出现两次。
   >
   > 所以，用一个异或前缀和来记录 字符串的状态，每次遇到新的字符，就更新状态。
   > 
   > ```c++
   > void sol(){
   >  string s;
   > cin >> s;
   >  vector<ll> cnt(1<<10);
   > ll ans=0;
   >  ll pf = 0;
   >  cnt[0]++;
   >  for(char c:s){
   >      pf ^= (1<<(c-'0'));//更新棋盘状态
   >     ans += cnt[pf];//更新结果
   >      cnt[pf]++;//更新棋盘新状态的次数
   > }
   >  cout<<ans<<endl;
   >}
   > ```
   >
   

## **线段树**

### 模板

> 频繁查询区间信息。
>
> ```java
> class SegmentTree {
>     int[] tree; // 线段树数组，存储区间和或最大/最小值等
>     int[] nums; // 原始数组，存储待查询区间的元素值
> 
>     /**
>      * 线段树构造函数，初始化线段树数组并建立线段树
>      * 
>      * @param nums 原始数组，存储待查询区间的元素值
>      */
>     public SegmentTree(int[] nums) {
>         this.nums = nums;
>         // 线段树最多需要 4n 个节点，其中 n 是原始数组的长度
>         tree = new int[4 * nums.length];
>         // 建立线段树
>         buildTree(0, 0, nums.length - 1);
>     }
> 
>     /**
>      * 建立线段树
>      * 
>      * @param treeIndex 当前节点在线段树数组中的下标
>      * @param left      当前节点表示的区间的左端点
>      * @param right     当前节点表示的区间的右端点
>      */
>     private void buildTree(int treeIndex, int left, int right) {
>         if (left == right) {
>             // 叶节点，存储原始数组中的元素值
>             tree[treeIndex] = nums[left];
>         } else {
>             int mid = left + (right - left) / 2;
>             int leftIndex = 2 * treeIndex + 1;
>             int rightIndex = 2 * treeIndex + 2;
>             // 递归建立左子树和右子树
>             buildTree(leftIndex, left, mid);
>             buildTree(rightIndex, mid + 1, right);
>             // 根据左右子树的值计算当前节点的值（这里以区间和为例）
>             tree[treeIndex] = tree[leftIndex] + tree[rightIndex];
>         }
>     }
> 
>     /**
>      * 查询区间和
>      * 
>      * @param left  待查询区间的左端点
>      * @param right 待查询区间的右端点
>      * @return 待查询区间的和
>      */
>     public int query(int left, int right) {
>         return query(0, 0, nums.length - 1, left, right);
>     }
> 
>     /**
>      * 在以 treeIndex 为根节点的线段树中查询区间和
>      * 
>      * @param treeIndex  当前节点在线段树数组中的下标
>      * @param left       当前节点表示的区间的左端点
>      * @param right      当前节点表示的区间的右端点
>      * @param queryLeft  待查询区间的左端点
>      * @param queryRight 待查询区间的右端点
>      * @return 待查询区间的和
>      */
>     private int query(int treeIndex, int left, int right, int queryLeft, int queryRight) {
>         if (left > queryRight || right < queryLeft) {
>             // 当前节点表示的区间与待查询区间不重叠，返回 0
>             return 0;
>         } else if (left >= queryLeft && right <= queryRight) {
>             // 当前节点表示的区间被完全包含在待查询区间内，直接返回当前节点的值
>             return tree[treeIndex];
>         } else {
>             int mid = left + (right - left) / 2;
>             int leftIndex = 2 * treeIndex + 1;
>             int rightIndex = 2 * treeIndex + 2;
>             // 分别查询左子树和右子树
>             int leftSum = query(leftIndex, left, mid, queryLeft, queryRight);
>             int rightSum = query(rightIndex, mid + 1, right, queryLeft, queryRight);
>             // 合并左右子树的结果并返回
>             return leftSum + rightSum;
>         }
>     }
> 
>     /**
>      * 更新指定下标的元素值
>      * 
>      * @param index 指定下标
>      * @param val   新的元素值
>      */
>     public void update(int index, int val) {
>         update(0, 0, nums.length - 1, index, val);
>     }
> 
>     /**
>      * 在以 treeIndex 为根节点的线段树中更新指定下标的元素值
>      * 
>      * @param treeIndex 当前节点在线段树数组中的下标
>      * @param left      当前节点表示的区间的左端点
>      * @param right     当前节点表示的区间的右端点
>      * @param index     待更新元素的下标
>      * @param val       新的元素值
>      */
>     private void update(int treeIndex, int left, int right, int index, int val) {
>         if (left == right) {
>             // 找到待更新元素所在的叶节点，更新该节点的值
>             tree[treeIndex] = val;
>         } else {
>             int mid = left + (right - left) / 2;
>             int leftIndex = 2 * treeIndex + 1;
>             int rightIndex = 2 * treeIndex + 2;
>             if (index <= mid) {
>                 // 待更新元素在左子树中，递归更新左子树
>                 update(leftIndex, left, mid, index, val);
>             } else {
>                 // 待更新元素在右子树中，递归更新右子树
>                 update(rightIndex, mid + 1, right, index, val);
>             }
>             // 根据左右子树的值计算当前节点的值
>             tree[treeIndex] = tree[leftIndex] + tree[rightIndex];
>         }
>     }
> }
> ```
>
> 

### 题目

## **字典树（前缀树）**

### 模板

```java
public class Trie {
    private final int N = 100009;
    private int[][] trie; // 存储 Trie 树的二维数组
    private int[] cnt; // 存储每个 Trie 树节点的出现次数
    private int idx; // 记录 Trie 树中节点的个数

    public Trie(){
        trie = new int[N][26]; // 初始化 Trie 树
        cnt = new int[N]; // 初始化出现次数数组
        idx = 0; // 节点个数初始为 0
    }

    // 向 Trie 树中插入字符串 s
    public void insert(String s){
        int p = 0; // 从根节点开始
        for(int i=0;i<s.length();i++){
            int u = s.charAt(i)-'a'; // 计算字符 s[i] 在数组中的下标
            if(trie[p][u] == 0) // 如果当前节点的 u 子节点不存在
                trie[p][u] = ++idx; // 创建一个新的节点，并记录节点个数
            p = trie[p][u]; // 移动到下一个节点
        }
        cnt[p]++; // 将最后一个节点的出现次数加 1
    }

    // 在 Trie 树中查找字符串 s
    public boolean search(String s){
        int p=0; // 从根节点开始
        for(int i=0;i<s.length();i++){
            int u = s.charAt(i)-'a'; // 计算字符 s[i] 在数组中的下标
            if(trie[p][u]==0) // 如果当前节点的 u 子节点不存在，说明字符串 s 在 Trie 树中不存在
                return false;
            p = trie[p][u]; // 移动到下一个节点
        }
        return cnt[p]!=0; // 如果最后一个节点的出现次数不为 0，则说明字符串 s 在 Trie 树中存在
    }

    // 判断 Trie 树中是否存在以字符串 s 为前缀的字符串
    public boolean startsWith(String s){
        int p = 0; // 从根节点开始
        for(int i=0;i<s.length();i++){
            int u = s.charAt(i)-'a'; // 计算字符 s[i] 在数组中的下标
            if(trie[p][u] == 0) // 如果当前节点的 u 子节点不存在，说明 Trie 树中不存在以字符串 s 为前缀的字符串
                return false;
            p = trie[p][u]; // 移动到下一个节点
        }
        return true; // 如果能够匹配到最后一个字符，则说明 Trie 树中存在以字符串 s 为前缀的字符串
    }
}

```

```java
class Trie {
    class TrieNode{
        boolean end;
        TrieNode[] tns = new TrieNode[26];
    }
    TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    public void insert(String word) {
        TrieNode p = root;
        for(int i=0;i<word.length();i++){
            int u = word.charAt(i)-'a';
            if(p.tns[u]==null){
                p.tns[u] = new TrieNode();
            }
            p = p.tns[u];
        }
        p.end = true;
    }

    public boolean search(String word) {
        TrieNode p = root;
        for(int i=0;i<word.length();i++){
            int u = word.charAt(i)-'a';
            if(p.tns[u]==null){
                return false;
            }
            p = p.tns[u];
        }
        return p.end;
    }

    public boolean startsWith(String prefix) {
        TrieNode p = root;
        for(int i=0;i<prefix.length();i++){
            int u = prefix.charAt(i)-'a';
            if(p.tns[u]==null){
                return false;
            }
            p = p.tns[u];
        }
        return true;
    }
}
```

> 除非某些语言在启动时，采用虚拟机的方式，并且预先分配了足够的内存，否则所有的 new 操作都需要反映到 os 上，而在 linux 分配时需要遍历红黑树，因此即使是总空间一样，一次性的 new 要比多次小空间的 new 更省时间，同时集中性的 new 也比分散性的 new 操作要更快，这也就是为什么我们不无脑使用 TrieNode 的原因
>

### 题目

1. [添加与搜索单词 - 数据结构设计](https://leetcode.cn/problems/design-add-and-search-words-data-structure/description/)

   > 请你设计一个数据结构，支持 添加新单词 和 查找字符串是否与任何先前添加的字符串匹配 。
   >
   > 实现词典类 `WordDictionary` ：
   >
   > - `WordDictionary()` 初始化词典对象
   > - `void addWord(word)` 将 `word` 添加到数据结构中，之后可以对它进行匹配
   > - `bool search(word)` 如果数据结构中存在字符串与 `word` 匹配，则返回 `true` ；否则，返回 `false` 。`word` 中可能包含一些 `'.'` ，每个 `.` 都可以表示任何一个字母。
   >
   > `思路`
   >
   > 问题在于search的word可能有`.`，而`.`可以是任何字母。所以，分为两种情况分别讨论。
   >
   > ```java
   > public boolean search(String word) {
   >     return dfs(word, root, 0);
   > }
   > 
   > private boolean dfs(String word, TrieNode p, int idx){
   >     int len = word.length();
   >     if(len == idx){
   >         return p.end;
   >     }
   >     char c = word.charAt(idx);
   >     if(c=='.'){
   >         for(int i=0;i<26;i++){
   >             if(p.tns[i]!=null && dfs(word,p.tns[i], idx+1))
   >                 return true;
   >         }
   >         return false;
   >     }else{
   >         int u = c-'a';
   >         if(p.tns[u]==null)
   >             return false;
   >         return dfs(word, p.tns[u], idx+1);
   >     }
   > }
   > ```

2. [单词替换](https://leetcode.cn/problems/replace-words/description/)

   > 在英语中，我们有一个叫做 `词根`(root) 的概念，可以词根**后面**添加其他一些词组成另一个较长的单词——我们称这个词为 `继承词`(successor)。例如，词根`an`，跟随着单词 `other`(其他)，可以形成新的单词 `another`(另一个)。
   >
   > 现在，给定一个由许多**词根**组成的词典 `dictionary` 和一个用空格分隔单词形成的句子 `sentence`。你需要将句子中的所有**继承词**用**词根**替换掉。如果**继承词**有许多可以形成它的**词根**，则用**最短**的词根替换它。
   >
   > 你需要输出替换之后的句子。
   >
   > `思路`
   >
   > 先把所有词根加进去，然后逐一判断。
   >
   > ```java
   > private String query(String word){
   >     TrieNode p = root;
   >     for (int i = 0; i < word.length(); i++) {
   >         int u = word.charAt(i) - 'a';
   >         if (p.tns[u] == null) {
   >             break;
   >         }
   >         if(p.tns[u].end){//保证了长度最短。
   >             return word.substring(0, i+1);
   >         }
   >         p = p.tns[u];
   >     }
   >     return word;
   > }
   > ```
   >

3. [键值映射](https://leetcode.cn/problems/map-sum-pairs/description/)

   > 设计一个 map ，满足以下几点:
   >
   > - 字符串表示键，整数表示值
   > - 返回具有前缀等于给定字符串的键的值的总和
   >
   > 实现一个 `MapSum` 类：
   >
   > - `MapSum()` 初始化 `MapSum` 对象
   > - `void insert(String key, int val)` 插入 `key-val` 键值对，字符串表示键 `key` ，整数表示值 `val` 。如果键 `key` 已经存在，那么原来的键值对 `key-value` 将被替代成新的键值对。
   > - `int sum(string prefix)` 返回所有以该前缀 `prefix` 开头的键 `key` 的值的总和。
   >
   > `思路`
   >
   > 把键值对存起来，再遍历所有的以prefix为前缀的结果。
   >
   > ```java
   > class MapSum {
   >     private HashMap<String,Integer> map;
   >     class TrieNode{
   >         boolean end;
   >         TrieNode[] tns = new TrieNode[26];
   >     }
   >     TrieNode root;
   >     public MapSum() {
   >         map = new HashMap<>();
   >         root = new TrieNode();
   >     }
   > 
   >     public void insert(String key, int val) {
   >         if(!map.containsKey(key)){
   >             TrieNode p = root;
   >             for(int i=0;i<key.length();i++){
   >                 int u = key.charAt(i)-'a';
   >                 if(p.tns[u]==null)
   >                     p.tns[u] = new TrieNode();
   >                 p = p.tns[u];
   >             }
   >             p.end = true;
   >         }
   >         map.put(key, val);
   >     }
   > 
   >     public int sum(String prefix) {
   >         TrieNode p = root;
   >         String st = new String(prefix);
   >         for(int i=0;i<prefix.length();i++){
   >             int u = prefix.charAt(i)-'a';
   >             if(p.tns[u]==null)
   >                 return 0;
   >             p = p.tns[u];
   >         }
   >         return dfs(st, p);
   >     }
   > 
   >     private int dfs(String sb, TrieNode son){
   >         int sum = map.getOrDefault(sb,0);
   >         if(son!=null){
   >             for (int i = 0; i < 26; i++) {
   >                 if (son.tns[i] != null) {
   >                     sum += dfs(sb+(char) ('a' + i), son.tns[i]);
   >                 }
   >             }
   >         }
   >         return sum;
   >     }
   > }
   > ```
   >
   > ```java
   > class MapSum {
   >     private static final int N = 2505;
   >     private static int trie[][] = new int[N][26];
   >     private static int cnt[] = new int[N];
   >     private static int idx;
   >     private static HashMap<String, Integer> hash= new HashMap<>();
   >     public MapSum() {
   >         hash.clear();
   >         for(int i=0;i<N;i++)
   >             Arrays.fill(trie[i], 0);
   >         Arrays.fill(cnt, 0);
   >         idx = 0;
   >     }
   > 	//优化sum，进行累加
   >     public void insert(String key, int val) {
   >         int _val = val;
   >         if (hash.containsKey(key))
   >             val -= hash.get(key);
   >         hash.put(key, _val);
   >         int p = 0;
   >         for (int i = 0; i < key.length(); i++) {
   >             int u = key.charAt(i) - 'a';
   >             if (trie[p][u] == 0) {
   >                 trie[p][u] = ++idx;
   >             }
   >             p = trie[p][u];
   >             cnt[p] += val;
   >         }
   >     }
   > 
   >     public int sum(String prefix) {
   >         int p = 0;
   >         for(int i=0;i<prefix.length();i++){
   >             int u = prefix.charAt(i)-'a';
   >             if(trie[p][u]==0){
   >                 return 0;
   >             }
   >             p = trie[p][u];
   >         }
   >         return cnt[p];
   >     }   
   > }
   > ```

4. [与数组中元素的最大异或值](https://leetcode.cn/problems/maximum-xor-with-an-element-from-array/description/)

   > https://mp.weixin.qq.com/s?__biz=MzU4NDE3MTEyMA==&mid=2247489259&idx=1&sn=042ee479cebfbcf1f3b517461b32ddac&chksm=fd9cbdf4caeb34e2254783b211bac795eb0c9bd9b4be844cf48450ca5afa7ca5694fd98f7d39&token=1848397639&lang=zh_CN#rd

5. [数组中两个数的最大异或值](https://leetcode.cn/problems/maximum-xor-of-two-numbers-in-an-array/description/)

   > 给你一个整数数组 `nums` ，返回 `nums[i] XOR nums[j]` 的最大运算结果，其中 `0 ≤ i ≤ j < n` 。
   >
   > `思路`
   >
   > 从高位往低找，对于每一个nums[j]，我们都试图让它的异或结果最大，然后去找这样的值是否存在。逐一更新答案。
   >
   > ```java
   > class TrieNode{
   >     TrieNode[] tns = new TrieNode[2];
   > }
   > private TrieNode root;
   > public Solution(){
   >     root = new TrieNode();
   > }
   > 
   > private void add(int x){
   >     TrieNode p = root;
   >     for(int i=31;i>=0;i--){
   >         int u = (x>>i) & 1;//屏蔽无关位
   >         if(p.tns[u]==null){
   >             p.tns[u] = new TrieNode();
   >         }
   >         p = p.tns[u];
   >     }
   > }
   > 
   > private int getXORVal(int x){
   >     int ans = 0;
   >     TrieNode p = root;
   >     for(int i=31;i>=0;i--){
   >         int a = (x>>i) & 1;
   >         int b = 1-a;//a与b异或结果为1的b的值
   >         if(p.tns[b]!=null){
   >             ans |= (b<<i);
   >             p = p.tns[b];
   >         }else{
   >             ans |= (a<<i);
   >             p = p.tns[a];
   >         }
   >     }
   >     return ans;
   > }
   > public int findMaximumXOR(int[] nums) {
   >     int ans = 0;
   >     for(int each:nums){
   >         add(each);
   >         int ant = getXORVal(each);
   >         ans = Math.max(ant^each, ans);
   >     }
   >     return ans;
   > }
   > ```
   >
   > 

6. [单词搜索 II](https://leetcode.cn/problems/word-search-ii/description/)

   > https://mp.weixin.qq.com/s?__biz=MzU4NDE3MTEyMA==&mid=2247489083&idx=1&sn=1971fdceb180ef3c7d51f8fbb81527d0&chksm=fd9cbd24caeb34321076e3f34bae0c001c9032b2b1814d15badab26cd4e8cddf48ac051550f6&scene=178&cur_album_id=2049538161285955584#rd

