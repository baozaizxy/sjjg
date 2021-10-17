# 第5章  散列

散列是一种以常数平均时间执行插入、删除和查找的技术。但是需要元素间任何排序信息的操作将不会得到有效支持。

## 5.1一般想法

理想的散列表数据结构只不过是一个含有关键字的具有固定大小的数字

不同关键字通过相同的散列函数不能计算出同一地址

表的大小记为TableSize

散列函数要在单元之间均匀的分配关键字

**待解决问题：要选择一个函数，决定当两个关键字散列到同一值的时候（称为冲突）应该做什么以及如何确定散列表的大小**

## 5.2散列函数

好的散列函数：计算简单+（计算得到的散列地址）分布均匀

Key mod TableSize

一般保证表的大小为素数

当输入关键字是随机整数时，散列函数不仅算起来简单而且关键字的分配也很均匀

通常关键字是字符串

1、把字符串中字符的ASCII码值加起来

2、 假设Key至少有两个字符外加NULL结束符

​     虽然3个字符有17576种可能但实际不同的组合仅有2851种

## 5.3分离链表法

缺点：需要指针，由于给新单元 分配地址需要时间，因此导致了算法的速度有些减慢

## 5.4开放定址法

/*处理散列冲突的方法*/

如果有冲突发生就要尝试选择另外的单元，直到找出空的单元为止。

单元h0(X),h1(X),h2(X)...相继试选，其中

hi(X)=（Hash(X)+F(i)）mod TableSize  

   （  F（0）=0）

函数F是解决冲突的方法。

一般来说装填因子应该低于拉姆达=0.5

#### 5.4.1线性探测法

F是i的线性函数，典型情况是F（i）=i

缺点：

花费时间且即使表比较空占据的单元也会形成聚集。

插入和不成功查找需要相同次数的探测

#### 5.4.2平方探测法

平方探测是消除线性探测中一次聚集问题的冲突解决方法

F(i)=i的平方

缺点：

表的性能会降低且当表被填满超过一半，就不能保证一次找到一个空单元。因为最多有一半的表用作解决冲突的备选位置。

###### 定理：如果表有一半是空的，且表的大小为素数，那么我们保证总能够插入一个新的元素

#### 5.4.3双散列

F（i）=i*hash2(X)

这个公式是说我们将第二个散列函数应用到X并在距离hash2(X)，2hash2(X)等处探测

hash2(X)=R-（X modR）这样的函数将起到良好的作用

如果表的大小不是素数，那么备选单元就可能提前用完。

如果双散列正确实现，则模拟表明，预期的探测次数几乎和随机冲突解决方法的情形相同

## 5.5再散列

对于使用平方探测的开放定址散列法，如果表填得太满，那么运行时间会过长且Insert可能会失败。

解决方案：建立另外一个大约两倍大的表（并且使用一个相关的新散列函数），扫描整个原始散列函表，计算每个元素位置并插入

再散列之前必然已经存在N/2次Insert，运行时间O(N)添加到每个插入上的花费基本上是一个常数开销

再散列可以用平方探测以多种方法实现

1、只要表填满一半就再散列

2、只有当插入失败时才再散列

3、当表到达某一填充因子时进行再散列

## 5.6可扩散列

处理数据量太大以至于存不进主存的情况

可扩散列允许用两次磁盘访问执行一次Find

# 感受

正在学习的这本书是翻译过来的有些地方读着不太通顺，并且直接啃书的过程还是比较痛苦的，很多很好理解的点用规范化的语言描述出来就变得十分抽象难懂，这周到最后了才看视频，书中一些我之前没懂的地方瞬间茅塞顿开了，下周可以考虑先看视频再看书。


