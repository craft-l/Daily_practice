#### Dijkstra算法

重新复习一下Dijkstra算法

Dijkstra算法是一种基于贪心策略的算法，用于求单源最短路径（单源：从一个顶点出发,Dijkstra算法只能求一个顶点到其他点的最短距离而不能任意两点）。每次新扩展一个路程最短的点，更新与其相邻的点的路程。注意在权值为负的情况下，Dijkstra算法不适用。

贪心算法是指，在对问题求解时，总是做出在当前看来是最好的选择。也就是说，不从整体最优上加以考虑，他所做出的是在某种意义上的局部最优解。如在Dijkstra算法中，我们总是选定离起点最近的点加入已选定点集合中。

三个步骤：①：更新结点信息     ②：扫描未选定结点   ③：选定最近点







![image-20210905194509310](C:\Users\phantump\AppData\Roaming\Typora\typora-user-images\image-20210905194509310.png)

我们将所有点分为已选的顶点与未选的顶点。

首先，我们选定一个点做为起点，这里选定A做为起点，D为目的点，A为已选定点，其余点为未选定点，初始时起点与未选定点的距离设为无穷大。

![image-20210906092838927](C:\Users\phantump\AppData\Roaming\Typora\typora-user-images\image-20210906092838927.png)

![](C:\Users\phantump\AppData\Roaming\Typora\typora-user-images\image-20210906090742033.png)

接下来扫描未选定点，A相邻点为B、F、G、H，则我们选定最近的H加入已选定点集合中，此时已经选定点集合为{A、H}，更新结点信息，H的父结点为A，状态改变为已选定，距离定为1。

![image-20210906093040874](C:\Users\phantump\AppData\Roaming\Typora\typora-user-images\image-20210906093040874.png)

![image-20210906091448117](C:\Users\phantump\AppData\Roaming\Typora\typora-user-images\image-20210906091448117.png)

接下来重复以上步骤。继续扫描未选定点，A、H的相邻点为B、F、G，我们选定最近的G加入已选定点中，此时已经选定点的集合为{A，H，G}，更新结点信息，E与A距离更新为11，父结点改为G，F与A距离更新为8，父结点改为G，继续扫描。

![image-20210906094501693](C:\Users\phantump\AppData\Roaming\Typora\typora-user-images\image-20210906094501693.png)

A->G->F小于A->F，更新结点F与起点的距离，将父结点由A改为G，选定最近点B加入选定点中......







得下表，则A到D点最近距离为16。

注意经过点与起点的最短距离也已经确定。

![image-20211009220450250](C:\Users\phantump\AppData\Roaming\Typora\typora-user-images\image-20211009220450250.png)







### unordered_set和unordered_map

  C++ 11中出现了两种新的关联容器:unordered_set和unordered_map，其内部实现与set和map大有不同，set和map内部实现是基于RB-Tree，而unordered_set和unordered_map内部实现是基于哈希表(hashtable)，由于unordered_set和unordered_map内部实现的公共接口大致相同，所以本文以unordered_set为例。
        unordered_set是基于哈希表，因此要了解unordered_set，就必须了解哈希表的机制。哈希表是根据关键码值而进行直接访问的数据结构，通过相应的哈希函数(也称散列函数)处理关键字得到相应的关键码值，关键码值对应着一个特定位置，用该位置来存取相应的信息，这样就能以较快的速度获取关键字的信息。比如：现有公司员工的个人信息（包括年龄），需要查询某个年龄的员工个数。由于人的年龄范围大约在[0，200]，所以可以开一个200大小的数组，然后通过哈希函数for(key) = key得到key对应的key-value，这样就能完成统计某个年龄的员工个数。而在这个例子中，也存在这样一个问题，两个员工的年龄相同，但其他信息（如：名字、身份证）不同，通过前面说的哈希函数，会发现其都位于数组的相同位置，这里，就涉及到“冲突”。准确来说，冲突是不可避免的，而解决冲突的方法常见的有：开发地址法、再散列法、链地址法(也称拉链法)。而unordered_set内部解决冲突采用的是----链地址法，当用冲突发生时把具有同一关键码的数据组成一个链表。下图展示了链地址法的使用:

<img src="C:\Users\phantump\AppData\Roaming\Typora\typora-user-images\image-20211001200300154.png" alt="image-20211001200300154" style="zoom:50%;" />

### tree

二叉树 红黑树 搜索树 前缀树

#### 并查集

摩尔投票法





























