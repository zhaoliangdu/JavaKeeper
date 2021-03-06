

http://netedu.xauat.edu.cn/jpkc/netedu/jpkc/ycx/kcjy/kejian/pdf/05.pdf

https://leetcode-cn.com/circle/article/lxC3ZB/

https://labuladong.gitbook.io/algo/dong-tai-gui-hua-xi-lie/dong-tai-gui-hua-xiang-jie-jin-jie

https://www.zhihu.com/question/39948290

https://zhuanlan.zhihu.com/p/26743197



## 前言

为了面试，不，为了生活，我重拾算法有一段时间了，但是每次都把动态规划放在了后边，因为这个大名鼎鼎的名字，听着就感觉很牛逼，很难学的样子。

> **动态规划**（英语：Dynamic programming，简称DP）是运筹学的一个分支，是求解决策过程(decision process)最优化的数学方法。20 世纪 50 年代初美国数学家 R.E.Bellman 等人在研究多阶段决策过程(multistep decision process) 的优化问题时，提出了著名的最优化原理 (principle of optimality)，把多阶段过程转化为一系列单阶段问题，逐个求解，创立了解决这类过程优化问题的新方法——动态规划。1957 年出版了他的名著 Dynamic Programming，这是该领域的第一本著作。
>
> 动态规划问世以来，在经济管理、生产调度、工程技术和最优控制等方面得到了广泛的应用。例如最短路线、库存管理、资源分配、设备更新、排序、装载等问题，用动态规划方法比用其它方法求解更为方便。
>
> 虽然动态规划主要用于求解以时间划分阶段的动态过程的优化问题，但是一些与时间无关的静态规划(如线性规划、非线性规划)，只要人为地引进时间因素，把它视为多阶段决策过程，也可以用动态规划方法方便地求解。
>
> 
>
> 通常许多子问题非常相似，为此动态规划法试图仅仅解决每个子问题一次，具有天然剪枝的功能，从而减少计算量：一旦某个给定子问题的解已经算出，则将其记忆化存储，以便下次需要同一个子问题解之时直接查表。这种做法在重复子问题的数目关于输入的规模呈指数增长时特别有用。
>
> 动态规划在查找有很多**重叠子问题**的情况的最优解时有效。它将问题重新组合成子问题。为了避免多次解决这些子问题，它们的结果都逐渐被计算并被保存，从简单的问题直到整个问题都被解决。因此，动态规划保存[递归](https://zh.wikipedia.org/wiki/递归)时的结果，因而不会在解决同样的问题时花费时间。
>
> 动态规划只能应用于有**最优子结构**的问题。最优子结构的意思是局部最优解能决定全局最优解（对有些问题这个要求并不能完全满足，故有时需要引入一定的近似）。简单地说，问题能够分解成子问题来解决。

看完之后，我说了一句脏话，然后就开始找技术博客了。



## 写在前面

计算机归根结底只会做一件事：穷举。

所有的算法都是在让计算机【如何聪明地穷举】而已，动态规划也是如此。

本文将会从以下角度来讲解动态规划：

- 什么是动态规划
- 动态规划从入门到进阶
- 再谈动态规划



## 动态规划是什么

动态规划(dynamic programming)是运筹学的一个分支，是解决<mark>**「多阶段决策」**</mark>过程最优化的一种数学方法。

**一般用来求最值问题**，多数情况下它可以采用<mark>**「自下而上」**</mark>的递推方式来得出每个子问题的最优解（即<mark>**「最优子结构」**</mark>），进而自然而然地得出依赖子问题的原问题的最优解。

有几个比较眼生的概念，我们看下：

- **多阶段决策**：比如说我们有一个复杂的问题要处理，我们可以按问题的时间或从空间关系分解成几个互相联系的阶段，使每个阶段的决策问题都是一个比较容易求解的“**子问题**”，这样依次做完每个阶段的最优决策后，他们就构成了整个问题的最优决策。简单地说，就是每做一次决策就可以得到解的一部分，当所有决策做完之后，完整的解就“浮出水面”了。有一种大事化小，小事化了的感觉。

- **最优子结构**：在我们拆成一个个子问题的时候，每个子问题一定都有一个最优解，既然它分解的子问题是全局最优解，那么依赖于它们解的原问题自然也是全局最优解。比如说，你的原问题是考出最高的总成绩，那么你的子问题就是要把语文考到最高，数学考到最高…… 为了每门课考到最高，你要把每门课相应的选择题分数拿到最高，填空题分数拿到最高…… 当然，最终就是你每门课都是满分，这就是最高的总成绩。

- **自下而上**：或者叫自底向上，对应的肯定有自上而下（自顶向下）

  - 啥叫**自顶向下**，比如我们求解递归问题，画递归树的时候，是从上向下延伸，都是从一个规模较大的原问题比如说 f(20)，向下逐渐分解规模，直到 f(1) 和 f(2) 触底，然后逐层返回答案，这就叫「自顶向下」，比如我们用递归法计算斐波那契数列的时候

    ![](https://pic.leetcode-cn.com/25e913ab8d7a22bb017669e4a097cf51d10861f365002f2d8556ee7a64464cd8-Picture0.png)

    ![](https://github.com/labuladong/fucking-algorithm/raw/master/pictures/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E8%AF%A6%E8%A7%A3%E8%BF%9B%E9%98%B6/2.jpg)

  - 反过来，自底向上，肯定就是从最底下，最简单，问题规模最小的 f(1) 和 f(2) 开始往上推，直到推到我们想要的答案 f(20)，这就是动态规划的思路，这也是为什么动态规划一般都脱离了递归，而是由循环迭代完成计算。

    ![img](https://github.com/labuladong/fucking-algorithm/raw/master/pictures/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E8%AF%A6%E8%A7%A3%E8%BF%9B%E9%98%B6/4.jpg)



从递归树中我们可以看到，自顶向下的递归算法，我们会求两次 f(18)，三次 f(17)，，，这就存在了大量的**「重叠子问题」**，这样暴力穷举的话效率会极其低下，所以需要「备忘录」或者「DP table」来优化穷举过程，避免不必要的计算。

怎样才能自下而上的求出每个子问题的最优解呢，可以肯定子问题之间是有一定联系的，即迭代递推公式，也叫<mark>「**状态转移方程**」</mark>，实际上就是描述问题结构的数学形式。

> 动态规划中当前的状态往往依赖于前一阶段的状态和前一阶段的决策结果。例如我们知道了第 i 个阶段的状态Si 以及决策 Ui，那么第 i+1 阶段的状态 Si+1 也就确定了。所以解决动态规划问题的关键就是确定状态转移方程，一旦状态转移方程确定了，那么我们就可以根据方程式进行编码。

以上提到的**重叠子问题、最优子结构、状态转移方程就是动态规划三要素**。



## 斐波那契数列

PS：我们先从一个简单的斐波那契数列来进一步理解下重叠子问题与状态转移方程（斐波那契数列并不是严格意义上的动态规划，因为它没有求最值，所以也没设计到最优子结构的问题）

**1、暴力递归**

斐波那契数列的数学形式就是递归的，写成代码就是这样：

```java
int fib(int N) {
    if (N == 1 || N == 2) return 1;
    return fib(N - 1) + fib(N - 2);
}
```

这个不用多说了，我们在 **自顶向下** 那部分画出的就是它的递归树，他有大量的重复计算问题，比如 `f(18)` 被计算了两次，而且你可以看到，以 `f(18)` 为根的这个递归树体量巨大，多算一遍，会耗费巨大的时间。更何况，还不止 `f(18)` 这一个节点被重复计算，所以这个算法及其低效。

![](https://github.com/labuladong/fucking-algorithm/raw/master/pictures/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E8%AF%A6%E8%A7%A3%E8%BF%9B%E9%98%B6/1.jpg)

这就是动态规划问题的第一个性质：**重叠子问题**。下面，我们想办法解决这个问题。

**2、带备忘录的递归解法**

明确了问题，其实就已经把问题解决了一半。即然耗时的原因是重复计算，那么我们可以造一个「备忘录」，每次算出某个子问题的答案后别急着返回，先记到「备忘录」里再返回；每次遇到一个子问题先去「备忘录」里查一查，如果发现之前已经解决过这个问题了，直接把答案拿出来用，不要再耗时去计算了。

一般使用一个数组充当这个「备忘录」，当然也可以使用哈希表（字典），思想都是一样的，也有人叫 **记忆化递归法**，备忘录其实就是一个缓存的思想。

```java
public static int fib(int n) {
    if (n == 1 || n == 2) {
        return 1;
    }
    //用一个数组充当备忘录，保存记录
    int[] dp = new int[n + 1];
    //初始值
    dp[0] = 0;
    dp[1] = 1;
    for(int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}
// 用 hash 表当备忘录
public int fib(int n) {
    if (n == 1 || n == 2) {
        return 1;
    }
    if (hashMap.containsKey(n)) {
        return hashMap.get(n);
    } else {
        int result = fib(n - 1) + fib(n - 2);
        hashMap.put(n,result);
        return result;
    }
}
```

带「备忘录」的递归算法，把一棵存在巨量冗余的递归树通过<mark>「**剪枝」**</mark>，改造成了一幅不存在冗余的递归图，极大减少了子问题（即递归图中节点）的个数。

![img](https://pic.leetcode-cn.com/e541109bc2125cfb78df53bd8f7a03a1d9707e258a7c1a5347ea6161b15c7286-file_1582002158301)

![](https://github.com/labuladong/fucking-algorithm/raw/master/pictures/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E8%AF%A6%E8%A7%A3%E8%BF%9B%E9%98%B6/3.jpg)

**3、动态规划解法**

有了上一步「备忘录」的启发，**自顶向下**的递推，每次“缓存”之前的结果，那**自底向上**的推算不也可以吗？而且推算的时候，我们只需要存储之前的两个状态就行，还省了很多空间，我靠，真是个天才，这就是，**动态规划**的做法。

![](https://github.com/labuladong/fucking-algorithm/raw/master/pictures/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E8%AF%A6%E8%A7%A3%E8%BF%9B%E9%98%B6/4.jpg)

画个图就很好理解了，我们一层一层的往上计算，得到最后的结果。

斐波那契数列的定义其实就是个**状态转移方程**：$f(n) = f(n-1) + f(n-2)$，$f(n)$ 就是子问题的状态，这个状态是由  $f(n-1)$ 和  $f(n-2)$ 这两个状态相加转移过来的，这就是状态转移。是不又有点理解了？

最难的状态转移方程有了，看下代码，定义三个变量循环迭代完成计算，搞定

```java
public int fib(int n) {
    if (n == 1 || n == 2) {
        return 1;
    }
    int result = 0, pre = 1, next = 2;
    for (int i = 3; i < n + 1; i++) {
        result = pre + next;
        pre = next;
        next = result;
    }
    return result;
}
```

有没有发现，这个状态转移方程的写法，和暴力破解有着千丝万缕的联系。其实状态转移方程直接代表着暴力解法。



## 什么样的题目适合用动态规划

可以使用动态规划的问题一般都有一些特点可以遵循。如题目的问法一般是三种方式：

1. 求最大值/最小值

2. 求可不可行

3. 求方案总数

如果你碰到一个问题，是问你这三个问题之一的，那么有 90% 的概率是可以使用动态规划来求解。



## 套路解题

动态规划是用大白话说就是一个算法范例，通过将其分解为子问题来解决给定的复杂问题，并存储子问题的结果，以避免再次计算相同的结果。

我们知道了动态规划三要素：重叠子问题、最优子结构、状态转移方程。

那要解决一个动态规划问题的大概步骤，应该也挺明确了：

1. **划分阶段：**按照问题的时间或空间特征，把问题分为若干个阶段。注意这若干个阶段一定要是有序的或者是可排序的（即无后向性），否则问题就无法用动态规划求解
2. **选择状态：**将问题发展到各个阶段时所处于的各种客观情况用不同的状态表示出来。当然，状态的选择要满足无后效性。
3. **确定决策并写出状态转移方程：**之所以把这两步放在一起，是因为决策和状态转移有着天然的联系，状态转移就是根据上一阶段的状态和决策来导出本阶段的状态。所以，如果我们确定了决策，状态转移方程也就写出来了。但事实上，我们常常是反过来做，根据相邻两段的各状态之间的关系来确定决策。
4. **写出规划方程（包括边界条件）：**动态规划的基本方程是规划方程的通用形式化表达式。一般说来，只要阶段、状态、决策和状态转移确定了，这一步还是比较简单的。



1. 拆问题：把问题先分成子问题
2. 选择状态：
3. 确定决策并写出状态转移方程：
4. 

接下来就要去理解动态规划的思路了，通常情况下，DP题可从下面4个要素去逐步剖析：

**1. 状态是什么**

**2. 状态转移方程是什么**

**3. 状态的初始值是什么**

**4. 问题要求的最后答案是什么**



**写出状态转移方程是最困难的**，这也就是为什么很多朋友觉得动态规划问题困难的原因，我来提供我研究出来的一个思维框架，辅助你思考状态转移方程：

**明确 base case -> 明确「状态」-> 明确「选择」 -> 定义 dp 数组/函数的含义**。

按上面的套路走，最后的结果就可以套这个框架：

```
# 初始化 base case
dp[0][0][...] = base
# 进行状态转移
for 状态1 in 状态1的所有取值：
    for 状态2 in 状态2的所有取值：
        for ...
            dp[状态1][状态2][...] = 求最值(选择1，选择2...)
```

下面通过几道经典、且极其常见的面试题来看下动态规划解题套路



斐波那契数列上手后，我们看下 leetcode_70，据说是道正宗的动态规划问题。

### 一、爬楼梯（leetcode_70）

> 假设你正在爬楼梯。需要 n 阶你才能到达楼顶。每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？注意：给定 n 是一个正整数。
>
> **示例 ：**
>
> ```
> 输入： 2
> 输出： 2
> 解释： 有两种方法可以爬到楼顶。
> 1.  1 阶 + 1 阶
> 2.  2 阶
> ```

这是一道 easy 题，又想说脏话了，当时我拿到这么一道题后，一点想法都没有。

不管了，“穷举思想”

假设 n = 5，有 5 级楼梯要爬。每次都有 2 种选择：爬 1 级或爬 2 级。

如果爬 1 级，则剩下 4 级要爬。

如果爬 2 级，则剩下 3 级要爬。

这分出了 2 个子问题：爬 4 级楼梯有几种方式？爬 3 级楼梯有几种方式？

爬 5 级楼梯的方式数 = 爬 4 级楼梯的方式数 + 爬 3 级楼梯的方式数，这样往下递归分析

爬 4 级楼梯的方式数 = 爬 3 级楼梯的方式数 + 爬 2 级楼梯的方式数

。。。

一脸懵逼，这不是上一节的斐波那契数列吗？？？？？ 

用 $f(x)$ 表示爬到第 x 级台阶的方案数，考虑最后一步可能跨了一级台阶，也可能跨了两级台阶，所以我们可以列出如下式子：

$f(x) = f(x - 1) + f(x - 2)$

它意味着爬到第 $x$ 级台阶的方案数是爬到第 $x - 1$ 级台阶的方案数和爬到第 $x - 2$ 级台阶的方案数的和。





### 二、不同路径（leetcode_62）

> 一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。
>
> 机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。
>
> 问总共有多少条不同的路径？
>
> ![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/robot_maze.png)
>
> 例如，上图是一个7 x 3 的网格。有多少可能的路径？
>
> 示例 1:
>
> ```
> 输入: m = 3, n = 2
> 输出: 3
> 解释:
> 从左上角开始，总共有 3 条路径可以到达右下角。
> 
> 1. 向右 -> 向右 -> 向下
> 2. 向右 -> 向下 -> 向右
> 3. 向下 -> 向右 -> 向右
> ```
>
>
> 示例 2:
>
> ```
> 输入: m = 7, n = 3
> 输出: 28
> ```
>
> **提示：**
>
> - `1 <= m, n <= 100`
> - 题目数据保证答案小于等于 `2 * 10 ^ 9`



注意，这个网格相当于一个二维数组，数组是从下标为 0 开始算起的，所以右下角的位置是 $(m-1, n - 1)$，所以 $dp[m-1] [n-1]$ 就是我们要找的答案。

![](https://pic.leetcode-cn.com/1600324833-ZRJZXN-WechatIMG150%201.jpeg)

$dp[i][j]$表示到坐标(i,j)的路径条数。由于机器人从i=0,j=0出发，每次只能向下或者向右移动，因此，在所有坐标为（0，j)的位置机器人要到达的话只有一条路径（一直向下）；在所有坐标为（i,0)的位置，机器人要到达也只有一条路径（一直向右）。而要到达任一位置(i,j)的总路径条数，总是等于「 位置(i-1,j)的路径条数」 加上 「位置（i，j-1)的路径条数」。
因此，dp[i][j] = dp[i-1][j] + dp[i][j-1]

```java
public int uniquePaths(int m, int n) {
    if(m==0 || n==0) return 0;

    int[][] dp = new int[m][n];
    for(int i=0; i<m;i++){
        for(int j=0;j<n; j++){
            if(i==0 || j==0){ 
                dp[i][j]=1; //到达该位置只有一条路径
            }else{
                dp[i][j] = dp[i-1][j] + dp[i][j-1]; //动态规划
            }          
        }
    }
    return dp[m-1][n-1];
}
```



### 三、最大子序和（leetcode_53）

> 给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。
>
> 示例:
>
> ```
> 输入: [-2,1,-3,4,-1,2,1,-5,4]
> 输出: 6
> 解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
> ```
>

#### 小技巧——涨知识

拿到这类题目，避免不了的是要遍历，假设我们给定数组 [a,b,c,d,e] ，通常我们遍历子串或者子序列有如下三种遍历方式：

- 以某个元素开头的所有子序列，比如以 a 开头的子序列  [a]，[a, b]，[ a, b, c] ... 接着是以 b  开头的子序列 [b]，[b, c]，[b,c,d] ... 接着是 c 开头、d 开头...
- 以子序列的长度为基准，比如先遍历出子序列长度为 1 的子序列，再遍历出长度为 2 的 ...
- 以某个元素结尾的所有子序列，比如以 a 结束的子序列只有 [a]，以 b 结束的子序列 [a,b]，[b]，以 c 结束的子序列 [a,b,c]，[b,c]，[c]，以 d 结束的 ...

想想这道题，用哪种遍历方式合适一些呢？

用哪种遍历方式，可以逐个分析嘛。第一种遍历方式通常用于暴力解法，第二中后边我们也会用到（最长回文子串），第三种由于可以产生递推关系，动态规划问题用的挺多的。

#### 分析题目：

拿到这个题目先理解了意思，我们要求的是连续子数组的和最大那一个，所以我们肯定要遍历出所有子数组，并把每个子数组的和保存起来，然后去比较找到最大的那个就是我们要的结果了。

用暴力法从头遍历所有子序列，用两个变量，一个记录最大和，一个记录当前和，双层循环也可以解决。

因为我们的数组中可能有负数的情况，从头遍历的话，如有下一个元素是负数的话，和反而更小了，所以我们遍历以元素结尾的子序列，若前一个元素大于 0（$nums[i-1] > 0$），则将它加到当前元素上 $nums[i] = nums[i-1]+nums[i]$。最终 $nums[i]$ 保存的是以原先数组中 $nums[i]$ 结尾的最大子序列和。最后整体遍历一边 $nums[i]$ 就能找到整个数组最大的子序列和啦！

```java
public int maxSubArray(int[] nums) {
    if(nums==null || nums.length==0) {
        return 0;
    }
    for(int i = 1; i < nums.length; i++){
        //若前一个元素大于0，则将它加到当前元素上
        if(nums[i-1] > 0){
            //现在每个nums[i]里面保存的是以原先nums[i]结尾的最大子序和
            nums[i] = nums[i-1] + nums[i];
        }
    }
    //再遍历一边nums[i],找出最大的那个数就是整个数组的最大子序和
    int max = nums[0];
    for(int i = 1; i < nums.length; i++){
        if(nums[i] > max){
            max = nums[i];
        }
    }
    return max;
}
```

优化后：

![PNG](https://www.geekxh.com/assets/img/1.d0382e2a.jpg)

```java
public int maxSubArray(int[] nums) {
    int pre = 0, maxAns = nums[0];
    for (int x : nums) {
        pre = Math.max(pre + x, x);
        maxAns = Math.max(maxAns, pre);
    }
    return maxAns;
}
```



 TODO :按套路来，第一步拆分子问题，以每个元素结尾的子序列的和是各个子问题；



### 四、最长回文子串（leetcode_5）

> 给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。
>
> 示例 1：
>
> ```
> 输入: "babad"
> 输出: "bab"
> 注意: "aba" 也是一个有效答案。
> ```













![img](https://pic2.zhimg.com/80/v2-4e3a7d5ae4bb76ce96bc3393013f13f8_720w.jpg?source=1940ef5c)

### 五、凑零钱问题

先看下题目：给你 `k` 种面值的硬币，面值分别为 `c1, c2 ... ck`，每种硬币的数量无限，再给一个总金额 `amount`，问你**最少**需要几枚硬币凑出这个金额，如果不可能凑出，算法返回 -1 。算法的函数签名如下：

```
// coins 中是可选硬币面值，amount 是目标金额
int coinChange(int[] coins, int amount);
```

比如说 `k = 3`，面值分别为 1，2，5，总金额 `amount = 11`。那么最少需要 3 枚硬币凑出，即 11 = 5 + 5 + 1。

你认为计算机应该如何解决这个问题？显然，就是把所有可能的凑硬币方法都穷举出来，然后找找看最少需要多少枚硬币。

**1、暴力递归**

首先，这个问题是动态规划问题，因为它具有「最优子结构」的。**要符合「最优子结构」，子问题间必须互相独立**。啥叫相互独立？你肯定不想看数学证明，我用一个直观的例子来讲解。

比如说，你的原问题是考出最高的总成绩，那么你的子问题就是要把语文考到最高，数学考到最高…… 为了每门课考到最高，你要把每门课相应的选择题分数拿到最高，填空题分数拿到最高…… 当然，最终就是你每门课都是满分，这就是最高的总成绩。

得到了正确的结果：最高的总成绩就是总分。因为这个过程符合最优子结构，“每门科目考到最高”这些子问题是互相独立，互不干扰的。

但是，如果加一个条件：你的语文成绩和数学成绩会互相制约，此消彼长。这样的话，显然你能考到的最高总成绩就达不到总分了，按刚才那个思路就会得到错误的结果。因为子问题并不独立，语文数学成绩无法同时最优，所以最优子结构被破坏。

回到凑零钱问题，为什么说它符合最优子结构呢？比如你想求 `amount = 11` 时的最少硬币数（原问题），如果你知道凑出 `amount = 10` 的最少硬币数（子问题），你只需要把子问题的答案加一（再选一枚面值为 1 的硬币）就是原问题的答案，因为硬币的数量是没有限制的，子问题之间没有相互制，是互相独立的。

那么，既然知道了这是个动态规划问题，就要思考**如何列出正确的状态转移方程**？

**先确定「状态」**，也就是原问题和子问题中变化的变量。由于硬币数量无限，所以唯一的状态就是目标金额 `amount`。

**然后确定 `dp` 函数的定义**：当前的目标金额是 `n`，至少需要 `dp(n)` 个硬币凑出该金额。

**然后确定「选择」并择优**，也就是对于每个状态，可以做出什么选择改变当前状态。具体到这个问题，无论当的目标金额是多少，选择就是从面额列表 `coins` 中选择一个硬币，然后目标金额就会减少：

```
# 伪码框架
def coinChange(coins: List[int], amount: int):
    # 定义：要凑出金额 n，至少要 dp(n) 个硬币
    def dp(n):
        # 做选择，选择需要硬币最少的那个结果
        for coin in coins:
            res = min(res, 1 + dp(n - coin))
        return res
    # 我们要求的问题是 dp(amount)
    return dp(amount)
```

**最后明确 base case**，显然目标金额为 0 时，所需硬币数量为 0；当目标金额小于 0 时，无解，返回 -1：

```
def coinChange(coins: List[int], amount: int):

    def dp(n):
        # base case
        if n == 0: return 0
        if n < 0: return -1
        # 求最小值，所以初始化为正无穷
        res = float('INF')
        for coin in coins:
            subproblem = dp(n - coin)
            # 子问题无解，跳过
            if subproblem == -1: continue
            res = min(res, 1 + subproblem)

        return res if res != float('INF') else -1
    
    return dp(amount)
```

至此，状态转移方程其实已经完成了，以上算法已经是暴力解法了，以上代码的数学形式就是状态转移方程：

[![img](https://github.com/labuladong/fucking-algorithm/raw/master/pictures/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E8%AF%A6%E8%A7%A3%E8%BF%9B%E9%98%B6/coin.png)](https://github.com/labuladong/fucking-algorithm/blob/master/pictures/动态规划详解进阶/coin.png)

至此，这个问题其实就解决了，只不过需要消除一下重叠子问题，比如 `amount = 11, coins = {1,2,5}` 时画出递归树看看：

![](https://github.com/labuladong/fucking-algorithm/raw/master/pictures/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E8%AF%A6%E8%A7%A3%E8%BF%9B%E9%98%B6/5.jpg)

**时间复杂度分析：子问题总数 x 每个子问题的时间**。

子问题总数为递归树节点个数，这个比较难看出来，是 O(n^k)，总之是指数级别的。每个子问题中含有一个 for 循环，复杂度为 O(k)。所以总时间复杂度为 O(k * n^k)，指数级别。

**2、带备忘录的递归**

只需要稍加修改，就可以通过备忘录消除子问题：

```
def coinChange(coins: List[int], amount: int):
    # 备忘录
    memo = dict()
    def dp(n):
        # 查备忘录，避免重复计算
        if n in memo: return memo[n]

        if n == 0: return 0
        if n < 0: return -1
        res = float('INF')
        for coin in coins:
            subproblem = dp(n - coin)
            if subproblem == -1: continue
            res = min(res, 1 + subproblem)
        
        # 记入备忘录
        memo[n] = res if res != float('INF') else -1
        return memo[n]
    
    return dp(amount)
```

不画图了，很显然「备忘录」大大减小了子问题数目，完全消除了子问题的冗余，所以子问题总数不会超过金额数 n，即子问题数目为 O(n)。处理一个子问题的时间不变，仍是 O(k)，所以总的时间复杂度是 O(kn)。

**3、dp 数组的迭代解法**

当然，我们也可以自底向上使用 dp table 来消除重叠子问题，`dp` 数组的定义和刚才 `dp` 函数类似，定义也是一样的：

**`dp[i] = x` 表示，当目标金额为 `i` 时，至少需要 `x` 枚硬币**。

```
int coinChange(vector<int>& coins, int amount) {
    // 数组大小为 amount + 1，初始值也为 amount + 1
    vector<int> dp(amount + 1, amount + 1);
    // base case
    dp[0] = 0;
    for (int i = 0; i < dp.size(); i++) {
        // 内层 for 在求所有子问题 + 1 的最小值
        for (int coin : coins) {
            // 子问题无解，跳过
            if (i - coin < 0) continue;
            dp[i] = min(dp[i], 1 + dp[i - coin]);
        }
    }
    return (dp[amount] == amount + 1) ? -1 : dp[amount];
}
```

![](https://github.com/labuladong/fucking-algorithm/raw/master/pictures/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E8%AF%A6%E8%A7%A3%E8%BF%9B%E9%98%B6/6.jpg)

PS：为啥 `dp` 数组初始化为 `amount + 1` 呢，因为凑成 `amount` 金额的硬币数最多只可能等于 `amount`（全用 1 元面值的硬币），所以初始化为 `amount + 1` 就相当于初始化为正无穷，便于后续取最小值。

### 三、最后总结

第一个斐波那契数列的问题，解释了如何通过「备忘录」或者「dp table」的方法来优化递归树，并且明确了这两种方法本质上是一样的，只是自顶向下和自底向上的不同而已。

第二个凑零钱的问题，展示了如何流程化确定「状态转移方程」，只要通过状态转移方程写出暴力递归解，剩下的也就是优化递归树，消除重叠子问题而已。

如果你不太了解动态规划，还能看到这里，真得给你鼓掌，相信你已经掌握了这个算法的设计技巧。

**计算机解决问题其实没有任何奇技淫巧，它唯一的解决办法就是穷举**，穷举所有可能性。算法设计无非就是先思考“如何穷举”，然后再追求“如何聪明地穷举”。

列出动态转移方程，就是在解决“如何穷举”的问题。之所以说它难，一是因为很多穷举需要递归实现，二是因为有的问题本身的解空间复杂，不那么容易穷举完整。

备忘录、DP table 就是在追求“如何聪明地穷举”。用空间换时间的思路，是降低时间复杂度的不二法门，除此之外，试问，还能玩出啥花活？









刚开始学的时候，看好多文章喜欢从 斐波那契数列 入手，我，，，，我，，连斐波那契数列都忘了，，，



### 买卖股票的最佳时机

> 买卖股票的最佳时机
> 给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。
>
> 如果你最多只允许完成一笔交易（即买入和卖出一支股票一次），设计一个算法来计算你所能获取的最大利润。
>
> 注意：你不能在买入股票前卖出股票。
>
> 示例 1:
>
> ```
> 输入: [7,1,5,3,6,4]
> 输出: 5
> 解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
>      注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
> ```
>
> 示例 2:
>
> ```
> 输入: [7,6,4,3,1]
> 输出: 0
> 解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
> ```





### 打家劫舍

> 你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。
>
> 给定一个代表每个房屋存放金额的非负整数数组，计算你 不触动警报装置的情况下 ，一夜之内能够偷窃到的最高金额。
>
> 示例 1：
>
> ```
> 输入：[1,2,3,1]
> 输出：4
> 解释：偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
>      偷窃到的最高金额 = 1 + 3 = 4 。
> ```
>
> 示例 2：
>
> ```
> 输入：[2,7,9,3,1]
> 输出：12
> 解释：偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。
>      偷窃到的最高金额 = 2 + 9 + 1 = 12 。
> ```
>
>
> 提示：
>
> 0 <= nums.length <= 100
> 0 <= nums[i] <= 400



