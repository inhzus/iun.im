---
title: 2019年后端实习生面试记录
date: 2019-04-24 21:26:11
tags: [Interview]
mathjax: true
hide: true
---

以下记录一下 2019 年国内某大厂后端实习生面试.

### 一面

- 介绍 TCP:

  传输层, 特点, 与 UDP 区别, 三次握手, 四次挥手.

- 四次挥手中 TIME_WAIT 和 CLOSE_WAIT 区别:

  具体说明 TIME_WAIT 和 CLOST_WAIT 的过程.

- 抛第 2k+1 次硬币正面朝上的概率, 抛 2k+1 次硬币正面朝上的概率, 并解释:

  1/2. 独立事件; 计算事件概率即得.

<!--more-->

- n 个数能构造几个 BST 树, 写出代码:
  
  转化为递归问题, 递归式如下:

$$
f(n) = \begin{cases}
0, n <= 1 \\
sum\{f(i) * f(n - 1 - i)| i = 0,1,\cdots,n\}, n > 1
\end{cases}
$$

- 实现程序: 两个链表相加, 如 1->5->9 + 3 ->2 = 1->9->1:

  翻转两个列表, 逐位相加并进位. 直至两个链表都遍历结束且进位值为0.

### 二面

- 实现程序: 找出一串字符串中最大的数字, 以字符串返回, 若为 000, 返回 "0", 若无数字, 返回 ""(这个数字可能非常大):

  从前往后遍历, 记录每个新的字符串, 并和之前最大的比较即可, 关键在于注意细节.

- 了解 LRU cache 吗? 不了解. 了解 cache 吗? 实现一个 HashMap:

  代码实现 HashMap, get(k), push(k, v). 构造函数, 拷贝构造, 析构函数.

- 基于上述代码, 如何实现一个带有过期时间的 cache:

  联系了一下最近用 Python 写的一个需要过期时间的 cache, 使用弱引用的 Pair, 每次 put 压入最小堆, 逐个检查堆顶是否过期并逐个 pop, 此时引用次数为 0, 自然会被销毁空间.

  C++ 实现: 在 Pair 数据结构中加入 expireTime 变量, 在 put 时将 Pair 的指针同时压入以 expireTime 为比较函数的最小堆, 在 put 与 get 时检查最小堆的堆顶, 超时 pop.

- 基于 HashMap, 如何实现一个最近最少使用的 cache:

  思考了一下栈和最小堆, 最后发现队列用在此最合适.

  雏形: 维护一个队列, put 时将 Pair 的指针压入队首. get 时查队列, 查到则删除, 然后将 get 的 Pair 重新压入队首.

- 每次 get 时查队列的时间复杂度太高, 系统地重新阐述一遍:

  队列的实现为 std::list, Pair 中添加一个指向队列中变量的指针. put 时,向队首压入 Pair 指针, 并将 Pair 中的指针指向这一位置. get 时, 将在 HashMap 中查到的 Pair 中指向的位置销毁, 重新将指针 push 到队首. 当需要从 cache 中舍弃一些 Pair 时, 销毁队尾指向的地址并 pop.

二面让我对这个面试官的印象非常好, 其实最后他让我实现的这个东西也就是 LRU cache.

### 三面

HR 面比较轻松, 问了: 你还在面哪些公司, 如果有多个 offer 你怎么选择; 你对部门有什么了解; 你实习的时间安排等等. 最后通知一周内答复.

希望可以过.
