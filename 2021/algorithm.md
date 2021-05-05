# 算法

## 精通一个领域

* Chunk it up (切碎知识点)
* Deliberate practicing (刻意练习)
* Feedback (反馈)

## 树

二叉搜索树(英语: Binary Search Tree) ，也称二叉搜索树、有
序二叉树(英语: ordered binary tree),
排序二叉树
(英语:sorted binary tree) ,
是指一棵空树或者具有下列性质的二叉树

1.左子树上所有结点的值均小于它的根结点的值;
2.右子树.上所有结点的值均大于它的根结点的值;
3. Recursively,左、右子树也分别为二叉查找树。


### 遍历
1.Pre-order 
2.In-order
3.Post-order 





## 数据结构

Data Structure
Array
Stack / Queue
PriorityQueue (heap)
LinkedList (single / double)
Tree / Binary Tree
Binary Search Tree
HashTable
Disjoint Set
Trie
BloomFilter
LRU Cache

Redis 为什么使用skiplist?

1 skiplist的复杂度和红黑树一样，而且实现起来更简单。
2 在并发环境下skiplist有另外一个优势，红黑树在插入和删除的时候可能需要做一些rebalance的操作，
这样的操作可能会涉及到整个树的其他部分，商skiplist的操作 显然更加局部性一些，锁需要盯住的节点更少，因此在这样的情况下性能好一些。


## 算法

Algorithm

General Coding
In-order/Pre-order/Post-order traversal
Greedy
Recursion/Backtrace
Breadth-first search
Depth-first search
Divide and Conquer
Dynamic Programming
Binary Search
Graph


### Big O notation
O(1): Constant Complexity: Constant常数复杂度
O(log n): Logarithmic Complexity:对数复杂度
O(n): Linear Complexity:线性时间复杂度
O(n^2): N square Complexity平方
O(n^3): N square Complexity立方
O(2^n): Exponential Growth指数
O(n!): Factorial阶乘
注意:只看最高复杂度的运算


|Algorithm| Run time|
|:--:|:--:|
|Binary search |O(log n)|
|Binary tree traversal |O(n)|
|Optimal sorted matrix search |O(n)|
|Merge sort | O(n log n)|



## 贪心Greedy

贪心法，又称贪心算法、贪婪算法:在对问题求解时，总是做出在当前看来是最好的选择。


### 适用Greedy的场景

简单地说,(问题能够分解成子问题来解决，子问题的最优解能递推到最终问题的最优解。这种子问题最优解成为最优子结构。

贪心算法与动态规划的不同在于它对每个子问题的解决方案都做出选择，不能回退。动态规划则会保存以前的运算结果，并根据以前的结果对当前进行选择,有回退功能。


https:/leetcode.com/problemset/all/


### 二分查找

1. Sorted (单 调递增或者递减)
2. Bounded (存在上下界)
3. Accessible by index ( 能够通过索引访问)

## 字典树

1. Trie树的数据结构

Trie树,即字典树，又称单词查找树或键树，是一种树形结构，是一种哈希树的变种。
典型应用是用于统计和排序大量的字符串(但不仅限于字符串)
所以经常被搜索引擎系统用于文本词频统计。
它的优点是:最大限度地减少无谓的字符串比较,查询效率比哈希表高。


2. Trie树的核心思想

Trie的核心思想是空间换时间。利用字符串的公共前缀来降低查询时间的开销以达到提高效率的目的。

3. Trie树的基本性质

1.根节点不包含字符，除根节点外每一个节点都只包含一个字符。
2.从根节点到某一节点，路径上经过的字符连接起来，为该节点对应的字符串。
3.每个节点的所有子节点包含的字符都不相同。

## 位运算

1.位运算介绍
程序中的所有数在计算机内存中都是以二进制的形式储存的。
位运算说穿了，就是直接对整数在内存中的二进制位进行操作。
比如，and运算本来是一个逻辑运算符，但整数与整数之间也可以进行and运算。

2.位运算常用操作

|符号|说明|含义|
|:--:|:--:|:--:|
|& |与| |
|`|`| 或||
|^ |异或|两个位相同为0，相异为1|
|~ |取反||
|<< |左移|各二进位全部左移若干位，高位丢弃，低位补0|
|>> |右移| 各二进位全部右移若干位，对无符号数，高位补0，有符号数，各编译器处理方法不一样，有的补符号位(算术右移)有的补0 (逻辑右移)|

3.位运算的应用

X&1==1 OR==0判断奇偶(x%2==1)
X=X&(X-1)=>清零最低位的1
X&-X=>得到最低位的1


## 动态规划(Dynamic Programming)

1.递归+记忆化->递推
2.状态的定义: opt[n], dp[n], fib[n]
3.状态转移方程: opt[n] = best_of(opt[n-1], opt[n-2], ..)
4.最优子结构

### DP VS回溯 VS 贪心

回溯(递归) 重复计算

贪心 永远局部最优

DP 记录局部最优子结构/多种记录值

## 并查集

并查集(union & find)是一种树型的数据结构，用于处理一些不交集(Disjoint Sets)的合并及查询问题。

Find:确定元素属于哪一个子集。它可以被用来确定两个元素是否属于同一子集。

Union:将两个子集合并成同一个集合。


## LRU Cache

LRU Cache
1. Least recently used (最近最少使用)
2. Double L inkedL ist
3. O(1)查询
4. O(1)修改、更新


LFU Cache

1. LFU - least frequently used (最近最不常用页面置换算法)
2. LRU - least recently usd ( 最近最少使用页面置换算法)

https://en.wikipedia.org/wiki/Cache_replacement_policies

## Bloom Filter (布隆过滤器)

一个很长的二进制向量和一个映射函数。

布隆过滤器可以用于检索一个元素是否在一个集合中。

它的优点是空间效率和查询时间都远远超过一般的算法，缺点是有一定的误识别率和删除困难。


## 面试答题四件套

1. Clarification (询问题目细节、边界条件、可能的极端错误情况)

2. Possible Solution (所有可能的解法都和面试官沟通一遍)

Compare Time & Space Complexity (时间复杂度&空间复杂度)

Optimal Solution (最优解)

3. Coding (写代码)

4. Test Cases (测试用例)

## 斐波那契数列
(1) 斐波那契数列求解，如果用直接法，时间复杂度是指数级的，不可行;
(2) 多深入理解递归，否则容易把自己玩死;
