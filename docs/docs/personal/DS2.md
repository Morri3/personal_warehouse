# 数据结构错题整理


### 前言

所整理的错题仅供参考，欢迎交流。



1、串的长度是指：串中包含的字符个数

2、设有两个串p和q，其中q是p的子串，求q在p中首次出现的位置的算法称为：模式匹配

**注**：KMP算法是模式匹配的一种

3、设主串的长度为n，模式串的长度为m，则串匹配的KMP算法时间复杂度是：O(n + m)

4、串是一种线性表，不过它的数据元素是：字符

5、稀疏矩阵一般的压缩存储方法有：三元组和十字链表

6、设有一个 10 阶的对称矩阵 A，采用压缩存储方式，以行序为主存储，a[1, 1] 为第一元素，其存储地址为 1，每个元素占一个地址空间，则 a[8, 5] 的地址为：33。

**解析：** 数组下标从1开始，只存储其下三角形元素，在a(8,5)的前面有7行，第1行有1个元素，第2行有2个元素，…，第7行有7个元素，这7行共有(1+7)×7/2=28个元素，在第8行中，a(8,5)前有4个元素，故a(8,5)前有28+4=32个元素，a(8,5)地址为33。

**另解：** 8*8的下三角总共有((1+8)*8)/2=36个，减去三个，就是a(8,5)。

7、广义表 A=(a,b,(c,d),(e,(f,g)))，则 Head( Tail( Head( Tail( Tail(A) ) ) ) ) 的值为：__d__

**解析：** 
tail第一步： (b,(c,d),(e,(f,g)))
tail第二步：((c,d),(e,(f,g)))
head第三步：(c,d)
tail第四步：(d)
head第五步：d

8、有n个数存放在一维数组A[1..n]中，在进行顺序查找时，这n个数的排列有序或无序其平均查找长度相同，均为(n+1)/2。

9、折半查找法的查找速度不一定比顺序查找法快

10、如果从有向图 G 的每一点均能通过深度优先搜索遍历到所有其它顶点，那么该图一定不存在拓扑序列。因为如果从有向图 G 的每一点均能通过深度优先搜索遍历到所有其它顶点，则该图是一个有环图；而拓扑排序的前提是有向无环图（DAG）。

11、BFS can work out the shortest path when costs of all the edges are equal.当所有边的代价相等时，BFS算法可以求出最短路径。

12、Single-source algorithms work fast on sparse graphs when finding the shortest path between any pair of vertices.单源算法在寻找任意一对顶点之间的最短路径时，在稀疏图上工作得很快。

13、任何一个无向连通图的最小生成树有一棵或多棵

14、Let T be a tree created by union-by-size with N nodes, then the height of T can be at most log2(N)+1.设T是由N个节点按大小并集而成的树，则T的高度最多为log2(N)+1。

15、Let T be a tree of N nodes created by union-by-size without path compression, then the minimum depth of T may be 1.设T是由N个节点按大小并集而成的树，不进行路径压缩，则T的最小深度可以是1。

16、对于不同的字符，每个字符的权重都不小于2。任何非叶节点的权重必须不小于下一级上任何节点的权重。

17、next lower level下一级

18、optimal prefix codes最佳前缀码

19、The inorder traversal sequence（中序遍历（左根右）） of an AVL tree must be in sorted (non-decreasing) order. 根据二叉搜索树性质，中序遍历一定是有序的，而且是递增的。

20、Preorder前序（根左右）    
Postorder后序（左右根）

21、If graph G is a connected graph, the spanning tree of G is a maximal connected subgraph containing all n vertices of G.如果图G是连通图，则G的生成树是包含G的所有n个顶点的最大连通子图。

