# 链表

## 一、 操作链表

### a. 合并有序链表

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

### b. 链表分解

1.  [分隔链表](https://leetcode.cn/problems/partition-list/)

   > 给你一个链表的头节点 head 和一个特定值 x ，请你对链表进行分隔，使得所有 小于 x 的节点都出现在 大于或等于 x 的节点之前。你应当 保留 两个分区中每个节点的初始相对位置
   >
   > `思路`
   >
   > - 模拟
   >
   >   建两个链表，一个存小的，一个存大的，最后连起来。
   >
   

### c. 反转链表

1. [反转链表](https://leetcode.cn/problems/reverse-linked-list/)

   > 给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。
   >
   > `思路`
   >
   > - 迭代
   >
   >   交换元素指针指向
   >
   > - 递归
   >
   >   递归，从后往前，所以是后面的先排好
   >
   >   假设k+1都排好了，对于k，希望k->next->next = k
   >
   >   注意，$n_1$->next = nullptr
   >
   >   ![image-20230226102948289](C:\Users\ldx\AppData\Roaming\Typora\typora-user-images\image-20230226102948289.png)
   >
   >   ```c++
   >   ListNode* reverse(ListNode* head){
   >       if(!head || !head->next)	return head;
   >       ListNode* tep = reverse(head->next);
   >       head->next->next = head;
   >       head->next = nullptr;
   >       return tep;
   >   }
   >   ```
   >

2. [反转链表 II](https://leetcode.cn/problems/reverse-linked-list-ii/)

   > 给你单链表的头指针 head 和两个整数 left 和 right ，其中 left <= right 。请你反转从位置 left 到位置 right 的链表节点，返回 反转后的链表 。
   >
   > `思路`
   >
   > 找到left和right的区间，先断开和之前的链接，再当作独立的链表反转，最后链接上去
   >
   > ```c++
   > ListNode* reverseBetween(ListNode* head, int left, int right) {
   >         ListNode* sor = new ListNode();
   >         sor->next = head;
   >         ListNode* pre = sor; //pre永远指向反转区域的第一个节点的前一个节点
   >         for(int i=0;i<left-1;i++)
   >             pre = pre->next;
   >         ListNode* cur = pre->next;//cur指向反转区域的第一个节点	
   >         for(int i=0;i<right-left;i++){
   >             ListNode* nxt = cur->next;//cur的下一个节点
   >             cur->next = nxt->next;//断开原来链接，换成下下个
   >             nxt->next = pre->next;//将c断开的节点链接反转区域的头节点
   >             pre->next = nxt;//反转区域的头节点和它的前一个节点重新链接
   >         }
   >         return sor->next;
   > }
   > ```

3. **[K 个一组翻转链表](https://leetcode.cn/problems/reverse-nodes-in-k-group/)**

   > 给你链表的头节点 head ，每 k 个节点一组进行翻转，请你返回修改后的链表。
   > k 是一个正整数，它的值小于或等于链表的长度。如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。
   > 你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。
   >
   > `思路`
   >
   > 每个区间先反转，然后递归反转
   >
   > - 代码一，递归
   >
   >   ```c++
   >   ListNode* reverseKGroup(ListNode* head, int k) {
   >           if(!head) return nullptr;
   >           ListNode* a = head;
   >           ListNode* b = head;
   >           for(int i=0;i<k;i++){
   >               if(!b)
   >                   return head;
   >               b = b->next;
   >           }
   >           ListNode* newHead = reverseList(a,b);
   >           a->next = reverseKGroup(b,k);
   >           return newHead;
   >       }
   >   
   >   ListNode* reverseList(ListNode* head, ListNode* tail){
   >       ListNode* pre = nullptr;
   >       ListNode* p = head;
   >       while(p!=tail){
   >           ListNode* tep = p->next;
   >           p->next = pre;
   >           pre = p;
   >           p = tep;
   >       }
   >       return pre;
   >   }
   >   ```
   >
   > - 代码二，迭代
   >
   >   ```c++
   >   ListNode* reverseKGroup(ListNode* head, int k) {
   >           ListNode* hair = new ListNode();
   >           hair->next = head;
   >           ListNode* pre = hair;
   >           while(head){
   >               ListNode* tail = pre;
   >               for(int i=0;i<k;i++){
   >                   tail = tail->next;
   >                   if(!tail){
   >                       return hair->next;
   >                   }
   >               }
   >               ListNode* nxt = tail->next;
   >               tie(head,tail) = reverseList(head,tail);
   >               pre->next = head;
   >               tail->next = nxt;
   >               pre = tail;
   >               head = tail->next;
   >           }
   >           return hair->next;
   >       }
   >   
   >   pair<ListNode*, ListNode*> reverseList(ListNode* head, ListNode* tail){
   >       ListNode* pre = tail->next;
   >       ListNode* p = head;
   >       while(pre != tail ){
   >           ListNode* tep = p->next;
   >           p->next = pre;
   >           pre = p;
   >           p = tep;
   >       }
   >       return {tail, head};
   >   }
   >   ```
   >
   >   
   >

4. **[回文链表](https://leetcode.cn/problems/palindrome-linked-list/)**

   > 给你一个单链表的头节点 `head` ，请你判断该链表是否为回文链表。如果是，返回 `true` ；否则，返回 `false` 
   >
   > `思路`
   >
   > - 回文的本质是，从中心向两边扩散，但由于是单链表，只能伪造双指针，可以结合后序遍历
   >
   >   ```c++
   >   ListNode* left;
   >       bool isPalindrome(ListNode* head) {
   >           left = head;
   >           return traverse(head);
   >       }
   >   
   >   bool traverse(ListNode* right){
   >       if(!right)
   >           return 1;
   >       bool ans = traverse(right->next);
   >       ans = ans && (left->val==right->val);
   >       left = left->next;
   >       return ans;
   >   }
   >   ```
   >
   > - 装入数组，按传统的方法，从两边往中心比较
   >
   >   ```c++
   >   bool isPalindrome(ListNode* head) {
   >       vector<int> vals;
   >       while (head != nullptr) {
   >           vals.emplace_back(head->val);
   >           head = head->next;
   >       }
   >       for (int i = 0, j = (int)vals.size() - 1; i < j; ++i, --j) {
   >           if (vals[i] != vals[j]) {
   >               return false;
   >           }
   >       }
   >       return true;
   >   }
   >   ```
   >
   > - 反转再比较

## 二、操作链表元素

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
   >  `思路`
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
   >如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。注意：pos 不作为参数进行传递 。仅仅是为了标识链表的实际情况。
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
   >         ListNode* slow = head;
   >         ListNode* fast = head;
   >         while(fast&&fast->next){
   >             fast=fast->next->next;
   >             slow=slow->next;
   >             if(fast==slow)
   >                 break;
   >         }
   >         if(fast==nullptr||fast->next==nullptr) //判断有环无环
   >             return nullptr;
   >         fast = head;
   >         while(fast!=slow){
   >             fast=fast->next;
   >             slow=slow->next;
   >         }
   >         return fast;
   >     }
   > ```

5. [相交链表](https://leetcode.cn/problems/intersection-of-two-linked-lists/)

   > 给你两个单链表的头节点 `headA` 和 `headB` ，请你找出并返回两个单链表相交的起始节点。如果两个链表不存在相交节点，返回 `null` 。题目数据 **保证** 整个链式结构中不存在环。
   >
   > `思路`
   >
   > 由于两链表长度不一，核心是消除长度差异。
   >
   > 两者从头跑，先跑到头的然后从另外一个的起点重新跑，如此，两者相遇时，便是相交节点。==交换路径==
   >
   > 证明如下：
   >
   > 对于链表A，从起点到相遇节点的距离为a，对于节点B，从起点到相遇节点的距离为b，相遇节点到终点的距离都为m，不妨假设B的长度大于A，则当A先跑完时，B的位置在b-a处，而此时A也从B起点出发，当A跑完b-a时，B跑完，从A开始，两者此时的链表长度相同。

