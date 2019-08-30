1．滑动窗口

- [滑动窗口的最大值（剑指offer）](https://www.nowcoder.com/practice/1624bc35a45c42c0bc17d17fa0cba788?tpId=13&tqId=11217&tPage=4&rp=4&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
- [滑动窗口中位数（LEETCODE）](https://leetcode-cn.com/problems/sliding-window-median/)
- [最小覆盖子串（LEETCODE）](https://leetcode-cn.com/problems/minimum-window-substring/)
- [K 个不同整数的子数组（LEETCODE）](https://leetcode-cn.com/problems/subarrays-with-k-different-integers/)

2．二指针或迭代器

- N-sum问题（LEETCODE）
- [无重复字符的最长自创（LEETCODE）](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)
- [接雨水（LEETCODE）](https://leetcode-cn.com/problems/trapping-rain-water/)
- [长度最小的子数组（LEETCODE）](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)

3．快速和慢速指针或迭代器

- [环形链表（LEETCODE）](https://leetcode-cn.com/problems/linked-list-cycle/)
- [相交链表（LEETCODE）](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)
- [环形链表入口节点（LEETCODE）](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

4．合并区间

- [合并区间（LEETCODE）](https://leetcode-cn.com/problems/merge-intervals/)
- [会议室（LEETCODE）](https://leetcode-cn.com/problems/meeting-rooms-ii/)
- [Range模块（LEETCODE）](https://leetcode-cn.com/problems/range-module/)
- [区间列表的交集（LEETCODE）](https://leetcode-cn.com/problems/interval-list-intersections/)

5．循环排序

- [缺失数字（LEETCODE）](https://leetcode-cn.com/problems/missing-number/)
- [寻找重复数（LEETCODE）](https://leetcode-cn.com/problems/find-the-duplicate-number/)
- [缺失的第一个正数（LEETCODE）](https://leetcode-cn.com/problems/first-missing-positive/)

6．原地反转链表

- [反转链表（LEETCODE）](https://leetcode-cn.com/problems/reverse-linked-list/)
- [反转链表II（LEETCODE）](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

7．树的宽度优先搜索（Tree BFS）

- [N叉树的层序遍历（LEETCODE）](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)
- [二叉树的层序遍历（LEETCODE）](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)
- [二叉树的锯齿形层次遍历](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)

8．树的深度优先搜索（Tree DFS）

- [求根到叶子节点数字之和（LEETCODE）](https://leetcode-cn.com/problems/sum-root-to-leaf-numbers/)
- [二叉树的最大深度（LEETCODE）](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)
- [从中序与后序遍历序列构造二叉树（LEETCODE）](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)
- [路径总和系列（LEETCODE）](https://leetcode-cn.com/problems/path-sum/)

9．Two Heaps

- [数据流的中位数（LEETCODE）](https://leetcode-cn.com/problems/find-median-from-data-stream/)
- [滑动窗口的最大值（剑指offer）](https://www.nowcoder.com/practice/1624bc35a45c42c0bc17d17fa0cba788?tpId=13&tqId=11217&tPage=4&rp=4&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

10．子集

- [子集系列（LEETCODE）](https://leetcode-cn.com/problems/subsets/)
- [字母大小写全排列（LEETCODE）](https://leetcode-cn.com/problems/letter-case-permutation/)
- [列举单词的全部缩写（LEETCODE）](https://leetcode-cn.com/problems/generalized-abbreviation/)
- [单词子集（LEETCODE）](https://leetcode-cn.com/problems/word-subsets/)

11．经过修改的二叉搜索

- [搜索旋转排序数组（LEETCODE）](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)
- [寻找两个有序数组的中位数（LEETCODE）](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)
- [寻找旋转排序数组中的最小值（LEETCODE）](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

12． 前 K 个元素

- [合并两个有序链表（LEETCODE）](https://leetcode-cn.com/problems/merge-two-sorted-lists/)
- [合并K个排序链表（LEETCODE）](https://leetcode-cn.com/problems/merge-k-sorted-lists/)
- [丑数系列（LEETCODE）](https://leetcode-cn.com/problems/ugly-number-ii/)

13． K 路合并

- [合并两个有序链表（LEETCODE）](https://leetcode-cn.com/problems/merge-two-sorted-lists/)
- [合并K个排序链表（LEETCODE）](https://leetcode-cn.com/problems/merge-k-sorted-lists/)
- [丑数系列（LEETCODE）](https://leetcode-cn.com/problems/ugly-number-ii/)

14．拓扑排序

- [课程表系列（LEETCODE）](https://leetcode-cn.com/problems/course-schedule/)
- [矩阵中的最长递增路径（LEETCODE）](https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix/)
- [序列重建（LEETCODE）](https://leetcode-cn.com/problems/sequence-reconstruction/)















### [滑动窗口的最大值](https://www.nowcoder.com/practice/1624bc35a45c42c0bc17d17fa0cba788?tpId=13&tqId=11217&tPage=4&rp=4&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

``` java
import java.util.ArrayList;
import java.util.LinkedList;

public class Solution {
    public ArrayList<Integer> maxInWindows(int[] num, int size) {
        ArrayList<Integer> res = new ArrayList<>();
        if (num == null || num.length < size || size <= 0) {
            return res;
        }
        LinkedList<Integer> deque = new LinkedList<>();
        for (int i = 0; i < num.length; i++) {
            // 窗口内存储num的下标，保持数据是递减的
            while (!deque.isEmpty() && num[i] > num[deque.peekLast()]) {
                deque.removeLast();
            }
            // 超过窗口大小时，移除队首元素
            if (!deque.isEmpty() && i - deque.peekFirst() == size) {
                deque.removeFirst();
            }
            deque.addLast(i);
            if (i + 1 >= size) {
                res.add(num[deque.peekFirst()]);
            }
        }
        return res;
    }
}
```



