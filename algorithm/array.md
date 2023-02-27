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
   >            slow++;
   >            nums[slow]=nums[fast];
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
   >   int removeDuplicates(vector<int>& nums) {
   >       int idx = 0;
   >       for(auto each:nums){
   >           if(idx<k || nums[idx-k] != each)
   >               nums[idx++] = each;
   >       }
   >       return idx;
   >   }
   >   ```

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

