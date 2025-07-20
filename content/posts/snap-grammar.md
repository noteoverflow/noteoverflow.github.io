+++
title = "SNAP：一种超轻量英语语法框架"
date = 2025-07-20
extra.toc = true
extra.katex = true
[taxonomies]
tags = ["linguistics"]
+++

之前我希望建立一个更轻量化的英语语法系统帮助学习者快速建立直觉：
> [基于「修饰」和「省略」的轻量级英语语法系统](/posts/light-weight-english-syntax)

今天我尝试将这一套方式系统化并整理成了**SNAP**框架，该框架有三个核心拼图：
- 修饰
- 省略
- 概率

接下来将逐个进行阐述。
在阐述前，再次重申：

> 本语法框架是为了语言的使用服务，仅为粗略描述，在熟练之后即可忘记本框架。

> 我没有时间，我没有时间，只能粗略写写
---
# 修饰
何谓修饰？修饰即一种特殊的「关系」而已，所谓关系，结构为：

$$
x \rightarrow y
$$

这里表示$x$修饰$y$。

举几个例子。比如常见的句子构成「主谓」结构：

> Tom likes learning math.

此处 "*likes learning math*" 作为谓语修饰主语 "*Tom*" ，而 "*learning math*" 又用来修饰 "*likes*" 来补全 "*likes*" 的内容。
形容词，副词等传统语法中的分类的修饰关系更加显然。

## SNAP
接下来我们进入SNAP的核心，即根据修饰关系的结构进行粗略的分类。我们可以把修饰的结构按照其是否自我修饰和修饰语序分为如下：

|名称|结构|说明|
|---|---|---|
|*N*|$x \rightarrow x$|自修饰|
|*A*|$x \rightarrow$|前置他修饰|
|*P*|$\rightarrow x$|后置他修饰|

我们来举几个例子。
比如名词或名词短语均为*N*，所有形容词类均可作为*A*，而*P*十分复杂，我们需要专门来讨论他。
*P*在传统语法中可以有如下几种可能：
- verb obj.
- linking-verb complement
- adv.
- clause
- obj.

具体而言，前两种是句子谓语的构成方式，即「动词+宾语」和「系动词+补语」。
后三种分别为「副词」、「从句」和「宾语」（没错，宾语可以看作修饰前面的动词！）。

有了这些概念我们就可以定义什么是句子，也就是SNAP中的*S*。

> 句子（S）即 使用*N*开头，并使用上述前两种*P*作为开头的后置修饰的结构。

这么一来，从句也就顺理成章的可以被识别了。

## 转换
在英语中，一个词的分类不是固定的（或者，如果你喜欢类型论，可以认为同一个词可以在不同类型之间被影射）。

> 分类不是由词本身决定，而是由其在句子中的结构和身份来决定。

建立了这种观念之后，我们就可以分类讨论不同的转换：

<center>
<img src="/img/blog/snap-grammar/snap-convertion.png" width=300/><br/>
</center>

### NAP转换
首先我们关注 NAP 这三剑客。
#### $N \rightarrow A$
「自修饰体」可以转换为「前置他修饰体」。

这十分常见，比如 "*book shelf*" 其中 *book* 本是自修饰的名词，此处却被作为前置修饰用来修饰 *shelf*。 

#### $N \rightarrow P$
「自修饰体」可以转换为「后置修饰体」。

这也非常常见，主要有以下两大情况：
- 作为宾语修饰动作：比如 "*play piano*" 中 *piano* 后置修饰 *play*;
- 加上系动词作为谓语：比如 "*He is Tom*" 中 *Tom* 加上 *is* 即可后置修饰 *He*;

#### $P \rightarrow N$
「后置修饰体」可转换为「自修饰体」。

比如动名词和动名词短语。

#### $A \rightarrow P$
「前置修饰体」可转换为「后置修饰体」

比如通过增加系动词转换为谓语。
有比如宾语补语、同位语等。

#### $P \rightarrow A$
**部分**「后置修饰体」可转换为「前置修饰体」。

注意这里仅是*部分*可转换。
比如部分简单动词可以通过「动状词」转换为形容词。


### S 转换
S 可以被转换为 NP 其一，其实就是传统语法中的各种从句。
这里由于时间原因不再赘述，仅进行如下梳理：
|结构|说明|
|---|---|
|$S \rightarrow N$|名词性从句|
|$S \rightarrow P$|定语从句，关系从句|

## 不规则修饰
除了上述根据语序可大致划分的修饰之外，其实还有不规则的修饰方式。
根据「时态」和「语气」可以对动词进行各种变形，这些均属于不规则修饰（即同时前置，后置，还有可能是不规则变化）。
这类需要专门处理。

---
# 省略
接下来进入第二块拼图：「省略」。
省略是一种十分强大的工具，省略的通则是：

> 省略从句中的主语与系动词，只留补语。

可是如果从句中没有系动词和补语怎么办？没关系，我们还有下面两条补充规则：
## 有助动词时，变成不定词
You must go at once.  
→ You are to go at once. （你必须马上离开。）

The train will leave in 10 minutes.  
→ The train is to leave in 10 minutes. （火车 10 分钟后开动。）

He should do as I say.  
→ He is to do as I say. （他该按我说的去做。）

You may call me "Sir."  
→ You are to call me "Sir." （你可以叫我“先生”。）

## 无助动词时，变成V-ing


---
# 概率
以上使用「修饰」和「省略」的语法系统是十分粗略的，现实世界中有许多特殊情况和惯用法，需要在日常使用中去习惯和积累，这里推荐一本书：
[English Grammar in use](https://www.amazon.com/English-Grammar-Use-Book-Answers/dp/1108457657)

<center>
<img src="/img/blog/snap-grammar/english-grammar-in-use.jpg" width=300/><br/>
</center>

