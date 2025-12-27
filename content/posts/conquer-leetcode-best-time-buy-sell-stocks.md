+++
title = "分治 leetcode「买股票的最佳时间」系列问题"
date = 2025-12-26
extra.toc = true
[taxonomies]
tags = ["programming", "algo", "leetcode"]
+++

「买股票的最佳时间」问题系列是典型的线性结构分治。
解决这类问题的思路非常简单，即：

将输入价格数组`prices`分为最后一个元素`p`和前面的前缀`ps`，也就是`prices = ps.append(p)`
设函数`f`对输入价格数组得到最大利润，
对`ps`递归得到对于`ps`的最大利润`f(ps)`，然后思考一个问题：

> *我需要前面对`ps`的递归提供什么**额外的信息**才能从`f(ps)`得到`f(prices)`？*

然后由于我们是在递归，所以既然要求`f(ps)`给出额外的信息，那么`f(prices)`也需要同样给出自己范围内的额外的信息。
我们根本不需要在意什么「动态规划」之类的表述，这些题目都非常简单。

接下来我们每个题目都进行同样的分析，展示为何所有这类问题的解决方式都简单而单一。

---

## 其一
### [题](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/description/)
给定一个数组 `prices` ，它的第 `i` 个元素 `prices[i]` 表示一支给定股票第 `i` 天的价格。

你只能选择 某一天 买入这只股票，并选择在 未来的某一个不同的日子 卖出该股票。设计一个算法来计算你所能获取的最大利润。
返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 0 。

> 示例 1：  
> 
> 输入：[7,1,5,3,6,4]  
> 输出：5  
> 解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。  
> 注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。  

### 解
由于我们已知`f(ps)`的最大利润，为了获得`f(prices)`，我们需要知道`ps`中最小的价格，然后在之前最小价格买入，在`p`这天卖出，
然后把这笔交易和`f(ps)`之前的最大利润比较即可：
```rust
pub fn max_profit(prices: Vec<i32>) -> i32 {
    let mut ans = 0;
    let mut min = prices[0];
    for p in &prices[1..] {
        let profit = *p - min;
        ans = ans.max(profit);
        min = min.min(*p);
    }
    ans
}
```


## 其二
### [题](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/description/)
给你一个整数数组 `prices` ，其中 `prices[i]` 表示某支股票第 `i` 天的价格。

在每一天，你可以决定是否购买和/或出售股票。你在任何时候 最多 只能持有 一股 股票。然而，你可以在 同一天 多次买卖该股票，但要确保你持有的股票不超过一股。
返回 你能获得的 最大利润 。

> 示例 1：  
>   
> 输入：prices = [7,1,5,3,6,4]  
> 输出：7  
> 解释：在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5 - 1 = 4。  
> 随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6 - 3 = 3。  
> 最大总利润为 4 + 3 = 7 。

### 解
这道题看上去多一个要求，其实难度没啥变化（其实所有这类问题难度都差不多简单），一样的思路：

已知`f(ps)`, `p`和`ps`，我们想得到`f(prices)`，于是我们思考需要`f(ps)`给出除了最大利润之外的什么额外信息才能组合出`f(prices)`；
很自然可以发现，我们需要`ps`范围内手持股票的情况下的利润最大值；

这里有趣的是，我们还会发现，为了得到「`ps`范围内手持股票的情况下的利润最大值」，
我们还需要「`ps`范围内已经交易完成的情况下的利润最大值」。

```rust
pub fn max_profit(prices: Vec<i32>) -> i32 {
    let mut hold = -prices[0];
    let mut sold = 0;
    let mut ans = sold;
    for i in 1..prices.len() {
        let p = prices[i];
        hold = hold.max(sold - p);
        sold = sold.max(hold + p);
        ans = ans.max(sold);
    }
    ans
}
```

## 其三
### [题](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/description/)
给定一个数组，它的第 `i` 个元素是一支给定的股票在第 `i` 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 两笔 交易。
注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

> 示例 1:  
>   
> 输入：prices = [3,3,5,0,0,3,1,4]   
> 输出：6  
> 解释：在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。  
> 随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。  


### 解
这题被标记为困难，实际上很简单。
由于我们最多只能交易2次，所以我们还需要第一次手持股票和第二次手持股票这两个额外信息，仔细一思考其实和前面的题目没有什么区别。

```rust
pub fn max_profit(prices: Vec<i32>) -> i32 {
    let Some(&a) = prices.get(0) else {
        return 0;
    };
    let mut ans = 0;
    let mut hold1 = -a;
    let mut hold2 = -a;
    let mut sold1 = 0;

    for p in prices.into_iter().skip(1) {
        let sold2 = sold1.max(hold2 + p);
        hold2 = hold2.max(sold1 - p);
        sold1 = sold1.max(hold1 + p);
        hold1 = hold1.max(-p);
        ans = ans.max(sold1).max(sold2);
    }
    ans
}
```

## 其四
### [题](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/description/)
给你一个整数数组 `prices` 和一个整数 `k` ，其中 `prices[i]` 是某支给定的股票在第 `i` 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 `k` 笔交易。也就是说，你最多可以买 `k` 次，卖 `k` 次。
注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

> 示例 1：  
>   
> 输入：k = 2, prices = [2,4,1]  
> 输出：2  
> 解释：在第 1 天 (股票价格 = 2) 的时候买入，在第 2 天 (股票价格 = 4) 的时候卖出，这笔交易所能获得利润 = 4-2 = 2 。

### 解
这只是「其三」的推广，仍然十分简单，甚至写起来更容易了。
```rust
pub fn max_profit(k: i32, prices: Vec<i32>) -> i32 {
    let k = k as usize;
    let mut hold = vec![0; k + 1];
    let mut sold = vec![0; k + 1];
    let mut ans = 0;

    let Some(&a) = prices.first() else {
        return 0;
    };

    for i in 1..=k {
        hold[i] = -a;
    }

    for p in prices.into_iter().skip(1) {
        for i in 1..=k {
            hold[i] = hold[i].max(sold[i - 1] - p);
            sold[i] = sold[i].max(hold[i] + p);
            ans = ans.max(sold[i]);
        }
    }
    ans
}
```


## 含手续费
### [题](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/description/)
给定一个整数数组 `prices`，其中 `prices[i]`表示第 `i` 天的股票价格 ；整数 `fee` 代表了交易股票的手续费用。

你可以无限次地完成交易，但是你每笔交易都需要付手续费。如果你已经购买了一个股票，在卖出它之前你就不能再继续购买股票了。
返回获得利润的最大值。
注意：这里的一笔交易指买入持有并卖出股票的整个过程，每笔交易你只需要为支付一次手续费。

> 示例 1：
> 
> 输入：prices = [1, 3, 2, 8, 4, 9], fee = 2  
> 输出：8   
> 解释：能够达到的最大利润:   
> 在此处买入 prices[0] = 1  
> 在此处卖出 prices[3] = 8  
> 在此处买入 prices[4] = 4  
> 在此处卖出 prices[5] = 9  
> 总利润: ((8 - 1) - 2) + ((9 - 4) - 2) = 8


### 解
看似变化不规则，其实只是在组合额外信息的时候注意减去手续费即可。
```rust
pub fn max_profit(prices: Vec<i32>, fee: i32) -> i32 {
    let Some(&a) = prices.first() else {
        return 0;
    };

    let mut hold = -a;
    let mut sold = 0;
    let mut ans = 0;

    for p in prices.into_iter().skip(1) {
        let hold2 = hold.max(sold - p);
        sold = sold.max(hold + p - fee);
        hold = hold2;
        ans = ans.max(sold);
    }

    ans
}
```


## 含冷冻期
### [题](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/description/)
给定一个整数数组`prices`，其中第  `prices[i]` 表示第 `i` 天的股票价格 。​

设计一个算法计算出最大利润。在满足以下约束条件下，你可以尽可能地完成更多的交易（多次买卖一支股票）:

卖出股票后，你无法在第二天买入股票 (即冷冻期为 1 天)。
注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

> 示例 1:
> 
> 输入: prices = [1,2,3,0,2]  
> 输出: 3   
> 解释: 对应的交易状态为: [买入, 卖出, 冷冻期, 买入, 卖出] 

### 解
这里额外的信息需要间隔一天之前交易完成的最大利润和前面一天刚交易完成的最大利润，其他和前面题目没什么区别；
```rust
pub fn max_profit(prices: Vec<i32>) -> i32 {
    let Some(&a) = prices.first() else {
        return 0;
    };

    let mut hold = -a;
    let mut sold = 0;
    let mut sold0 = 0;
    let mut ans = 0;

    for p in prices.into_iter().skip(1) {
        let hold2 = hold.max(sold - p);
        sold = sold.max(sold0);
        sold0 = hold + p;
        hold = hold2;
        ans = ans.max(sold);
    }

    ans.max(sold0)
}
```

