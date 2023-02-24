# 链表

## 1. 合并有序链表

1. [合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)

   > 将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。
   >
   > `思路`
   >
   > - 迭代
   >
   >   设置空的头节点，然后两个有序列表逐一比较大小，连入头节点
   >
   > - 递归
   >
   >   终止条件，两个链表有一个为空即可

2. [合并K个升序链表](https://leetcode.cn/problems/merge-k-sorted-lists/)

   > 给你一个链表数组，每个链表都已经按升序排列。请你将所有链表合并到一个升序链表中，返回合并后的链表。
   >
   > `思路`
   >
   > - 顺序合并
   >
   >   直接两两合并即可
   >
   > - 分治合并
   >
   >   类似快速幂的思想，分组合并，再组之间合并
   >
   >   ```c++
   >   ListNode* div(vector<ListNode*>& lists, int l, int r){
   >           if(l==r)
   >               return lists[l];
   >           else if(l>r)
   >               return nullptr;
   >           int mid = (l+r)>>1;
   >           return merge(div(lists,l,mid),div(lists,mid+1,r));
   >   }
   >   ```
   >
   > - 

## 2. 链表分解

1. [分隔链表](https://leetcode.cn/problems/partition-list/)

   > 给你一个链表的头节点 head 和一个特定值 x ，请你对链表进行分隔，使得所有 小于 x 的节点都出现在 大于或等于 x 的节点之前。你应当 保留 两个分区中每个节点的初始相对位置
   >
   > `思路`
   >
   > - 模拟
   >
   >   建两个链表，一个存小的，一个存大的，最后连起来。



## 3. 操作链表元素

1. [删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

   > 给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。
   >
   > `思路`
   >
   > <img src="C:\Users\ldx\AppData\Roaming\Typora\typora-user-images\image-20230224102047394.png" alt="image-20230224102047394" style="zoom:50%;" />
   >
   > 设总长度为len，则倒数第n个节点就是正数第len-n+1个节点，但无法知道总长度
   >
   > 如果有两个指针p1，p2，当p2恰好走到len-n+1时，p1已经走完了，即p1=len+1，所以，两者之间差为n
   >
   > 综上，只需要让p1先走n步即可。

2. [链表的中间结点](https://leetcode.cn/problems/middle-of-the-linked-list/)

   > 给你单链表的头结点 `head` ，请你找出并返回链表的中间结点。如果有两个中间结点，则返回第二个中间结点。
   >
   > `思路`
   >
   > 不妨假设链表长度为n，则就变成了返回第$\lceil{\frac{n}{2}}\rceil$个节点，因此只需要遍历出即可。==同步指针==
   >
   > 如果有两个指针p1，p2，当p1走到n时，p2走到$\lceil{\frac{n}{2}}\rceil$，所以，如果它们都是从head出发，则说明p1速度是p2的两倍才行
   >
   > 综上，只需要p2走1，p1走2
   >
   > <img src="C:\Users\ldx\AppData\Roaming\Typora\typora-user-images\image-20230224144121877.png" alt="image-20230224144121877" style="zoom:50%;" />
   >
   > <img src="C:\Users\ldx\AppData\Roaming\Typora\typora-user-images\image-20230224144141313.png" alt="image-20230224144141313" style="zoom:50%;" />

3. [环形链表](https://leetcode.cn/problems/linked-list-cycle/)

   > 给你一个链表的头节点 head ，判断链表中是否有环。
   > 如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。注意：pos 不作为参数进行传递 。仅仅是为了标识链表的实际情况。
   > 如果链表中存在环 ，则返回 true 。 否则，返回 false 。
   >
   > `思路`
   >
   > 成环可以看成赛跑套圈的问题。==同步指针==

4. [环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/)

   > 给定一个链表的头节点  head ，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。
   > 如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。
   > 不允许修改 链表。
   >
   > `思路`
   >
   > 假设有两个指针，slow，fast，速度比1:2，当两者相遇时，若slow走了k步，则fast走了2k步，一圈的长度为k，假设起点到相遇节点距离为s，则入环节点到相遇节点距离为k-s
   >
   > <img src="C:\Users\ldx\AppData\Roaming\Typora\typora-user-images\image-20230224191007683.png" alt="image-20230224191007683" style="zoom:50%;" />
   >
   > ```c++
   > ListNode *detectCycle(ListNode *head) {
   >      ListNode* slow = head;
   >      ListNode* fast = head;
   >      while(fast&&fast->next){
   >          fast=fast->next->next;
   >          slow=slow->next;
   >          if(fast==slow)
   >              break;
   >      }
   >      if(fast==nullptr||fast->next==nullptr) //判断有环无环
   >          return nullptr;
   >      fast = head;
   >      while(fast!=slow){
   >          fast=fast->next;
   >          slow=slow->next;
   >      }
   >      return fast;
   >  }
   > ```

5. [相交链表](https://leetcode.cn/problems/intersection-of-two-linked-lists/)

   > 给你两个单链表的头节点 `headA` 和 `headB` ，请你找出并返回两个单链表相交的起始节点。如果两个链表不存在相交节点，返回 `null` 。题目数据 **保证** 整个链式结构中不存在环。
   >
   > `思路`
   >
   > 

