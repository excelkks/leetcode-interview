# LeetCode 精选TOP面试题

[原题链接](https://leetcode-cn.com/problemset/algorithms/?listId=2ckc81c)

[TOC]

## 1. 两数之和

难度：♦️

[链接🔗](https://leetcode-cn.com/problems/two-sum/)

给定一个整数数组`nums`和一个整数目标值`target`，请你在该数组中找出和为目标值的那两个整数，并返回它们的数组下标。你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。你可以按任意顺序返回答案。

示例

```c++
1.
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。

2.
输入：nums = [3,2,4], target = 6
输出：[1,2]

3.  
输入：nums = [3,3], target = 6
输出：[0,1]
```

### 暴力求解

略

### 哈希表法

将输入的数组放入hash表中，再看target与当前索引值的差是否在哈希表中

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int, int> hashTable;
        vector<int> sumIndex;
        for(int i = 0; i < nums.size(); ++i)
            hashTable[nums[i]] = i;
        for(int j = 0; j < nums.size(); ++j)
            if(hashTable.count(target - nums[j]) != 0 && 
                hashTable[target-nums[j]] != j){
                    sumIndex.push_back(j);
                    sumIndex.push_back(hashTable[target - nums[j]]);
                    break;
                }
        return sum_index;
    }
}
```

### 哈希表优化法

把target减当前索引值的差放入hash表中，如果当前值在hash表中，那么求解成功

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int, int> hashTable;
        vector<int> sumIndex;
        for(int i = 0; i < nums.size(); ++i){
            if(hashTable.count(nums[i]) != 0){
                sumIndex.push_back(hashTable[nums[i]]);
                sumIndex.push_back(i);
                break;
            }
            hashTable[target-nums[i]] = i;
        }
        return sumIndex;
    }
}
```

## 2. 两数相加

难度：♦️♦️

[链接🔗](https://leetcode-cn.com/problems/add-two-numbers/)

给你两个**非空**的链表，表示两个非负的整数。它们每位数字都是按照**逆序**的方式存储的，并且每个节点只能存储**一位**数字。请你将两个数相加，并以相同形式返回一个表示和的链表。你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例

```c++
1.
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
  
2.
输入：l1 = [0], l2 = [0]
输出：[0]
  
3.
输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出：[8,9,9,9,0,0,0,1]
```

需要注意第一位的计算

```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *head = nullptr, *tail = nullptr;
        int carry = 0;
        while (l1 || l2) {
            int n1 = l1 ? l1->val: 0;
            int n2 = l2 ? l2->val: 0;
            int sum = n1 + n2 + carry;
            if (!head) {
                head = tail = new ListNode(sum % 10);
            } else {
                tail->next = new ListNode(sum % 10);
                tail = tail->next;
            }
            carry = sum / 10;
            if (l1) {
                l1 = l1->next;
            }
            if (l2) {
                l2 = l2->next;
            }
        }
        if (carry > 0) {
            tail->next = new ListNode(carry);
        }
        return head;
    }
};
```

