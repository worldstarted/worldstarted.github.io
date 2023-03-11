# 数组

## 一、快慢指针

1. [删除有序数组中的重复项](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/)

   > 给你一个 升序排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 一致 。
   > 由于在某些语言中不能改变数组的长度，所以必须将结果放在数组nums的第一部分。更规范地说，如果在删除重复项之后有 k 个元素，那么 nums 的前 k 个元素应该保存最终结果。
   > 将最终结果插入 nums 的前 k 个位置后返回 k 。
   > 不要使用额外的空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。
   >
   > `思路`
   >
   > - 快慢指针，slow，fast，fast每找到一个不重复的元素，slow就前进一步，保证0-slow都是无重复的元素。
   >
   >   ```c++
   >   int removeDuplicates(vector<int>& nums) {
   >    int len = nums.size();
   >    int slow = 0, fast = 0;
   >    while(fast<len){
   >        if(nums[slow]!=nums[fast]){
   >            nums[++slow]=nums[fast];
   >        }
   >        fast++;
   >    }
   >    return slow+1;
   >   }
   >   ```
   >
   > - 通法
   >
   >   ```c++
   >   //如果是保留k位，对于前k个数字，可以直接保留，对于之后的每一个数字，只需要判断其与第k个是否相同，只有不相同，才可以保留
   >    int removeDuplicates(vector<int>& nums) {
   >        int idx = 0;
   >        for(auto each:nums){
   >            if(idx<k || nums[idx-k] != each)
   >                nums[idx++] = each;
   >        }
   >        return idx;
   >    }
   >   ```
   >
   
2. [删除有序数组中的重复项 II](https://leetcode.cn/problems/remove-duplicates-from-sorted-array-ii/)

   > 给你一个有序数组 nums ，请你 原地 删除重复出现的元素，使得出现次数超过两次的元素只出现两次 ，返回删除后数组的新长度。不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。
   >
   > `思路`
   >
   > 对于前2个数字，可以直接保留，对于之后的每一个数字，只需要判断其与第2个是否相同，只有不相同，才可以保留
   >
   > - 快慢指针
   >
   >   ```c++
   >   int removeDuplicates(vector<int>& nums) {
   >       int len = nums.size();
   >       if(len<=2)
   >           return len;
   >       int slow = 2, fast = 2;
   >       while(fast<len){
   >           if(nums[slow-2] != nums[fast]){
   >               nums[slow++] = nums[fast];
   >           }
   >           fast++;
   >       }
   >       return slow;
   >   }
   >   ```

3. [移除元素](https://leetcode.cn/problems/remove-element/)

   > 给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。
   > 不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。
   > 元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。
   >
   > `思路`
   >
   > - 法一： 左指针指向下一个赋值的位置，右指针指向当前处理的元素。
   >
   >   - 如果右指针指向的元素不等于val，那么一定在输出数组里，赋值给左指针，然后左右都右移一步
   >
   >   - 如果右指针指向的元素等于val，那么该元素会被舍弃，左边不动，右边右移一步。
   >
   >     ```c++
   >     int removeElement(vector<int>& nums, int val) {
   >         int len = nums.size();
   >         int slow=0,fast=0;
   >         while(fast<len){
   >             if(nums[fast]!=val){
   >             	nums[slow++]=nums[fast];
   >             }
   >         	fast++;
   >         }
   >         return slow;
   >     }
   >     ```
   >
   >     
   >
   > - 法二： 左指针指向指向当前要被赋值的元素，右指针指向处理的元素。
   >
   >   - 如果左指针指向元素不等于val，那么左指针右移，右指针左移
   >
   >   - 如果左指针指向元素等于val，那么左指针等于右指针指向的元素。
   >
   >   - 终止条件，左边等于右边
   >
   >     ```c++
   >     int removeElement(vector<int>& nums, int val) {
   >         int left=0,right = nums.size();
   >         while(left<right){
   >             if(nums[left]==val){
   >                 nums[left]=nums[--right];
   >             }else{
   >                 left++;
   >             }
   >         }
   >         return left;
   >     }
   >     ```
   >
   >     

## 二、左右指针

1. [两数之和 II - 输入有序数组](https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted/)

   > 给你一个下标从 1 开始的整数数组 numbers ，该数组已按 非递减顺序排列  ，请你从数组中找出满足相加之和等于目标数 target 的两个数。如果设这两个数分别是numbers[index1] 和 numbers[index2] ，则 1 <= index1 < index2 <= numbers.length 。
   > 以长度为 2 的整数数组 [index1, index2] 的形式返回这两个整数的下标 index1 和 index2。
   > 你可以假设每个输入 只对应唯一的答案 ，而且你 不可以 重复使用相同的元素。
   > 你所设计的解决方案必须只使用常量级的额外空间。
   >
   > `思路`
   >
   > 左右指针，如果和等于。返回，如果和大了，说明右边大了，左移，如果和小了，说明左边小了，右移。

2. [盛最多水的容器](https://leetcode.cn/problems/container-with-most-water/)

   > 给定一个长度为 n 的整数数组 height 。有 n 条垂线，第 i 条线的两个端点是 (i, 0) 和 (i, height[i]) 。
   > 找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。
   > 返回容器可以储存的最大水量。
   > 说明：你不能倾斜容器。
   >
   > `思路`
   >
   > 左指针，右指针，==长板向内，水平距离减少，总体积减少，短板向内，可能增大，可能减小==
   >
   > 所以，每次只需移动较短的即可。

3. [搜索二维矩阵 II](https://leetcode.cn/problems/search-a-2d-matrix-ii/)

   > 编写一个高效的算法来搜索 m x n 矩阵 matrix 中的一个目标值 target 。该矩阵具有以下特性：
   > 每行的元素从左到右升序排列。
   > 每列的元素从上到下升序排列。
   >
   > `思路`
   >
   > ==右上角==很特殊，往左，就是减小，往下，就是增大。

4. [反转字符串](https://leetcode.cn/problems/reverse-string/)

   > 编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 s 的形式给出。
   > 不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。
   >
   > `思路`
   >
   > 左右指针，交换内容，左指针往右走，右指针往左走。

5. [最长回文子串](https://leetcode.cn/problems/longest-palindromic-substring/)

   > 给你一个字符串 `s`，找到 `s` 中最长的回文子串。
   > 如果字符串的反序与原始字符串相同，则该字符串称为回文字符串。
   >
   > `思路`
   >
   > ==回文，中心向两边扩散==
   >
   > 分奇偶，然后向两边找，更新答案。

## 三、前缀和

1. [ 区域和检索 - 数组不可变](https://leetcode.cn/problems/range-sum-query-immutable/)

   > 给定一个整数数组  nums，处理以下类型的多个查询:
   > 计算索引 left 和 right （包含 left 和 right）之间的 nums 元素的 和 ，其中 left <= right
   > 实现 NumArray 类：
   > NumArray(int[] nums) 使用数组 nums 初始化对象
   > int sumRange(int i, int j) 返回数组 nums 中索引 left 和 right 之间的元素的 总和 ，包含 left 和 right 两点（也就是 nums[left] + nums[left + 1] + ... + nums[right] )
   >
   > `思路`
   >
   > 再构造一个数组用来存储前缀和。

2. [二维区域和检索 - 矩阵不可变](https://leetcode.cn/problems/range-sum-query-2d-immutable/)

   >  给定一个二维矩阵 matrix，以下类型的多个请求：
   > 计算其子矩形范围内元素的总和，该子矩阵的 左上角 为 (row1, col1) ，右下角 为 (row2, col2) 。
   > 实现 NumMatrix 类：
   > NumMatrix(int[][] matrix) 给定整数矩阵 matrix 进行初始化
   > int sumRegion(int row1, int col1, int row2, int col2) 返回 左上角 (row1, col1) 、右下角 (row2, col2) 所描述的子矩阵的元素 总和 。
   >
   > `思路`
   >
   > - 同上，构建一个二维数组用来存储和，实质上，结果是一层层的加起来，还是一维前缀和的方法
   >
   > - 二位前缀和，这样子，取答案的时候，就是O(1)，观察发现，设二维矩阵前缀和为$f$，则
   >  $$
   >   f(i,j) = matrix[i][j]+f(i-1,j)+f(i,j-1)-f(i-1,j-1)
   >  $$
   >
   >   ```c++
   >   NumMatrix(vector<vector<int>>& matrix) {
   >       for(int i=0;i<matrix.size();i++){
   >           for(int j=0;j<matrix[0].size();j++){
   >              //由于公式有i-1,j-1，所以为了方便计算，让sum矩阵的i,j比原矩阵大1
   >               sum[i+1][j+1] = matrix[i][j]+sum[i+1][j]+sum[i][j+1]-sum[i][j];
   >           }
   >       }
   >   }
   >     
   >   int sumRegion(int row1, int col1, int row2, int col2) {
   >       // 注意现在，组成四块的是row1,col1,row2,col2,所以i,j要换成这些
   >       return sum[row2+1][col2+1]+sum[row1][col1]-sum[row1][col2+1]-sum[row2+1][col1];
   >   }
   >   ```

## 四、差分数组

1. [航班预订统计](https://leetcode.cn/problems/corporate-flight-bookings/)

   > 这里有 n 个航班，它们分别从 1 到 n 进行编号。
   > 有一份航班预订表 bookings ，表中第 i 条预订记录 bookings[i] = [firsti, lasti, seatsi] 意味着在从 firsti 到 lasti （包含 firsti 和 lasti ）的 每个航班 上预订了 seatsi 个座位。请你返回一个长度为 n 的数组 answer，里面的元素是每个航班预定的座位总数。
   >
   > `思路`
   >
   > - 模拟
   >
   > - 差分算法
   >
   >   区间加一个数，等价于，$diff[left] += val, diff[right+1] -= val$
   >
   >   ```java
   >   public int[] corpFlightBookings(int[][] bookings, int n) {
   >   	int [] ans = new int [n];
   >       for(int[] each:bookings){
   >       	ans[each[0]-1] += each[2];
   >           if(each[1]<n){
   >           	ans[each[1]] -= each[2];
   >           }
   >       }
   >       for(int i=1;i<n;i++)
   >       ans[i] += ans[i-1];
   >       return ans;
   >   ```

2. [拼车](https://leetcode.cn/problems/car-pooling/)

   > 车上最初有 capacity 个空座位。车 只能 向一个方向行驶（也就是说，不允许掉头或改变方向）
   >
   > 给定整数 capacity 和一个数组 trips ,  trip[i] = [numPassengersi, fromi, toi] 表示第 i 次旅行有 numPassengersi 乘客，接他们和放他们的位置分别是 fromi 和 toi 。这些位置是从汽车的初始位置向东的公里数。
   >
   > 当且仅当你可以在所有给定的行程中接送所有乘客时，返回 true，否则请返回 false。
   >
   > `思路`
   >
   > 区间加减，差分数组
   >
   > ```java
   > public boolean carPooling(int[][] trips, int capacity) {
   >     int [] ans = new int[1005];
   >     for(int[] trip:trips){
   >         ans[trip[1]] += trip[0];
   >         ans[trip[2]] -= trip[0];
   >     }
   >     if(ans[0]>capacity)
   >         return false;
   >     for(int i=1;i<1001;i++){
   >         ans[i] += ans[i-1];
   >         if(ans[i]>capacity)
   >             return false;
   >     }
   >     return true;
   > }
   > ```

## 五、二维数组的特殊操作

1. [旋转图像](https://leetcode.cn/problems/rotate-image/)

   > 给定一个 n × n 的二维矩阵 matrix 表示一个图像。请你将图像顺时针旋转 90 度。
   >
   > 你必须在 原地 旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要 使用另一个矩阵来旋转图像。
   >
   > `思路`
   >
   > 参考[反转字符串中的单词](https://leetcode.cn/problems/reverse-words-in-a-string/)
   >
   > ```java
   > class Solution {
   >     public String reverseWords(String s) {
   >         int left = 0;
   >         int right = s.length()-1;
   >         while(left<=right && s.charAt(left)==' ')
   >             left++;
   >         while(left<=right&&s.charAt(right)==' ')
   >             right--;
   >         Deque<String> dq = new ArrayDeque<String>();
   >         StringBuilder sb = new StringBuilder();
   >         while(left<=right){
   >             char c = s.charAt(left);
   >             if(sb.length()>0&&c==' '){
   >                 dq.offerFirst(sb.toString());
   >                 sb.setLength(0);
   >             }
   >             else if(c!=' ')
   >                 sb.append(c);
   >             left++;
   >         }
   >         dq.offerFirst(sb.toString());
   >         return String.join(" ",dq);
   >     }
   > }
   > ```
   >
   > 观察发现，先把矩阵的行做反转，之后再做转置

2. [螺旋矩阵](https://leetcode.cn/problems/spiral-matrix/)

   > 给你一个 `m` 行 `n` 列的矩阵 `matrix` ，请按照 **顺时针螺旋顺序** ，返回矩阵中的所有元素。
   >
   > `思路`
   >
   > ==模拟==，定义四个边界，逐一遍历
   >
   > ```java
   > int colLeft = 0;
   > int rowTop = 0;
   > int colRgiht = matrix[0].length-1;
   > int rowBottom = matrix.length-1;
   > while(true){
   >     // right
   >     for(int j = colLeft;j<=colRgiht;j++){
   >         ans.add(matrix[rowTop][j]);
   >     }
   >     rowTop++;
   >     if(rowBottom<rowTop)
   >         break;
   > 
   >     // down
   >     for(int i=rowTop;i<=rowBottom;i++){
   >         ans.add(matrix[i][colRgiht]);
   >     }
   >     colRgiht--;
   >     if(colLeft>colRgiht)
   >         break;
   > 
   >     //left
   >     for(int j=colRgiht;j>=colLeft;j--){
   >         ans.add(matrix[rowBottom][j]);
   >     }
   >     rowBottom--;
   >     if(rowBottom<rowTop)
   >         break;
   > 
   > 
   >     //up
   >     for(int i = rowBottom;i>=rowTop;i--){
   >         ans.add(matrix[i][colLeft]);
   >     }    
   >     colLeft++;
   >     if(colLeft>colRgiht)
   >         break;
   > }
   > ```

3. [螺旋矩阵 II](https://leetcode.cn/problems/spiral-matrix-ii/)

   > 给你一个正整数 `n` ，生成一个包含 `1` 到 `n2` 所有元素，且元素按顺时针顺序螺旋排列的 `n x n` 正方形矩阵 `matrix` 。
   >
   > `思路`
   >
   > 和螺旋矩阵一样，按照右下左上，往里填数据就行

## 六、滑动窗口

```java
//模板
/* 滑动窗口算法框架 */
void slidingWindow(string s) {
    unordered_map<char, int> window;
    
    int left = 0, right = 0;
    while (right < s.size()) {
        // c 是将移入窗口的字符
        char c = s[right];
        // 增大窗口
        right++;
        // 进行窗口内数据的一系列更新
        ...

        /*** debug 输出的位置 ***/
        // 注意在最终的解法代码中不要 print
        // 因为 IO 操作很耗时，可能导致超时
        printf("window: [%d, %d)\n", left, right);
        /********************/
        
        // 判断左侧窗口是否要收缩
        while (window needs shrink) {
            // d 是将移出窗口的字符
            char d = s[left];
            // 缩小窗口
            left++;
            // 进行窗口内数据的一系列更新
            ...
        }
    }
}
```

1. [最小覆盖子串](https://leetcode.cn/problems/minimum-window-substring/)

   > 给你一个字符串 `s` 、一个字符串 `t` 。返回 `s` 中涵盖 `t` 所有字符的最小子串。如果 `s` 中不存在涵盖 `t` 所有字符的子串，则返回空字符串 `""` 。
   >
   > `思路`
   >
   > 构建滑动窗口
   >
   > ```java
   > class Solution {
   >     public String minWindow(String s, String t) {
   >         Map<Character,Integer> window = new HashMap<Character,Integer>();
   >         Map<Character,Integer> need = new HashMap<Character,Integer>();
   >         for(int i=0;i<t.length();i++){
   >             need.put(t.charAt(i), need.getOrDefault(t.charAt(i),0)+1);
   >         }
   >         int left = 0;
   >         int right = 0;
   >         int valid = 0;
   >         int start = 0, len = Integer.MAX_VALUE;
   >         while(right<s.length()){
   >             Character c = s.charAt(right);
   >             right+=1;
   >             if(need.containsKey(c)){//如果该字符是需要的
   >                 window.put(c,window.getOrDefault(c,0)+1);//就在窗口里加入
   >                 if(window.get(c).equals(need.get(c)))//判断窗口里的值和需要的值是否相同
   >                     valid++;
   >             }
   >             while(valid == need.size()){
   >                 if(right-left<len){//更新最小长度
   >                     start = left;
   >                     len = right-start;
   >                 }
   >                 Character d = s.charAt(left);
   >                 left++;
   >                 if(need.containsKey(d)){
   >                     if(window.get(d).equals(need.get(d))){
   >                         valid--;
   >                     }
   >                     window.replace(d,window.get(d)-1);
   >                 }
   >             }
   >         }
   >         return len == Integer.MAX_VALUE?"":s.substring(start,start+len);
   >     }
   > }
   > ```

2. [字符串的排列](https://leetcode.cn/problems/permutation-in-string/)

   > 给你两个字符串 s1 和 s2 ，写一个函数来判断 s2 是否包含 s1 的排列。如果是，返回 true ；否则，返回 false 。
   >
   > 换句话说，s1 的排列之一是 s2 的 子串 。
   >
   > `思路`
   >
   > s1的排列之一是s2的子串，那么，在s2的某个窗口内，只要其字符数与s1的完全一致，由于是排列，所以一定满足子串的条件。
   >
   > 因此，就转化成了滑动窗口的问题。

3. [找到字符串中所有字母异位词](https://leetcode.cn/problems/find-all-anagrams-in-a-string/)

   > 给定两个字符串 s 和 p，找到 s 中所有 p 的 异位词 的子串，返回这些子串的起始索引。不考虑答案输出的顺序。
   >
   > 异位词 指由相同字母重排列形成的字符串（包括相同的字符串）。
   >
   > `思路`
   >
   > 基本同上

4. [无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

   > 给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。
   >
   > `思路`
   >
   > 收缩窗口的条件是什么？ 何时更新答案？
   >
   > - 收缩窗口要等到当前字符的数量大于一，说明有重复了
   > - 只有没有重复的字符，才可以更新答案，也就是，窗口收缩后才能。

5. [重复的DNA序列](https://leetcode.cn/problems/repeated-dna-sequences/)

   > DNA序列 由一系列核苷酸组成，缩写为 'A', 'C', 'G' 和 'T'.。
   >
   > 例如，"ACGAATTCCG" 是一个 DNA序列 。
   > 在研究 DNA 时，识别 DNA 中的重复序列非常有用。
   >
   > 给定一个表示 DNA序列 的字符串 s ，返回所有在 DNA 分子中出现不止一次的 长度为 10 的序列(子字符串)。你可以按 任意顺序 返回答案。
   >
   > `思路`

6. [找出字符串中第一个匹配项的下标](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/)

   > 给你两个字符串 haystack 和 needle ，请你在 haystack 字符串中找出 needle 字符串的第一个匹配项的下标（下标从 0 开始）。如果 needle 不是 haystack 的一部分，则返回  -1 。
   >
   > `思路`
   >
   > RK算法
   >
   > ```java
   > // Rabin-Karp 指纹字符串查找算法
   > int rabinKarp(String txt, String pat) {
   >     // 位数
   >     int L = pat.length();
   >     // 进制（只考虑 ASCII 编码）
   >     int R = 256;
   >     // 取一个比较大的素数作为求模的除数
   >     long Q = 1658598167;
   >     // R^(L - 1) 的结果
   >     long RL = 1;
   >     for (int i = 1; i <= L - 1; i++) {
   >         // 计算过程中不断求模，避免溢出
   >         RL = (RL * R) % Q;
   >     }
   >     // 计算模式串的哈希值，时间 O(L)
   >     long patHash = 0;
   >     for (int i = 0; i < pat.length(); i++) {
   >         patHash = (R * patHash + pat.charAt(i)) % Q;
   >     }
   >     
   >     // 滑动窗口中子字符串的哈希值
   >     long windowHash = 0;
   >     
   >     // 滑动窗口代码框架，时间 O(N)
   >     int left = 0, right = 0;
   >     while (right < txt.length()) {
   >         // 扩大窗口，移入字符
   >         windowHash = ((R * windowHash) % Q + txt.charAt(right)) % Q;
   >         right++;
   > 
   >         // 当子串的长度达到要求
   >         if (right - left == L) {
   >             // 根据哈希值判断是否匹配模式串
   >             if (windowHash == patHash) {
   >                 // 当前窗口中的子串哈希值等于模式串的哈希值
   >                 // 还需进一步确认窗口子串是否真的和模式串相同，避免哈希冲突
   >                 if (pat.equals(txt.substring(left, right))) {
   >                     return left;
   >                 }
   >             }
   >             // 缩小窗口，移出字符
   >             windowHash = (windowHash - (txt.charAt(left) * RL) % Q + Q) % Q;
   >             // X % Q == (X + Q) % Q 是一个模运算法则
   >             // 因为 windowHash - (txt[left] * RL) % Q 可能是负数
   >             // 所以额外再加一个 Q，保证 windowHash 不会是负数
   > 
   >             left++;
   >         }
   >     }
   >     // 没有找到模式串
   >     return -1;
   > }
   > 
   > ```
   >
   > `KMP算法`
   >
   > ```java
   > public int strStr(String haystack, String needle) {
   >     int []next = new int[needle.length()];
   >     int j=0,k=-1;
   >     next[0]=-1;
   >     while(j<needle.length()-1){
   >         if(k==-1 || needle.charAt(j)==needle.charAt(k)){
   >             next[++j] = ++k;
   >         }else{
   >             k = next[k];
   >         }
   >     }
   >     int i=0;
   >     j=0;
   >     while(i<haystack.length()&&j<needle.length()){
   >         if(j==-1||haystack.charAt(i)==needle.charAt(j)){
   >             i++;
   >             j++;
   >         }else{
   >             j = next[j];
   >         }
   >     }
   >     if(j==needle.length()){
   >         return i-j;
   >     }return -1;
   > }
   > ```
   >
   > 

## 七、二分搜索

###  1 基本的二分搜索

```java
int binarySearch(int[] nums, int target) {
    int left = 0; 
    int right = nums.length - 1; // 注意

    while(left <= right) {
        int mid = left + (right - left) / 2;
        if(nums[mid] == target)
            return mid; 
        else if (nums[mid] < target)
            left = mid + 1; // 注意
        else if (nums[mid] > target)
            right = mid - 1; // 注意
    }
    return -1;
}
```

`注意`

while循环的<= 与 < 的问题

> <= right = len-1 搜索区间是`[ left, right ]` 左闭右闭   终止区间为空
>
> <   right = len 搜索区间是 ` [ left, right )` 左闭，右开， 终止区间为 ` [ end, end ]`

### 2 寻找左侧边界的二分搜索

```java
int binarySearch(int nums[], int targer){
    int left = 0;
    int right = nums.length; // 注意
    
    while (left < right) { // 注意
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            right = mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid; // 注意
        }
    }
    // 此时 target 比所有数都大，返回 -1
    if (left == nums.length) return -1;
    // 判断一下 nums[left] 是不是 target
    return nums[left] == target ? left : -1;
}
```

1. while` <` 而非` <=`

   > right = nums.length，搜索区间为` [ left, right )`
   >
   > 终止条件， `[ left, left )`

2. `left = mid+1`与`right = mid`

   > 搜索区间为`[left,right)`，所以每次判断完nums[mid]后，应该变成`[left,mid)`或`[mid+1, right)`，在mid的左侧或右侧找

### 3 寻找右侧边界的二分搜索

```java
int right_bound(int[] nums, int target) {
    int left = 0, right = nums.length;
    
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            left = mid + 1; // 注意
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid;
        }
    }
    return left - 1; // 注意
}
```

### 4 总结

```java
int binary_search(int[] nums, int target) {
    int left = 0, right = nums.length - 1; 
    while(left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1; 
        } else if(nums[mid] == target) {
            // 直接返回
            return mid;
        }
    }
    // 直接返回
    return -1;
}

int left_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，锁定左侧边界
            right = mid - 1;
        }
    }
    // 判断 target 是否存在于 nums 中
    // 此时 target 比所有数都大，返回 -1
    if (left == nums.length) return -1;
    // 判断一下 nums[left] 是不是 target
    return nums[left] == target ? left : -1;
}

int right_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，锁定右侧边界
            left = mid + 1;
        }
    }
    // 此时 left - 1 索引越界
    if (left - 1 < 0) return -1;
    // 判断一下 nums[left] 是不是 target
    return nums[left - 1] == target ? (left - 1) : -1;
}

```

[在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)

> 给你一个按照非递减顺序排列的整数数组 nums，和一个目标值 target。请你找出给定目标值在数组中的开始位置和结束位置。
>
> 如果数组中不存在目标值 target，返回 [-1, -1]。
>
> 你必须设计并实现时间复杂度为 O(log n) 的算法解决此问题。
>
> `思路`
>
> 二分搜索左侧边界，然后遍历找右侧边界。

## 八、随机选择

[按权重随机选择](https://leetcode.cn/problems/random-pick-with-weight/)

> 给你一个 下标从 0 开始 的正整数数组 w ，其中 w[i] 代表第 i 个下标的权重。
>
> 请你实现一个函数 pickIndex ，它可以 随机地 从范围 [0, w.length - 1] 内（含 0 和 w.length - 1）选出并返回一个下标。选取下标 i 的 概率 为 w[i] / sum(w) 。
>
> 例如，对于 w = [1, 3]，挑选下标 0 的概率为 1 / (1 + 3) = 0.25 （即，25%），而选取下标 1 的概率为 3 / (1 + 3) = 0.75（即，75%）。
>
> `思路`
>
> <img src="C:\Users\ldx\AppData\Roaming\Typora\typora-user-images\image-20230310161205871.png" alt="image-20230310161205871" style="zoom:50%;" />
>
> 通过前缀和模拟概率，在这种情况下， 随机在线段上投一个点，落在哪，就取其索引即可。
>
> ```java
> private int[] presum ;
> private Random rand = new Random();
> 
> public Solution(int[] w) {
>     presum = new int [w.length+1];
>     presum[0] = 0;
>     for(int i=1;i<=w.length;i++){
>         presum[i] = presum[i-1]+w[i-1];
>     }
> }
> 
> public int pickIndex() {
>     int len = presum.length;
>     int target = rand.nextInt(presum[len-1])+1;
>     int left=0, right = len;
>     while (left<right){
>         int mid = left+ (right-left)/2;
>         if(presum[mid]==target){
>             right = mid;
>         }else if(presum[mid]>target){
>             right = mid;
>         }else{
>             left = mid+1;
>         }
>     }
>     return left-1;
> }
> ```

## 九、二分扩展

1. [在 D 天内送达包裹的能力](https://leetcode.cn/problems/capacity-to-ship-packages-within-d-days/)

   > 传送带上的包裹必须在 days 天内从一个港口运送到另一个港口。
   >
   > 传送带上的第 i 个包裹的重量为 weights[i]。每一天，我们都会按给出重量（weights）的顺序往传送带上装载包裹。我们装载的重量不会超过船的最大运载重量。
   >
   > 返回能在 days 天内将传送带上的所有包裹送达的船的最低运载能力。
   >
   > `思路`
   >
   > 可以看到，超过最低运载能力x时，可以提前运完，低于x时，无法提前运完。
   >
   > 这转化成了一个二分问题。
   >
   > 左边界，所有货物中的最大值
   >
   > 右边界，所有货物的总和
   >
   > 判断标准，当前运载能力下，需要的天数与days之间的关系。
   >
   > ```java
   > public int shipWithinDays(int[] weights, int days) {
   >     int left = 0, right = 0;
   >     for(int w:weights){
   >         right += w;
   >         left = Math.max(left, w);
   >     }
   >     while(left<right){
   >         int mid = left + (right-left)/2;
   >         int need = 1, cur = 0;
   >         for(int w:weights){
   >             if(cur+w>mid){//当天运载的货物超过运载能力mid
   >                 need++;//加一天
   >                 cur = 0;//重置运载货物数
   >             }
   >             cur += w;
   >         }
   >         if(need>days){
   >             left = mid+1;
   >         }else if(need<=days){//答案是找最少运载能力，所以是在寻找左边界
   >             right = mid;
   >         }
   >     }
   >     return left;
   > }
   > ```
   >
   > 

2. [分割数组的最大值](https://leetcode.cn/problems/split-array-largest-sum/)

   > 给定一个非负整数数组 `nums` 和一个整数 `m` ，你需要将这个数组分成 `m` 个非空的连续子数组。设计一个算法使得这 `m` 个子数组各自和的最大值最小。
   >
   > `思路`
   >
   > ==二分+贪心==
   >
   > 关键在于连续，m次是固定的，子数组和是变化的
   >
   > 求的是子数组和的最大值里的最小值，这个子数组和的最大值，最小可以小到单个元素，最大可以到整个数组元素和
   >
   > 对其进行二分查找
   >
   > ```java
   > public int splitArray(int[] nums, int k) {
   >     int left = 0, right = 0;
   >     for(int each:nums){
   >         left = Math.max(each,left);
   >         right += each;
   >     }
   >     while(left<right){
   >         int mid = left+ (right-left)/2;
   >         int need = 1, sum = 0;
   >         for(int each:nums){
   >             if(each+sum>mid){
   >                 sum=0;
   >                 need++;
   >             }
   >             sum+=each;
   >         }
   >         if(need<=k){
   >             right = mid;
   >         }else if(need>k){
   >             left = mid+1;
   >         }
   >     }
   >     return left;
   > }
   > ```
   >
   > ==动态规划==
   >
   > 「将数组分割为 *m* 段，求……」是动态规划题目常见的问法。
   >
   > 
   
   
