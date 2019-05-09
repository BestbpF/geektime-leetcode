[TOC]

# 简述

极客时间算法40讲中所出现的leetcode算法题

# 题目

#### [【链表】reverse-linked-list（反转一个单链表）](https://leetcode-cn.com/problems/reverse-linked-list/)

```
示例:
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```
**代码**

`递归`

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode node = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return node;
    }
}
```
`迭代`

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        while(head != null){
            ListNode tmp = head.next;
            head.next = prev;
            prev = head;
            head = tmp;
        }
        return prev;
    }
}
```

------------

#### [【链表】swap-nodes-in-pairs（两两交换链表中的节点）](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。
你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

```
示例:
给定 1->2->3->4, 你应该返回 2->1->4->3.
```

**代码**

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode res = head.next;
        ListNode pre = new ListNode(-1);
        pre.next = head;
        while(pre.next != null && pre.next.next != null){
            ListNode a = pre.next;
            ListNode b = a.next;
            pre.next = b;
            a.next = b.next;
            b.next = a;
            pre = a;
        }
        return res;
    }
}
```

--------------------

#### [【链表】linked-list-cycle（环形链表）](https://leetcode-cn.com/problems/linked-list-cycle/)

给定一个链表，判断链表中是否有环。

为了表示给定链表中的环，我们使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 `pos` 是 `-1`，则在该链表中没有环。

**示例 1：**

```
输入：head = [3,2,0,-4], pos = 1
输出：true
解释：链表中有一个环，其尾部连接到第二个节点。
```
![](http://upload-images.jianshu.io/upload_images/13065313-34213dc5d38dcd68.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**示例 2：**

```
输入：head = [1,2], pos = 0
输出：true
解释：链表中有一个环，其尾部连接到第一个节点。
```

![](http://upload-images.jianshu.io/upload_images/13065313-fe9726415b946d03.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**示例 3：**

```
输入：head = [1], pos = -1
输出：false
解释：链表中没有环。
```

![](http://upload-images.jianshu.io/upload_images/13065313-c6d3fb051f518174.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**代码**

`双指针`

```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null || head.next == null || head.next.next == null) return false;
        ListNode slow = head;
        ListNode fast = head;
        while(fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;
            if(fast == slow){
                return true;
            }
        }
        return false;
    }
}
```
`set检测重复`
```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        Set<ListNode> set = new HashSet<>();
        while(head != null){
            if(set.contains(head)) return true;
            set.add(head);
            head = head.next;
        }
        return false;
    }
}
```

---------------------------

#### [【链表】linked-list-cycle-ii（环形链表 II）](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 `null`。

为了表示给定链表中的环，我们使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 `pos` 是 `-1`，则在该链表中没有环。

**说明：**不允许修改给定的链表。

**示例 1：**

```
输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。
```

![](http://upload-images.jianshu.io/upload_images/13065313-95a7d4681aecab46.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**示例 2：**

```
输入：head = [1,2], pos = 0
输出：tail connects to node index 0
解释：链表中有一个环，其尾部连接到第一个节点。
```

![](http://upload-images.jianshu.io/upload_images/13065313-0cfe0c4b0edbe375.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**示例 3：**

```输入：head = [1], pos = -1
输出：no cycle
解释：链表中没有环。
```

![](http://upload-images.jianshu.io/upload_images/13065313-018f26f441a37030.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**代码**

`双指针`

```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        boolean isCycle = false;
        ListNode a = head;//慢指针
        ListNode b = head;//快指针
        while(b != null && b.next != null){
            a = a.next;
            b = b.next.next;
            if(a == b){
                isCycle = true;
                break;
            }
        }
        if(isCycle){
            ListNode c = head;
            while(c != a){
                c = c.next;
                a = a.next;
            }
            return a;
        }else return null;
    }
}
```
`set判断重复`
```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        Set<ListNode> set = new HashSet<>();
        while(head != null){
            if(set.contains(head)) return head;
            set.add(head);
            head = head.next;
        }
        return null;
    }
}
```

-----------------

 #### [【链表】reverse-nodes-in-k-group（k个一组翻转链表）](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)

给出一个链表，每 k 个节点一组进行翻转，并返回翻转后的链表。
k 是一个正整数，它的值小于或等于链表的长度。如果节点总数不是 k 的整数倍，那么将最后剩余节点保持原有顺序。

```
示例 :
给定这个链表：1->2->3->4->5
当 k = 2 时，应当返回: 2->1->4->3->5
当 k = 3 时，应当返回: 3->2->1->4->5
```

**代码**

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode tmp = new ListNode(-1);
        ListNode pre = tmp;
        ListNode cur = pre;
        tmp.next = head;
        int num = 0;
        while(cur != null){
            cur = cur.next;
            num ++;
        }
        while(num > k){
            cur = pre.next;
            for(int i = 1; i < k; i ++){
                ListNode t = cur.next;
                cur.next = t.next;
                t.next = pre.next;
                pre.next = t;
            }
            pre = cur;
            num -= k;
        }
        return tmp.next;
        
    }
}
```

----------------

 #### [【栈】valid-parentheses（有效的括号）](https://leetcode-cn.com/problems/valid-parentheses/)

给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串，判断字符串是否有效。

有效字符串需满足：

1.  左括号必须用相同类型的右括号闭合。
2.  左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

**示例 1:**

```
输入: "()"
输出: true
```

**示例 2:**

```
输入: "()[]{}"
输出: true
```

**示例 3:**

```
输入: "(]"
输出: false
```
**示例 4:**

```
输入: "([)]"
输出: false
```

**示例 5:**

```
输入: "{[]}"
输出: true
```

**代码**

```
class Solution {
    public boolean isValid(String s) {
        Map<Character, Character> map = new HashMap<>();
        map.put(')', '(');
        map.put('}', '{');
        map.put(']', '[');
        Stack<Character> stack = new Stack<>();
        
        char[] arr = s.toCharArray();
        for(char c : arr){
            if(!map.containsKey(c)) stack.push(c);
            else if(stack.isEmpty() || map.get(c) != stack.pop()) return false;
        }
        return stack.isEmpty();
    }
}
```

----------------------

 #### [【队列&栈】implement-stack-using-queues（用队列实现栈）](https://leetcode-cn.com/problems/implement-stack-using-queues/)

使用队列实现栈的下列操作：
- push(x) -- 元素 x 入栈
- pop() -- 移除栈顶元素
- top() -- 获取栈顶元素
- empty() -- 返回栈是否为空

**代码**

```
class MyStack {

    Queue<Integer> q;
    /** Initialize your data structure here. */
    public MyStack() {
        q = new LinkedList<>();
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        q.offer(x);
        int n = q.size();
        for(int i = 0; i < n - 1; i ++){
            q.offer(q.poll());
        }
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        return q.poll();
    }
    
    /** Get the top element. */
    public int top() {
        return q.peek();
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return q.isEmpty();
    }
}
```

--------------------------------

 #### [【队列&栈】Implement Queue using Stacks（用栈实现队列）](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

使用栈实现队列的下列操作：
- push(x) -- 将一个元素放入队列的尾部。
- pop() -- 从队列首部移除元素。
- peek() -- 返回队列首部的元素。
- empty() -- 返回队列是否为空。

**代码**

```
class MyQueue {

    Stack<Integer> s1, s2;
    /** Initialize your data structure here. */
    public MyQueue() {
        s1 = new Stack<>();
        s2 = new Stack<>();
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        s1.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        if(!s2.isEmpty()) return s2.pop();
        else{
            while(!s1.isEmpty()){
                s2.push(s1.pop());
            }
            return s2.pop();
        }
    }
    
    /** Get the front element. */
    public int peek() {
        if(!s2.isEmpty()) return s2.peek();
        else{
            while(!s1.isEmpty()){
                s2.push(s1.pop());
            }
            return s2.peek();
        }
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return s1.isEmpty() && s2.isEmpty();
    }
}
```

---------------------

#### [【优先队列】kth-largest-element-in-a-stream（数据流中的第K大元素）](https://leetcode-cn.com/problems/kth-largest-element-in-a-stream/)

设计一个找到数据流中第K大元素的类（class）。注意是排序后的第K大元素，不是第K个不同的元素。

你的 `KthLargest `类需要一个同时接收整数` k` 和整数数组`nums `的构造器，它包含数据流中的初始元素。每次调用 `KthLargest.add`，返回当前数据流中第`K`大的元素。
```
示例:
int k = 3;
int[] arr = [4,5,8,2];
KthLargest kthLargest = new KthLargest(3, arr);
kthLargest.add(3);   // returns 4
kthLargest.add(5);   // returns 5
kthLargest.add(10);  // returns 5
kthLargest.add(9);   // returns 8
kthLargest.add(4);   // returns 8
```
说明: 
你可以假设 nums 的长度≥ k-1 且k ≥ 1。

**代码**

```
class KthLargest {

    PriorityQueue<Integer> q;
    int k;
    public KthLargest(int k, int[] nums) {
        this.k = k;
        q = new PriorityQueue<>();
        for(int i : nums) add(i);
    }
    
    public int add(int val) {
        if(q.size() < k) q.offer(val);
        else if(val > q.peek()){
            q.poll();
            q.offer(val);
        }
        return q.peek();
    }
}
```

--------------------------

#### [【优先队列】sliding-window-maximum（滑动窗口最大值）](https://leetcode-cn.com/problems/sliding-window-maximum/)

给定一个数组 *nums*，有一个大小为 *k* 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口 *k* 内的数字。滑动窗口每次只向右移动一位。

返回滑动窗口最大值。

**示例:**

```
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**注意：**

你可以假设 *k* 总是有效的，1 ≤ k ≤ 输入数组的大小，且输入数组不为空。

**代码**

`优先队列`

```
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums.length == 0) return new int[0];
        int[] res = new int[nums.length - k + 1];
        PriorityQueue<Integer> q = new PriorityQueue<>(k, Comparator.reverseOrder());
        for(int i = 0; i < k; i ++){
            q.offer(nums[i]);
        }
        res[0] = q.peek();
        int index = 1;
        for(int i = k; i < nums.length; i ++){
            q.remove(nums[index - 1]);
            q.offer(nums[i]);
            res[index++] = q.peek();
        }
        return res;
    }
}
```

`双端队列`

```
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums.length == 0) return new int[0];
        int[] res = new int[nums.length - k + 1];
        Deque<Integer> q = new LinkedList<>();
        int index = 0;
        for(int i = 0; i < nums.length; i ++){
            while(!q.isEmpty() && nums[q.peekLast()] <= nums[i]){
                q.pollLast();
            }
            q.offerLast(i);
            if(q.peek() == i - k) q.pollFirst();
            if(i >= k - 1) res[index ++] = nums[q.peek()];
        }
        return res;
    }
}
```

------

#### [【哈希】valid-anagram（有效的字母异位词）](https://leetcode-cn.com/problems/valid-anagram/)

给定两个字符串 *s* 和 *t* ，编写一个函数来判断 *t* 是否是 *s* 的一个字母异位词。

**示例 1:**

```
输入: s = "anagram", t = "nagaram"
输出: true
```

**示例 2:**

```
输入: s = "rat", t = "car"
输出: false
```

**说明:**
你可以假设字符串只包含小写字母。

**代码**

`hashmap`

```
class Solution {
    public boolean isAnagram(String s, String t) {
        Map<Character, Integer> sMap = new HashMap<>();
        Map<Character, Integer> tMap = new HashMap<>();
        char[] sC = s.toCharArray();
        char[] sT = t.toCharArray();
        for(char c : sC){
            sMap.put(c, sMap.getOrDefault(c, 0) + 1);
        }
        
        for(char c : sT){
            tMap.put(c, tMap.getOrDefault(c, 0) + 1);
        }
        return sMap.equals(tMap);
    }
}
```

`数组映射`

```
class Solution {
    public boolean isAnagram(String s, String t) {
        int[] a = new int[26];
        int[] b = new int[26];
        
        char[] sC = s.toCharArray();
        char[] tC = t.toCharArray();
        
        for(char c : sC){
            a[c - 'a'] += 1;
        }
        
        for(char c : tC){
            b[c - 'a'] += 1;
        }
        return Arrays.equals(a, b);
    }
}
```
------------------
#### [【哈希】two-sum（两数之和）](https://leetcode-cn.com/problems/two-sum/)

给定一个整数数组 `nums` 和一个目标值 `target`，请你在该数组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

**示例:**

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

**代码**

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i ++){
            if(map.containsKey(target - nums[i])) {
            	return new int[]{map.get(target - nums[i]), i};
            }
            map.put(nums[i], i);
        }
        return new int[2];
    }
}
```

------

#### [【哈希】3sum（三数之和）](https://leetcode-cn.com/problems/3sum/)

给定一个包含 *n* 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素 *a，b，c ，*使得 *a + b + c =* 0 ？找出所有满足条件且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

```
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

**代码**

`排序后枚举`

```
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        Set<List<Integer>> res = new HashSet<>();
        for(int i = 0; i < nums.length - 1; i ++){   
            if(i > 0 && nums[i] == nums[i - 1]) continue;
            Set<Integer> set = new HashSet<>();
            for(int j = i + 1; j < nums.length; j ++){
                if(!set.contains(nums[j])) set.add(-nums[i]-nums[j]);
                else {
                    res.add(Arrays.asList(nums[i], -nums[i] - nums[j], nums[j]));
                }
            }
        }
        return new ArrayList<>(res);
    }
}
```

`排序后使用双指针`

```
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        for(int i = 0; i < nums.length - 1; i ++){
            if(i > 0 && nums[i] == nums[i - 1]) continue; 
            int start = i + 1;
            int end = nums.length - 1;
            while(start < end){
                int sum = nums[i] + nums[start] + nums[end];
                if(sum > 0) end --;
                else if(sum < 0) start ++;
                else {
                    res.add(Arrays.asList(nums[i], nums[start], nums[end]));
                    //判重
                    while(start < end && nums[start] == nums[start + 1]) start ++;
                    while(start < end && nums[end] == nums[end - 1]) end --;
                    start ++;
                    end --;
                }
            }

        }
        return res;
    }
}
```

------

#### [【二叉树】validate-binary-search-tree（验证二叉搜索树）](https://leetcode-cn.com/problems/validate-binary-search-tree/)

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

- 节点的左子树只包含**小于**当前节点的数。
- 节点的右子树只包含**大于**当前节点的数。
- 所有左子树和右子树自身必须也是二叉搜索树。

**示例 1:**

```
输入:
    2
   / \
  1   3
输出: true
```

**示例 2:**

```
输入:
    5
   / \
  1   4
     / \
    3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
     根节点的值为 5 ，但是其右子节点值为 4 。
```

**代码**

`利用中序遍历的有序性`

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    
    List<Integer> list = new ArrayList<>();
    
    public boolean isValidBST(TreeNode root) {
        midOrder(root);
        if(list.size() == 0) return true;
        int tmp = list.get(0);
        for(int i = 1,length = list.size(); i < length; i ++){
            if(list.get(i) <= tmp){
                return false;
            }
            tmp = list.get(i);
        }
        return true;
    }
    
    public void midOrder(TreeNode root){
        if(root != null){
            midOrder(root.left);
            list.add(root.val);
            midOrder(root.right);
        }
    }
}
```

`递归`

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    TreeNode pre = null;
    public boolean isValidBST(TreeNode root) {
        if(root == null) return true;
        if(!isValidBST(root.left)) return false;
        if(pre != null && pre.val >= root.val) return false;
        pre = root;
        return isValidBST(root.right);
    }
    
}
```

-----------------------------------

#### [【二叉树】lowest-common-ancestor-of-a-binary-search-tree（二叉搜索树的最近公共祖先）](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

[百度百科](https://baike.baidu.com/item/最近公共祖先/8918834?fr=aladdin)中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（**一个节点也可以是它自己的祖先**）。”

例如，给定如下二叉搜索树:  root = [6,2,8,0,4,7,9,null,null,3,5]

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/binarysearchtree_improved.png)

 

**代码**

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        while(root != null){
            if(p.val > root.val && q.val > root.val) root = root.right;
            else if(p.val < root.val && q.val < root.val) root = root.left;
            else return root;
        }    
        return null;
    }
}
```

------------------

#### [【递归&分治】Pow(x, n)](https://leetcode-cn.com/problems/powx-n/)

实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 x 的 n 次幂函数。

**示例 1:**

```
输入: 2.00000, 10
输出: 1024.00000
```

**示例 2:**

```
输入: 2.10000, 3
输出: 9.26100
```

**示例 3:**

```
输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
```

**说明:**

- -100.0 < *x* < 100.0
- *n* 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。

**代码**

```
class Solution {
    public double myPow(double x, int n) {
        if(n < 0) return 1.0 / helper(x, -n);
        return helper(x, n);
    }
    
    public double helper(double x, int n){
        if(n == 0) return 1;
        double v = helper(x, n / 2);
        if(n % 2 == 0){
            return v * v;
        } else {
            return v * v * x;
        }
    }
}
```

----------------------

#### [【计数】majority-element（求众数）](https://leetcode-cn.com/problems/majority-element/)

给定一个大小为 *n* 的数组，找到其中的众数。众数是指在数组中出现次数**大于** `⌊ n/2 ⌋` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在众数。

**示例 1:**

```
输入: [3,2,3]
输出: 3
```

**示例 2:**

```
输入: [2,2,1,1,1,2,2]
输出: 2
```

**代码**

`利用map计数`

```
class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0, length = nums.length; i < length; i ++){
            if(map.containsKey(nums[i])){
                map.put(nums[i], map.get(nums[i]) + 1);
            }else{
                map.put(nums[i], 1);
            }
        }
        Set<Integer> set = map.keySet();
        for(Integer key : set){
            if(map.get(key) > nums.length/2) return key;
        }
        return 0;
    }
}
```

`排序计数`

```
class Solution {
    public int majorityElement(int[] nums) {
        if(nums.length == 1) return nums[0];
        Arrays.sort(nums);
        int count = 1;
        for(int i = 1; i < nums.length; i ++){
            if(nums[i] == nums[i-1]){
                count ++;
            } else count = 1; 
            if(count > nums.length / 2) return nums[i];
        }
        return 0;
    }
}
```

--------------

#### [【贪心】best-time-to-buy-and-sell-stock-ii（买卖股票的最佳时机 II）](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

给定一个数组，它的第 *i* 个元素是一支给定股票第 *i* 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

**注意：**你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

**示例 1:**

```
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
```

**示例 2:**

```
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```

**示例 3:**

```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

**代码**

```
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0) return 0;
        int cur = prices[0];
        int length = prices.length;
        int res = 0;
        for(int i = 0; i < length; i ++){
            if(prices[i] > cur){
                res += (prices[i] - cur);
                cur = prices[i];
            }else{
                cur = prices[i];
            }
        }   
        return res;
    }
}
```

-------------------------------

#### 【BFS】 广度优先搜索 （伪码）

```
BFS()
{
  输入起始点；
  初始化所有顶点标记为未遍历；
  初始化一个队列queue并将起始点放入队列；

  while（queue不为空）
  {
    从队列中删除一个顶点s并标记为已遍历； 
    将s邻接的所有还没遍历的点加入队列；
  }
}
```

-----------------------------------

#### 【DFS】 深度优先搜索（伪码）

```
DFS（顶点v）
{
  标记v为已遍历；
  for（对于每一个邻接v且未标记遍历的点u）
      DFS（u）;
}
```

----------------------

#### [【BFS】binary-tree-level-order-traversal（二叉树的层次遍历）](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
]
```

**代码**

`bfs`

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        if(root == null) return new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> result = new ArrayList<>();
        queue.offer(root);
        while (!queue.isEmpty()){
            List<Integer> node = new ArrayList<>();
            int length = queue.size();
            while (length > 0){
                TreeNode tree = queue.poll();
                if(tree.left != null){
                    queue.offer(tree.left);
                }
                if(tree.right != null){
                    queue.offer(tree.right);
                }
                node.add(tree.val);
                length --;
            }            
            result.add(node);
        }      
        return result;
    }
}
```

`也可以用dfs`

```
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        if(root == null) return new ArrayList<>();
        List<List<Integer>> res = new ArrayList<>();
        _dfs(res, root, 0);
        return res;
    }
    
    public void _dfs(List<List<Integer>> list, TreeNode node, int level){
        if(node == null) return;
        if(list.size() < level + 1){
            list.add(new ArrayList<>());
        }
        list.get(level).add(node.val);
        _dfs(list, node.left, level + 1);
        _dfs(list, node.right, level + 1);
    }
}
```

-----------------

#### [【DFS】maximum-depth-of-binary-tree（二叉树的最大深度）](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明:** 叶子节点是指没有子节点的节点。

**示例：**
给定二叉树 `[3,9,20,null,null,15,7]`，

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。

**代码**

`DFS`

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int maxDepth(TreeNode root) {
        return root == null ? 0 : Math.max(maxDepth(root.left),maxDepth(root.right)) + 1; 
    }
}
```

`BFS`

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null) return 0;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        int count = 1;
        while(!q.isEmpty()){
            int length = q.size();
            boolean flag = false;
            for(int i = 0; i < length; i ++){
                TreeNode node = q.poll();
                if(node.left != null || node.right != null) flag = true;
                if(node.left != null) q.offer(node.left);
                if(node.right != null) q.offer(node.right);
            }
            if(flag) count ++;
        }
        return count;
    }
}
```

----------------------

#### [【DFS】minimum-depth-of-binary-tree（二叉树的最小深度）](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**

给定二叉树 `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最小深度  2.

**代码**

`BFS`

```
class Solution {
    public int minDepth(TreeNode root) {
        if(root == null) return 0;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        int count = 1;
        while(!q.isEmpty()){
            int length = q.size();
            boolean flag = false;
            for(int i = 0; i < length; i ++){
                TreeNode node = q.poll();
                if(node.left == null && node.right == null) return count;
                if(node.left != null || node.right != null) flag = true;
                if(node.left != null) q.offer(node.left);
                if(node.right != null) q.offer(node.right);
            }
            if(flag) count ++;
        }
        return count;
    }
}
```

`DFS`

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int minDepth(TreeNode root) {
        if(null == root) return 0;
        if(null == root.left) return minDepth(root.right) + 1;
        if(null == root.right) return minDepth(root.left) + 1;
        return Math.min(minDepth(root.left),minDepth(root.right)) + 1;     
    }
}
```

--------------------

